# Система підтримки (Support Tickets)

## Огляд

Вбудована система тікетів підтримки для адміністраторів студії. Тікет створюється в адмін-панелі, потрапляє в чергу на Pi-сервер, де Claude Code аналізує його і автоматично відповідає, задає уточнюючі питання, або ескалює як баг/фіча-реквест у Jira.

Клієнт (адмін) ніколи не бачить ні Jira, ні Pi — комунікація завжди через сторінку `/support` в адмін-додатку.

---

## Архітектура

```
┌─────────────────────┐         ┌──────────────────────────┐
│ fitstudiocrm-app    │         │ fitstudiocrm-server      │
│ /support route      │ <─────> │ /support/* (client)      │
│   list / detail     │  REST   │ /support-internal/*      │
│   create + screen   │         │   (HMAC-signed, no auth) │
│   10-min poll modal │         │ DB: support_ticket / msg │
└─────────────────────┘         └────────────┬─────────────┘
                                             │ POST /v1/ticket-event
                                             │ (HMAC, request_id)
                                             ▼
┌──────────────────────────────────────────────────────────┐
│ Pi: handler-support (NestJS)                             │
│ ─ POST /v1/ticket-event → Redis priority queues          │
│ ─ GET  /health, /health/metrics                          │
│ ─ HMAC middleware, request_id dedup                      │
└────────────┬─────────────────────────────────────────────┘
             │ systemd timer (кожні 10 хвилин)
             ▼
┌──────────────────────────────────────────────────────────┐
│ Claude one-shot (process-queue.ts)                       │
│ ─ Pop тікет з Redis (priority order)                     │
│ ─ Fetch деталі через /support-internal                   │
│ ─ Рішення: answer | question | escalate                  │
│ ─ POST коментар назад через /support-internal            │
│ ─ Якщо escalate → Jira issue + Slack alert              │
└──────────────────────────────────────────────────────────┘
```

---

## База даних

### support_ticket

| Поле | Тип | Опис |
|------|-----|------|
| id | UUID (PK) | |
| subject | VARCHAR | Тема тікета |
| body | TEXT | Опис проблеми |
| priority | ENUM | low, medium, high, critical |
| status | ENUM | open, awaiting_user, resolved, closed |
| createdByUserId | UUID | ID адміна що створив |
| createdAt | TIMESTAMPTZ | |
| updatedAt | TIMESTAMPTZ | |
| lastNotifiedAt | TIMESTAMPTZ | Коли останній раз Pi був повідомлений |

### support_message

| Поле | Тип | Опис |
|------|-----|------|
| id | UUID (PK) | |
| ticketId | UUID (FK) | → support_ticket.id |
| authorKind | ENUM | user, support |
| authorUserId | UUID | Тільки для user |
| body | TEXT | Текст повідомлення |
| kind | ENUM | text, answer, question, defect_created |
| jiraKey | VARCHAR | Ключ Jira issue (тільки для defect_created) |
| createdAt | TIMESTAMPTZ | |

### support_attachment

| Поле | Тип | Опис |
|------|-----|------|
| id | UUID (PK) | |
| messageId | UUID (FK) | → support_message.id |
| filename | VARCHAR | Оригінальне ім'я файлу |
| mimeType | VARCHAR | |
| sizeBytes | INT | |
| storageUrl | VARCHAR | Шлях на FS |
| createdAt | TIMESTAMPTZ | |

---

## API Endpoints

### Client-facing (Firebase auth, Admin/SuperAdmin)

| Метод | Шлях | Опис |
|-------|------|------|
| GET | /support/tickets | Список тікетів поточного юзера |
| GET | /support/tickets/:id | Деталі + повідомлення + вкладення |
| POST | /support/tickets | Створити тікет {subject, body, priority} |
| POST | /support/tickets/:id/messages | Додати повідомлення + файли (до 5) |
| GET | /support/unread-count | Кількість тікетів зі статусом awaiting_user |

### Internal (HMAC auth, без Firebase)

| Метод | Шлях | Опис |
|-------|------|------|
| GET | /support-internal/ticket/:id?appId= | Повний тікет для Claude |
| POST | /support-internal/ticket/:id/comment?appId= | Claude постить відповідь |
| GET | /support-internal/attachment-data/:id?appId= | Base64 вкладення |
| GET | /support-internal/attachment/:id/file?appId= | Raw файл (download) |

---

## Обмеження

- **1 тікет на годину** на appId (rate limit)
- **10 повідомлень** максимум на тікет
- **5 файлів** максимум на повідомлення

---

## Frontend (fitstudiocrm-app)

**Сторінка:** `/support` — доступ Admin/SuperAdmin.

**Компоненти:**
- Ліва панель — список тікетів з фільтром по статусу
- Права панель — detail view (messenger-стиль: user праворуч, Support Bot ліворуч)
- Modal створення — тема, опис, пріоритет
- Reply box — textarea + file attach

**Poll:** `useSupportStore` опитує `GET /support/unread-count` кожні 10 хвилин. Якщо з'явились нові відповіді — модалка "Підтримка відповіла" з кнопкою переходу.

---

## handler-support (Pi NestJS)

**Репозиторій:** `goodpesik/handler-support`

**Компоненти:**
- `ticket-event.controller.ts` — прийом webhook, dedup, enqueue
- `redis.service.ts` — priority queues (critical/high/medium/low), in_flight ZSET
- `hmac.middleware.ts` — HMAC-SHA256 верифікація з anti-replay (±5 хв)
- `health.controller.ts` — `/health` + `/health/metrics`

**Consumer:** `scripts/process-queue.ts`
- Pop тікет з Redis (priority order)
- Move до in_flight (visibility timeout 15 хв)
- Fetch деталі + вкладення через product API
- Побудова промпта + запуск Claude CLI
- Parse JSON рішення (answer/question/escalate)
- POST результат через `/support-internal`
- При escalate: Jira issue (label `auto:support`) + Slack webhook
- При timeout: Jira issue + Slack + fallback відповідь юзеру

**Systemd:** timer кожні 10 хвилин → oneshot service.

---

## HMAC схема

Headers на кожному запиті:
```
X-Support-Product:    fitstudio
X-Support-Timestamp:  <unix seconds>
X-Support-Request-Id: <UUID>
X-Support-Signature:  HMAC-SHA256(secret, "METHOD\n/path\n{timestamp}\n{body}")
```

Anti-replay: ±5 хвилин від поточного часу.

---

## Claude рішення

| Рішення | Дія | kind |
|---------|-----|------|
| answer | Покрокова інструкція | answer |
| question | Уточнююче питання | question |
| escalate | Баг/фіча → Jira + Slack | defect_created |

Всі відповіді — **тільки українською**.

---

## Environment variables

### fitstudiocrm-server
```
HANDLER_SUPPORT_URL=http://pi:3200
HANDLER_SUPPORT_SECRET=<HMAC secret>
STORAGE_PATH=./uploads
```

### handler-support
```
PORT=3200
REDIS_HOST=localhost
REDIS_PORT=6379
HMAC_SECRET_FITSTUDIO=<same secret>
FITSTUDIO_API_URL=http://fitstudio:3100
HANDLER_SUPPORT_SECRET=<same secret>
JIRA_API_TOKEN=<token>
JIRA_BASE_URL=https://goodpesyk.atlassian.net
JIRA_PROJECT_KEY=FC
JIRA_ASSIGNEE=levinets@gmail.com
SLACK_SUPPORT_WEBHOOK_URL=<webhook>
```

---

## Roadmap

- ✅ Phase 1 — Backend entities, migration, REST, frontend /support page, handler-support NestJS + Redis
- ✅ Phase 2 — Claude one-shot consumer, prompt, systemd
- ✅ Phase 3 — Jira escalation + Slack alerts
- Phase 4 — Secret rotation, multi-product (Barhandler, Petshandler), pgvector docs indexing, monitoring

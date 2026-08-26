# Support System (Support Tickets)

## Overview

A built-in support ticket system for studio administrators. A ticket is created in the admin panel, enters a queue on the Pi server, where Claude Code analyzes it and automatically answers, asks clarifying questions, or escalates it as a bug/feature request in Jira.

The client (admin) never sees Jira or the Pi server — communication always happens through the **Support** window, which is opened via the button of the same name in the header of the admin app.

---

## Architecture

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
             │ systemd timer (every 10 minutes)
             ▼
┌──────────────────────────────────────────────────────────┐
│ Claude one-shot (process-queue.ts)                       │
│ ─ Pop ticket from Redis (priority order)                 │
│ ─ Fetch details via /support-internal                    │
│ ─ Decision: answer | question | escalate                 │
│ ─ POST comment back via /support-internal                │
│ ─ On escalate → Jira issue + Slack alert                 │
└──────────────────────────────────────────────────────────┘
```

---

## Database

### support_ticket

| Field | Type | Description |
|------|-----|------|
| id | UUID (PK) | |
| subject | VARCHAR | Ticket subject |
| body | TEXT | Problem description |
| priority | ENUM | normal, sos |
| status | ENUM | open, awaiting_user, resolved, closed |
| createdByUserId | UUID | ID of the admin who created it |
| createdAt | TIMESTAMPTZ | |
| updatedAt | TIMESTAMPTZ | |
| lastNotifiedAt | TIMESTAMPTZ | When the Pi server was last notified |

### support_message

| Field | Type | Description |
|------|-----|------|
| id | UUID (PK) | |
| ticketId | UUID (FK) | → support_ticket.id |
| authorKind | ENUM | user, support |
| authorUserId | UUID | Only for user |
| body | TEXT | Message text |
| kind | ENUM | text, answer, question, defect_created |
| jiraKey | VARCHAR | Jira issue key (only for defect_created) |
| createdAt | TIMESTAMPTZ | |

### support_attachment

| Field | Type | Description |
|------|-----|------|
| id | UUID (PK) | |
| messageId | UUID (FK) | → support_message.id |
| filename | VARCHAR | Original file name |
| mimeType | VARCHAR | |
| sizeBytes | INT | |
| storageUrl | VARCHAR | Path on the filesystem |
| createdAt | TIMESTAMPTZ | |

---

## API Endpoints

### Client-facing (Firebase auth, Admin/SuperAdmin)

| Method | Path | Description |
|-------|------|------|
| GET | /support/tickets | List of all studio tickets, no filter by author |
| GET | /support/tickets/:id | Details + messages + attachments |
| POST | /support/tickets | Create a ticket {subject, body, priority} |
| POST | /support/tickets/:id/messages | Add a message + files (up to 5) |
| GET | /support/unread-count | Number of tickets with status awaiting_user |

### Internal Routes (without Firebase login verification)

> ⚠️ Currently these routes are not protected by a signature — this is a known shortcoming, tracked as a separate ticket. A signature is generated only for outgoing requests to the support server.

| Method | Path | Description |
|-------|------|------|
| GET | /support-internal/ticket/:id?appId= | Full ticket for Claude |
| POST | /support-internal/ticket/:id/comment?appId= | Claude posts a reply |
| GET | /support-internal/attachment-data/:id?appId= | Base64 attachment |
| GET | /support-internal/attachment/:id/file?appId= | Raw file (download) |

---

## Limits

- **monthly ticket limit** per studio (unlimited by default). The Super Admin role is not subject to the limit
- **3 consecutive messages** — no more can be sent until support has replied (this does not apply to the Super Admin)
- **5 files** maximum per message

---

## Frontend (fitstudiocrm-app)

**Location:** the **Support** button in the header of the admin app — accessible to Admin/SuperAdmin.

**Components:**
- Ticket list (no status filter)
- Ticket details open in the same window (messenger style: user on the right, Support Bot on the left)
- Creation modal — subject, description, priority
- Reply box — textarea + file attachment

**Poll:** `useSupportStore` polls `GET /support/unread-count` every 10 minutes. If new replies have appeared, a "Support has replied" window appears with a **Got it** button, which only closes it — there is no automatic navigation to the ticket.

---

## handler-support (Pi NestJS)

**Repository:** `goodpesik/handler-support`

**Components:**
- `ticket-event.controller.ts` — receives the webhook, dedup, enqueue
- `redis.service.ts` — priority queues (critical/high/medium/low), in_flight ZSET
- `hmac.middleware.ts` — HMAC-SHA256 verification with anti-replay (±5 min)
- `health.controller.ts` — `/health` + `/health/metrics`

**Consumer:** `scripts/process-queue.ts`
- Pop a ticket from Redis (priority order)
- Move to in_flight (visibility timeout 15 min)
- Fetch details + attachments via the product API
- Build the prompt + run the Claude CLI
- Parse the JSON decision (answer/question/escalate)
- POST the result via `/support-internal`
- On escalate: Jira issue (label `auto:support`) + Slack webhook
- On timeout: Jira issue + Slack + fallback reply to the user

**Systemd:** timer every 10 minutes → oneshot service.

---

## HMAC Scheme

Headers on every request:
```
X-Support-Product:    fitstudio
X-Support-Timestamp:  <unix seconds>
X-Support-Request-Id: <UUID>
X-Support-Signature:  HMAC-SHA256(secret, "METHOD\n/path\n{timestamp}\n{body}")
```

Anti-replay: ±5 minutes from the current time.

---

## Claude Decisions

| Decision | Action | kind |
|---------|-----|------|
| answer | Step-by-step instructions | answer |
| question | Clarifying question | question |
| escalate | Bug/feature → Jira + Slack | defect_created |

All replies are **in Ukrainian only**.

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

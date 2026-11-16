# Support System

## Overview

A built-in support request system for studio administrators. A request is created in the admin panel and passed to the Fitshandler support service (handler-support), which analyses the request and replies in the request: gives an answer, asks a clarifying question or files a defect.

Communication with support takes place in the **Підтримка** (Support) window, opened by the button of the same name in the admin panel header.

---

## The «Підтримка» window

**Access:** the **Підтримка** button in the header — the **Супер Адмін** (Super Admin) and **Адмін** (Admin) roles. The button shows the number of requests with the **Нова відповідь** (New reply) status.

**Request list** — columns **Тема** (Subject), **Статус** (Status), **Пріоритет** (Priority), **Оновлено** (Updated). Buttons **Новий тікет** (New ticket), **Посібник користувача** (User guide, opens this documentation) and **Запланувати консультацію** (Schedule a consultation).

**New request** — fields **Тема \*** («Коротко опишіть проблему», Briefly describe the problem), **Опис \*** (Description; «Детально опишіть проблему...», Describe the problem in detail...), **Пріоритет** (**Звичайний** (Normal) / **SOS**). The **Створити** (Create) button; if the subject or description is empty — «Заповніть тему та опис» (Fill in the subject and description). After creation — «Тікет створено» (Ticket created).

**A request** opens in the same window as a conversation. The type of a support message is marked: **Відповідь** (Answer), **Уточнення** (Clarification), **Дефект** (Defect). The «Ваше повідомлення...» (Your message...) field, the file attachment button and **Надіслати** (Send). The **Закрити тікет** (Close ticket) button closes the request («Тікет закрито», Request closed). The **Назад** (Back) button returns to the list.

A user with the **Супер Адмін** role also sees the «Відповісти як підтримка...» (Reply as support...) field and the **Надіслати як підтримка** (Send as support) button.

**Request statuses:**

| Status | Meaning |
| --- | --- |
| **Відкрито** (Open, `open`) | The request is waiting to be processed by support |
| **Нова відповідь** (New reply, `awaiting_user`) | Support answered or asked a question. When the user opens the request, the status changes to **Відкрито** |
| **Вирішено** (Resolved, `resolved`) | The request is resolved |
| **Закрито** (Closed, `closed`) | The request is closed |

**Updates.** The number of requests with the **Нова відповідь** status is checked every 10 minutes. If it has grown, the «Вам відповіла підтримка» (Support has replied to you) window with the **Зрозуміло** (Got it) button is shown; the window only informs and does not open the request.

---

## Limits

| Limit | Value | Message |
| --- | --- | --- |
| Requests per month per studio | No limit | «Місячний ліміт тікетів вичерпано. Створити новий тікет можна буде наступного місяця.» (The monthly ticket limit is used up. A new ticket can be created next month.) (`TICKET_MONTHLY_LIMIT`) |
| SOS requests per month per studio | No limit | «Місячний ліміт SOS-звернень вичерпано. Оберіть звичайний пріоритет або зачекайте до наступного місяця.» (The monthly SOS limit is used up. Choose the normal priority or wait until next month.) (`SOS_MONTHLY_LIMIT`) |
| User messages in a row without a support reply | 3 | «Ви надіслали 3 повідомлення підряд. Дочекайтеся відповіді підтримки, щоб продовжити.» (You have sent 3 messages in a row. Wait for the support reply to continue.) (`COMMENT_CONSECUTIVE_LIMIT`) |
| Files per message | 5 (images or PDF) | — |
| File size | 5 MB | — |

Monthly limits are counted from the first day of the calendar month (UTC). Monthly limits and the messages-in-a-row restriction do not apply to the **Супер Адмін** role.

---

## Request processing

- When a request is created and on each new user message, the studio server sends an event to the support service. Sending the same request again does not create a duplicate.
- Requests with the **SOS** priority are processed every minute and first; normal ones — every 10 minutes.
- Support service decisions:

| Decision | Action | Message type (`kind`) |
| --- | --- | --- |
| `answer` | An answer with instructions | `answer` |
| `question` | A clarifying question | `question` |
| `escalate` | A defect is filed | `defect_created` |

Replies are given in the language of the request: Cyrillic text — in Ukrainian, otherwise — in English.

---

## Technical specification

### Database

#### support_ticket

| Field | Type | Description |
|------|-----|------|
| id | UUID (PK) | |
| subject | VARCHAR | Request subject |
| body | TEXT | Problem description |
| priority | ENUM | `normal`, `sos` |
| status | ENUM | `open`, `awaiting_user`, `resolved`, `closed` |
| createdByUserId | UUID | User who created the request |
| createdAt | TIMESTAMPTZ | |
| updatedAt | TIMESTAMPTZ | |
| lastNotifiedAt | TIMESTAMPTZ | Time the support service was last notified |

#### support_message

| Field | Type | Description |
|------|-----|------|
| id | UUID (PK) | |
| ticketId | UUID (FK) | → support_ticket.id |
| authorKind | ENUM | `user`, `support` |
| authorUserId | UUID | Only for `user` |
| body | TEXT | Message text |
| kind | ENUM | `text`, `answer`, `question`, `defect_created` |
| jiraKey | VARCHAR | Defect key (only for `defect_created`) |
| createdAt | TIMESTAMPTZ | |

#### support_attachment

| Field | Type | Description |
|------|-----|------|
| id | UUID (PK) | |
| messageId | UUID (FK) | → support_message.id |
| filename | VARCHAR | Original file name |
| mimeType | VARCHAR | |
| sizeBytes | INT | |
| storageUrl | VARCHAR | File path |
| createdAt | TIMESTAMPTZ | |

### Studio server API

**Admin panel routes** (user sign-in required):

| Method | Path | Description |
|-------|------|------|
| GET | /support/tickets | Studio requests |
| GET | /support/tickets/:id | Request with messages and attachments |
| GET | /support/unread-count | Number of requests with the `awaiting_user` status |
| GET | /support/limits | Monthly limits and remaining balance |
| POST | /support/tickets | Create a request `{subject, body, priority}` |
| POST | /support/tickets/:id/messages | Add a message and files (up to 5) |
| POST | /support/tickets/:id/reply-as-support | Reply on behalf of support |
| PATCH | /support/tickets/:id/status | Change the request status |

**Internal routes** (for the support service; an HMAC signature is required):

| Method | Path | Description |
|-------|------|------|
| GET | /support-internal/ticket/:id?appId= | Full request |
| POST | /support-internal/ticket/:id/comment?appId= | Support message in the request |
| GET | /support-internal/attachment-data/:id?appId= | Attachment in Base64 |
| GET | /support-internal/attachment/:id/file?appId= | Attachment file |
| GET | /support-internal/investigate/* | Reading studio data to analyse the request |
| POST | /support-internal/actions/client-plans/close | Closing a client membership |

### HMAC signature

Headers of every request between the studio server and the support service:

```
X-Support-Product:    fitstudio
X-Support-Timestamp:  <unix time in seconds or milliseconds>
X-Support-Request-Id: <UUID>
X-Support-Signature:  HMAC-SHA256(secret, "METHOD\n/path?query\n{timestamp}\n{body}")
```

- The full path including query parameters and the unchanged request body are signed.
- The request is rejected (`401`) if the signature or time is missing, the signature does not match, or the time differs from the current time by more than 5 minutes.

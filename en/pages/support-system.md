# Support System

## Overview

A built-in support request system for studio administrators. A request is created in the admin panel and passed to the Fitshandler support service (handler-support), which analyses the request and replies in the request: gives an answer, asks a clarifying question or files a defect.

Communication with support takes place in the **Підтримка** (Support) window, opened by the button of the same name in the admin panel header.

---

## The «Підтримка» window

**Access:** the **Підтримка** button in the header — the **Супер Адмін** (Super Admin) and **Адмін** (Admin) roles. The button shows the number of requests with the **Нова відповідь** (New reply) status.

**Request list** — columns **Тема** (Subject), **Статус** (Status), **Пріоритет** (Priority), **Оновлено** (Updated). Buttons **Новий тікет** (New ticket), **Посібник користувача** (User guide, opens this documentation) and **Запланувати консультацію** (Schedule a consultation).

**New request** — fields **Тема \*** («Коротко опишіть проблему», Briefly describe the problem), **Опис \*** (Description; «Детально опишіть проблему...», Describe the problem in detail...), **Пріоритет** (**Звичайний** (Normal) / **SOS**), the **Додати файли** (Add files) and **Записати голосове** (Record a voice message) buttons. The subject is required. The request is described in text in the **Опис** field or by a voice message; either one is enough. An image or a PDF without text or a voice message does not replace the description. The **Створити** (Create) button; if the subject is missing or the request is not described — «Вкажіть тему та опишіть запит текстом або голосовим повідомленням» (Enter the subject and describe the request in text or by a voice message). After creation — «Тікет створено» (Ticket created).

**A request** opens in the same window as a conversation. The type of a support message is marked: **Відповідь** (Answer), **Уточнення** (Clarification), **Дефект** (Defect). The «Ваше повідомлення...» (Your message...) field, the file attachment button, the voice recording button (microphone) and **Надіслати** (Send). A message is sent when it holds text, a file or a voice message. The **Закрити тікет** (Close ticket) button closes the request («Тікет закрито», Request closed). The **Назад** (Back) button returns to the list.

The «Відповісти як підтримка...» (Reply as support...) field and the **Надіслати як підтримка** (Send as support) button are shown only to the **Супер Адмін** role and only for a ticket that is not closed. The reply is recorded as a support message. Only the **Супер Адмін** role can reply on behalf of support; a request from any other role is rejected with code 403. The server does not check the ticket status for this request.

**Request statuses:**

| Status | Meaning |
| --- | --- |
| **Відкрито** (Open, `open`) | The request is waiting to be processed by support |
| **Нова відповідь** (New reply, `awaiting_user`) | Support answered or asked a question. When the user opens the request, the status changes to **Відкрито** |
| **Вирішено** (Resolved, `resolved`) | The request is resolved |
| **Закрито** (Closed, `closed`) | The request is closed |

**Updates.** The number of requests with the **Нова відповідь** status is checked every 10 minutes. If it has grown, the «Вам відповіла підтримка» (Support has replied to you) window with the **Зрозуміло** (Got it) button is shown; the window only informs and does not open the request.

### Voice messages

A voice message is recorded in a new ticket (the **Записати голосове** button) and in a reply in an open request (the microphone button next to the file attachment button).

| Stage | What is shown |
| --- | --- |
| Recording | «Іде запис» (Recording), a timer in the `m:ss / 3:00` format and the **Зупинити** (Stop) button. The recording stops automatically after 3 minutes |
| After stopping | A player to listen to the recording, the **Скасувати** (Cancel) and **Надіслати** (Send) buttons |
| **Скасувати** | The recording is deleted, nothing is added to the request |
| **Надіслати** | The recording is added to the files of the request or reply and sent with them. For a new ticket the same requirements apply as for the **Створити** button |
| A sent voice message | Shown in the conversation as a player |

- The browser asks for microphone access to record.
- A voice message is a file of the request: the file count and size limits apply to it (see [Limits](#limits)).
- While recording and until the recording is sent or cancelled, the record button is unavailable.
- Closing the window, returning to the list or opening another request deletes an unfinished recording.

| Situation | Message |
| --- | --- |
| The browser does not support recording | «Ваш браузер не підтримує запис голосу. Опишіть, будь ласка, запит текстом.» (Your browser does not support voice recording. Please describe the request in text.) |
| Microphone access is denied | «Доступ до мікрофона заборонено. Дозвольте доступ у налаштуваннях браузера або опишіть запит текстом.» (Microphone access is denied. Allow access in the browser settings or describe the request in text.) |
| The recording could not start | «Не вдалося розпочати запис. Спробуйте ще раз або опишіть запит текстом.» (The recording could not start. Try again or describe the request in text.) |
| The recording was interrupted or is empty | «Запис перервано. Спробуйте ще раз або опишіть запит текстом.» (The recording was interrupted. Try again or describe the request in text.) Such a recording is not sent |

The rest of the **Підтримка** window keeps working during recording and after a refusal.

---

## Limits

| Limit | Value | Message |
| --- | --- | --- |
| Requests per month per studio | No limit | «Місячний ліміт тікетів вичерпано. Створити новий тікет можна буде наступного місяця.» (The monthly ticket limit is used up. A new ticket can be created next month.) (`TICKET_MONTHLY_LIMIT`) |
| SOS requests per month per studio | No limit | «Місячний ліміт SOS-звернень вичерпано. Оберіть звичайний пріоритет або зачекайте до наступного місяця.» (The monthly SOS limit is used up. Choose the normal priority or wait until next month.) (`SOS_MONTHLY_LIMIT`) |
| User messages in a row without a support reply | 3 | «Ви надіслали 3 повідомлення підряд. Дочекайтеся відповіді підтримки, щоб продовжити.» (You have sent 3 messages in a row. Wait for the support reply to continue.) (`COMMENT_CONSECUTIVE_LIMIT`) |
| Files per request or reply | 10 (images except SVG, PDF, voice messages) | «До одного звернення можна додати не більше 10 файлів.» (No more than 10 files can be added to one request.) |
| File size | 5 MB | «Не додано N файл(ів): більші за 5 МБ.» (N file(s) not added: larger than 5 MB.) |
| Total size of the files of a request or reply | 20 MB | «Загальний розмір файлів одного звернення — не більше 20 МБ.» (The total size of the files of one request is no more than 20 MB.) |
| Voice message duration | 3 minutes | The recording stops automatically |

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
| POST | /support/tickets/:id/messages | Add a message and files (up to 10) |
| POST | /support/tickets/:id/reply-as-support | Reply on behalf of support `{body}`. Only the Супер Адмін role; any other role gets 403 |
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

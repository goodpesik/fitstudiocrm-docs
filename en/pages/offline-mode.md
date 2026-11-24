# Offline mode

Offline mode lets a till computer with Device Handler installed work without internet and while the Fitshandler server is unavailable. Operations made without a connection are sent to the server once the connection is back.

## Overview

### What works without internet

- The offline till works by the same rules in the «No internet» and «Server unavailable» states (see [Connection states](#connection-states)).
- Without a connection to the server the following are available: opening and closing an offline shift; selling plans, products, single classes and certificates; paying in parts and «оплатити пізніше» (pay later); debt payment; payment from the personal account; certificate redemption; refunds; bank transfer payment; class registration; client creation; the self check-in QR; reports for the offline period (see [Available actions](#available-actions)).
- Payment methods: cash, card without a terminal, personal account, bank transfer.
- Each action becomes one queue operation and is sent to the server once the connection is back. An operation shown as saved stays saved after a power cut of the computer.

### What is not available offline

- The **Тренування** (Workouts), **Тренери** (Coaches), **Зали** (Rooms) and **Налаштування** (Settings) sections, the **Підтримка** (Support) and **Сповіщення** (Notifications) buttons.
- Personal account top-up and correction, bonuses, confirmation of a bank transfer payment, editing and deleting transactions, payment and refund through a terminal, Monobank acquiring, refund of a personal account top-up (see [Operations not accepted offline](#operations-not-accepted-offline)).
- The waiting list, recurring bookings, moving and cancelling classes, creating and editing workouts, editing, deleting, importing and exporting clients (see [Class and client actions not available offline](#class-and-client-actions-not-available-offline)).
- Issuing fiscal receipts and the **Не фіскалізовано** (Not fiscalized) tab (see [Fiscalization after the sync](#fiscalization-after-the-sync)).
- An action not available in the offline till shows the message «Ця дія недоступна в офлайн-режимі.»

### Till refusals on till data

The till checks an action against its own data, refuses with an explanation and does not queue the operation, in particular:

- a payment without an open offline shift;
- a payment from the personal account above the balance, a product sale above the stock;
- a registration by a plan that is used up, frozen, expired, not active or not valid for the class; a registration for a class with no free seats or a cancelled class;
- redemption of a certificate that is not in the till data, is already redeemed or has expired;
- a refund above the available sum, a refund of a sale paid through a terminal and a refund of a personal account top-up;
- a debt payment above the remaining debt and a payment of a debt created without internet;
- creating a client with a phone or card number that is already in the till data.

The full list of codes and messages is in [Till refusal codes](#till-refusal-codes).

### Enabling offline mode

1. Device Handler is installed and running on the till computer; the offline till starts with it (see [Installation and start](#installation-and-start)).
2. A user with the **Супер Адмін** (Super Admin) or **Адмін** (Admin) role, in the browser of this computer, opens the **Налаштування** (Settings) section, the **Офлайн-режим** (Offline mode) tab, the **Цей компʼютер** (This computer) block, sets **Номер каси** (Till number) and presses **Увімкнути офлайн-режим** (Enable offline mode) (see [Enabling on a computer](#enabling-on-a-computer)).
3. The offline till receives the full data package and then updates the data while connected (see [Data updates](#data-updates)).

### Going to the offline till and back online

1. When the server does not answer, the online admin shows the «Сервер FitStudioCRM недоступний» window; the **Перейти в офлайн-касу** button opens the offline till in a new tab (see [Server unavailable mode](#server-unavailable-mode)). The offline till is also opened by the **Відкрити офлайн-касу** button and by the link in the error window.
2. Payments are taken after the offline shift is opened (see [Offline shift](#offline-shift)).
3. The offline banner shows the connection state, the data time and the number of unsynced operations (see [Offline banner](#offline-banner)).
4. Once the connection is back, the queue is sent to the server with no user action, and the offline till shows the «Звʼязок із сервером відновлено» window. The **Перейти в онлайн-адмінку** button opens the closing of the offline shift when it is open, and after closing — the online admin (see [Back to the online admin](#back-to-the-online-admin)).
5. The online admin reminds about an open offline shift until it is closed (see [Reminder about an open offline shift](#reminder-about-an-open-offline-shift)).

### Sales and fiscalization after the sync

- Queue operations are sent to the server one by one in the order they were made. Each operation is applied at most once, including after a connection break in the middle of sending and a repeated sending (see [One-time application of operations](#one-time-application-of-operations)).
- An operation the server did not accept for the moment stays in the queue in the «Очікує синхронізації» (Waiting for sync) state; the next queue operations wait for it.
- Transactions, stock movements, personal account history and certificates are saved with the operation time at the till; sales and debt payments go into a shift by the rules of [Shift](#shift).
- An operation that contradicts changes made while there was no connection is not applied and is shown on the **Потребує уваги** (Needs attention) tab (see [Operation sync codes](#operation-sync-codes)).
- The offline till creates no fiscal receipts: the buyer gets a non-fiscal document with a number. Fiscal receipts for sales and refunds of the offline period are created after the sync on the [Каса → Не фіскалізовано](/en/menu/pos#_397-not-fiscalized) tab when the studio has an active fiscal integration (see [Fiscalization after the sync](#fiscalization-after-the-sync)).

### Data available offline

- Studio plans, categories, products with stock, coaches, rooms, workouts; clients with the personal account balance and plans; unpaid debts; active certificates; sales and closed shifts for the last 3 days; the schedule from 3 days before the current day to 7 days after it; self check-in codes for 48 hours; studio settings (see [Contents](#contents)).
- Data is updated regularly and only while connected; the till receives the full data package periodically. Data not updated for more than 24 hours is marked as stale (see [Stale data](#stale-data)).
- Keys, tokens, cashier PIN codes and secrets are not passed to the till computer.

### Limits of work without a connection

| Limit | Value |
|---|---|
| Age of an operation at the sync | not more than 30 days; the server refuses an older operation with the `OCCURRED_TOO_LONG_AGO` code |
| Till computer clock | not more than 5 minutes ahead of the server time; otherwise the operation is refused with the `OCCURRED_IN_FUTURE` code |
| Stale data | more than 24 hours without an update |
| Self check-in QR | not longer than 48 hours after the last data update |
| Online admin operations with an unknown result | passed to the offline till when they are not older than 24 hours |

### Operations that need attention

- Offline till operations the server did not apply, or applied with a mark, are shown in the online admin on the [Каса → Потребує уваги](/en/menu/pos#_398-needs-attention) tab with the reason (see [Needs attention](#needs-attention) and [Operation sync codes](#operation-sync-codes)).
- For each operation not applied the admins get one notification.
- An admin resolves the operation with the tab's actions or marks it **Переглянуто** (Reviewed).
- Operations refused by the check of the operation kind, version and time are shown on the tab as refused, with the reason. Only operations with an invalid id and operations whose id belongs to another operation are not shown (see [Operation check refusals](#operation-check-refusals)).

### Related pages

- [Каса](/en/menu/pos) (POS) — the **Не фіскалізовано** and **Потребує уваги** tabs, fiscalizing a transaction.
- [Розклад](/en/menu/schedule) (Schedule) — classes and client booking.
- [Клієнти](/en/menu/clients) (Clients) — client card, personal account, debts.
- [Зміна та сповіщення](/en/pages/shifts) (Shift and notifications) — opening and closing a shift, admin notifications.
- [ПРРО offline-mode registers](/en/pages/prro-registers) — the registers a computer signs fiscal receipts with while there is no internet.

## Installation and start

### Requirements

- The offline till runs on a till computer with Device Handler installed. Device Handler starts the offline till and stops it together with itself; no separate installation is needed.
- Offline mode must be enabled on the computer (see [Devices and access](#devices-and-access)).
- The offline till is available only on the computer it runs on; other computers of the network cannot reach it.

### Offline till address

| Parameter | Value |
|---|---|
| Address | `http://127.0.0.1:9899` |
| Time zone of dates and times | the studio's time zone, regardless of the computer's time zone |

- The offline till shows the studio data received during the last connection, including when there is no internet.
- An action or section unavailable in the offline till shows the message «Ця дія недоступна в офлайн-режимі.» (code `OFFLINE_NOT_AVAILABLE`).

### Data updates

| Event | What the till receives |
|---|---|
| First start after offline mode is enabled | the full data package |
| Regularly while connected | a data update; periodically the full data package |
| Connection restored | the operation queue is sent to the server, then the till receives data |

- Data is updated only while the server can be reached.
- Operations made without a connection are sent to the server after the connection is restored, without user action, one by one in the order they were made. An operation the server did not accept for a temporary reason is sent again; the next operations of the queue wait for it.
- While the queue holds operations not yet sent to the server, received data is not applied; it is applied after the queue is sent.
- Each queued operation has a state: `queued` — waiting to be sent, `applied` — applied on the server, `rejected` — refused, `conflict` — needs an administrator's decision.
- An operation shown as saved is kept after the computer loses power.

### Stale data

- Data not updated for more than 24 hours is stale. The offline till reports it on the offline mode banner.

### Sync stop

| Server response | What happens |
|---|---|
| The computer's access is not valid or was issued to another computer | the sync stops until offline mode is enabled on the computer again (see [Devices and access](#devices-and-access)) |
| The server does not accept the queue from this offline till version | the sync stops until the offline till is updated; the operations stay in the queue with the `queued` state |

- After a stop, the offline till sends no further request to the server automatically; a request from the «Синхронізувати» (Sync) button is refused.
- After offline mode is enabled again or the offline till is updated, the queue is sent to the server under the general rules.

### Connection states

| State | Meaning |
|---|---|
| Online | the Fitshandler server answers |
| No internet | the server does not answer, and a public internet address does not answer either |
| Server unavailable | the internet is available, the Fitshandler server does not answer |

- The till checks the server regularly. A failed check: the server did not answer or reported it is temporarily unavailable.
- The «No internet» or «Server unavailable» state is set after several failed checks in a row; the «Online» state returns after several successful checks in a row.

- A server refusal that explains its reason is not a failed check.
- One failed check does not change the state.
- A separate check of a public internet address tells «No internet» from «Server unavailable».
- In the «No internet» and «Server unavailable» states the offline till works by the same rules.

## Devices and access

### Enabling on a computer

- Offline mode is enabled separately for each till computer.
- A user with the **Super Admin** or **Admin** role, signed in on that computer, can enable offline mode. A user with the **Manager** role is refused.
- On enabling, the computer receives a device access — a separate key bound to the studio, the user and the computer.
- The key is passed to the computer once. The server stores only its hash; the key cannot be restored from the server data.
- One user on one computer has one valid device access. Enabling again issues a new access; the previous one stops working.
- A device access opens only the data exchange of the offline till with the server: sending offline operations and receiving the till data. Other sections of the system are not available with a device access.
- Enabling is done in **Settings** on the **Offline mode** tab, in the **This computer** block, in the browser of the till computer with the Device Handler switched on.
- The **This computer** block shows the state of offline mode on the computer:

| State | Text |
|---|---|
| The Device Handler does not answer | Device Handler на цьому компʼютері не відповідає. Увімкніть його в розділі «Інтеграції». |
| A Device Handler version without offline mode | Ця версія Device Handler не підтримує офлайн-режим FitStudioCRM. Оновіть Device Handler. |
| Enabled for another studio | На цьому компʼютері офлайн-режим увімкнено для іншої студії. |
| Disabled | Офлайн-режим на цьому компʼютері вимкнено. |
| Enabled, the offline till is not running | Офлайн-режим увімкнено, але офлайн-каса не запущена. Перевірте Device Handler. |
| Enabled | Офлайн-режим на цьому компʼютері увімкнено. |

- The **Номер каси** (till number) field takes a whole number from 1 to 99 (1 by default). The till number is part of the offline till's document number (see [Document number](#document-number)).
- The **Увімкнути офлайн-режим** button (for a disabled computer) or **Оновити доступ** (for an enabled one) issues a device access to the computer and passes it to the Device Handler with the till number. After a successful enabling the message «Офлайн-режим на цьому компʼютері увімкнено» is shown. A Device Handler refusal is shown as a message with the reason.
- The **Відкрити офлайн-касу** button opens the offline till in a new tab. The button is shown when offline mode is enabled for this studio and the offline till is running.
- The Device Handler and printer settings of the computer are passed to the offline till after enabling and after every change; the offline till applies them when it starts.

### Access validity

- A device access is valid for 7 days from the computer's last contact with the server, not from the day it was enabled.
- Every request of the computer to the server extends the validity by 7 days from that request. A computer that contacts the server daily does not lose access.
- A computer that has not contacted the server for more than 7 days loses access. Offline mode on it must be enabled again while it is online.
- The access stops working if the user it was issued to no longer has a role with access to the system.

| Parameter | Value |
|---|---|
| Access validity | 7 days from the last contact |
| Valid accesses per user and computer | 1 |

### Device list and revoking

- The device list is placed in **Settings** ("Налаштування") on the **Offline mode** ("Офлайн-режим") tab. The tab is visible only to users with the **Super Admin** or **Admin** role; a user with the **Manager** role does not see it.
- The list contains valid device accesses in the columns: **Device name** ("Назва пристрою"), **User** ("Користувач"), **Last contact** ("Останній звʼязок"), **Enabled on** ("Дата увімкнення": date and time offline mode was enabled on the computer), **Access valid until** ("Доступ діє до": date and time the access expires).
- Dates and times in the **Last contact**, **Enabled on** and **Access valid until** columns are shown in the studio time zone, regardless of the time zone of the computer the list is opened on.
- If the computer has not contacted the server since offline mode was enabled, the **Last contact** ("Останній звʼязок") column shows "Ще не виходив на звʼязок" (has not contacted the server yet).
- If there are no valid accesses, the list shows "Немає пристроїв з увімкненим офлайн-режимом" (no devices with offline mode enabled).
- The **Revoke** ("Відкликати") button opens a confirmation dialog. After confirmation the device access stops at once, the message "Доступ пристрою відкликано" (device access revoked) is shown and the list is refreshed. If the server did not revoke the access, the revocation message is not shown and the list is refreshed. The next request of the computer with this access is refused; offline mode on it must be enabled again.
- The **Cancel** ("Відміна") button in the confirmation dialog closes it without changes.
- A revoked access and an expired access are not shown in the list.
- If the list cannot be loaded, the list is empty.

- A request with an access that is revoked, expired, or whose user has no role with access is refused; the sync stops (see [Sync stop](#sync-stop)).
- A request with a device access to a section that access does not open is refused.
- A request with data of another computer than the one the access was issued to is refused with the code `DEVICE_MISMATCH`.

## Device Handler

### The "Офлайн режим" (Offline mode) item

- The **Офлайн режим** (Offline mode) button on the Device Handler page (`http://localhost:9999`) is shown when the installed Device Handler version contains the offline till and FitStudioCRM offers offline mode, or offline mode is already enabled on this computer.
- When offline tills of several products (FitStudioCRM and Petshandler) are available on the computer, the **Офлайн режим** window shows the **Продукт** (Product) field to choose the till. Tills of different products run at the same time and independently of each other.

| Window row | Value |
|---|---|
| **Статус** (Status) | `вимкнено` (off); `увімкнено, сервіс працює` (on, the service is running); `увімкнено, сервіс не працює` (on, the service is not running) with the reason; `потрібне повторне увімкнення у FitStudioCRM` (needs to be switched on again in FitStudioCRM) — the device access is not valid (see [Sync stop](#sync-stop)); `черга зупинена: потрібне оновлення Девайс менеджера` (the queue is stopped: the Device Handler needs an update) — the server does not accept the queue from this offline till version |
| **Заклад** (Shop) | the studio name |
| **Дані станом на** (Data as of) | date and time of the till data |
| **Не синхронізовано операцій** (Operations not synchronised) | the number of operations in the `queued` state |
| **Номер каси** (Till number) | the till number among the studio computers (see [Several tills](#several-tills)) |

- The **Заклад**, **Дані станом на**, **Не синхронізовано операцій** and **Номер каси** rows are shown only while offline mode is enabled. While it is off, a hint is shown: "Увімкнення офлайн-режиму: FitStudioCRM → Налаштування → вкладка «Офлайн-режим» → «Увімкнути офлайн-режим»." (To switch offline mode on: FitStudioCRM → Settings → the «Offline mode» tab → «Enable offline mode».)

### Buttons

| Button | When shown | Action |
|---|---|---|
| **Відкрити офлайн-касу** (Open the offline till) | offline mode is enabled, the offline till is running | opens the offline till (`http://127.0.0.1:9899`) in a new browser tab |
| **Синхронізувати** (Synchronise) | offline mode is enabled, the offline till is running | sends the operation queue to the server and updates the till data without waiting for the scheduled update |
| **Вимкнути** (Switch off) | offline mode is enabled | switches offline mode off on the computer after confirmation |
| **Закрити** (Close) | always | closes the window |

- After the sync the message "Синхронізацію виконано. Не синхронізовано операцій: N" (Synchronisation done. Operations not synchronised: N) is shown. When the operations were not sent, the message "Синхронізація не вдалася. Операції залишаються в черзі й будуть надіслані автоматично після відновлення звʼязку." (Synchronisation failed. The operations stay in the queue and will be sent automatically once the connection is back.) is shown.
- Switching off removes the studio's local data from the computer, including the fiscal documents of the ПРРО registers. Switching off is not performed while the queue holds operations not sent to the server; the message "Офлайн-операцій, що ще не надійшли на сервер: N. Вимкнення можливе після синхронізації." (Offline operations not yet received by the server: N. Switching off is possible after the sync.) is shown.
- Switching off is not performed while a ПРРО register has an open offline session or documents not handed over to the tax service (see [Switching offline mode off with documents not handed over](/en/pages/prro-registers#switching-offline-mode-off-with-documents-not-handed-over)).
- A Device Handler update is not performed while the offline till queue holds operations not sent to the server; Device Handler reports: "офлайн-операції FitStudioCRM ще не надійшли на сервер: N" (FitStudioCRM offline operations have not reached the server yet: N).

### Several tills

- Offline mode is enabled separately on each till computer of the studio. Each computer has its own device access, its own offline shift and its own document numbering.
- The till number is set when offline mode is enabled on the computer. The till number is part of the document number (see [Document number](#document-number)). Computers of one studio must be given different till numbers.

| Parameter | Value |
|---|---|
| Till number | a whole number from 1 to 99 |
| Till number when not set | 1 |
| Offline tills of one product per computer | 1 |

- Enabling offline mode again on a computer with another till number changes the number for the following documents; the studio's local data is kept.
- Enabling offline mode for another studio on a computer where offline mode is already enabled is not performed; the message "Офлайн-режим уже увімкнено для іншого закладу. Спершу вимкніть його там." (Offline mode is already enabled for another shop. Switch it off there first.) is shown.

## Data available without internet

The offline till works with the data received from the server at the last connection. The offline banner shows when the data was received: "Data as of …".

### Contents

| Data | What is sent |
|---|---|
| Plans | every plan of the studio with its price, number of sessions and duration |
| Categories | every workout category |
| Products | name, price, stock |
| Coaches | name, colour, categories; phone and birthday are not sent |
| Rooms | name, capacity |
| Workouts | recurring workout templates in effect within the schedule window, and one-time workouts of the schedule window |
| Clients | first name, last name, type, card number, vacations (freezes), phone (`phone`), personal account balance and time of the last personal account operation; email and birthday are not sent |
| Client plans | active, not yet activated and frozen plans, including plans shared across a studio network, with sessions left, sessions at the start of the plan (`initialWorkouts`) and validity; ended plans are not sent |
| Debts | unpaid debts with total amount (`totalAmount`), amount left to pay (`remainingAmount`), contents and clients; the amount left to pay equals the one on the client's debt screen |
| Certificates | active certificates within their validity only: number, description, price, plans of the certificate, validity, client, status |
| Sales | sales and personal account top-ups from the start of the day 3 days back in the studio time zone, except sales of the current online shift: lines, amount, payment method, paid from the personal account flag, top-up flag, invoice payment confirmation flag, paid through a terminal flag, refunds made, fiscalization state, fiscal card id |
| Shifts | closed shifts from the start of the day 3 days back in the studio time zone; the current online shift is not sent |
| Schedule | workouts from 3 days before today to 7 days after it, with booked clients and the number of taken seats; recurring workouts on dates with no workout created yet, from today on, with their regular clients |
| Self check-in codes | ready QR links for every hour of the next 48 hours: for all rooms, for each room alone and for the room sets the till asks for; only when self check-in is on |
| Settings | studio name and time zone, shift and booking parameters, self check-in parameters, printers, studio receipt header (`receiptHeader`); fiscal cards — id, name, type, active flag and receipt header (`receiptHeader`); acquiring cards — id, name, type and active flag only |

- Keys, tokens, cashier PIN codes, licence keys and the self check-in signing secret are not sent to the till computer.
- A self check-in code from the till's data is the code the server accepts in that hour. The server accepts the previous hour's code for 10 more minutes after the hour changes.

### Client phone and search by phone

| Field | Type | Presence | Format |
|---|---|---|---|
| `clients[].phone` | string \| null | always | `0XXXXXXXXX` (0 and 9 digits) — the form the server stores and compares with in the online search by phone |

- `+380…` and `380…` numbers are given as `0…`; spaces, dashes and brackets are removed.
- A client without a usable phone number: `phone` is `null`.
- The offline client search by phone must bring the entered number to the same form before comparing; the search result matches the online client search by the same number.

### Receipt header

| Field | Type | Value |
|---|---|---|
| `catalog.settings.receiptHeader` | string \| null | the [studio receipt header](/en/login/settings#receipt-header) without leading and trailing spaces; `null` when no text is set |
| `catalog.settings.fiscal[].receiptHeader` | string \| null | the effective receipt header of the card: the [card's](/en/login/settings#fiscal-integrations) text without leading and trailing spaces when set, otherwise the studio text without leading and trailing spaces; `null` when neither is set |

- An empty value or a value of spaces only is the same as no value.
- No length limit.

Printing rules for the offline till:

- A receipt with a fiscal card must print that card's `receiptHeader` from `catalog.settings.fiscal[]`.
- A receipt without a fiscal card must print `catalog.settings.receiptHeader`.
- The text is printed at the top of the receipt; line breaks must be kept.
- A `null` value — no receipt header is printed.
- The receipt header is not printed on online receipts of the fiscal provider (Checkbox, VchasnoKasa).

### Full package and updates

- The full package contains all the data in the table.
- An update contains all the data except plans, categories, products (name and price), coaches, rooms, workouts and settings. Product stock is sent in an update as a separate list.
- Every list of an update is complete: the till replaces its list with the one received. A record missing from an update list (a redeemed or expired certificate, a paid or deleted debt, an ended plan) is removed by the till.
- A product sale, a personal account payment, a certificate redemption and a refund made online or in the app appear in the offline till after the next update.

### Self check-in codes in the till data

- If self check-in is off, no self check-in codes are passed to the till data.
- If self check-in is on but the codes could not be made (in particular, the studio has no saved public code or code signing secret yet; the first opening of the online self check-in QR creates them), no codes are passed; the rest of the data is passed.

## One-time application of operations

- Every till action receives an operation id at the moment of the click. The id does not change when the action is sent again.
- An action the till received no server response to (connection drop, server unavailable) is sent again with the same id — online or during the sync of the offline queue. The server applies an operation at most once: sending it again returns the stored result; no second sale, payment or booking is created.
- The stored result is returned in the form the first server response had it (JSON): dates as ISO 8601 strings, money amounts in the same format as in the first response.
- The same id with another operation content is refused.
- An online sale or refund stopped after a step that cannot be undone (a cash ledger row, a fiscal receipt) is not run again. Such an operation gets the `conflict` result with the `OPERATION_INTERRUPTED` code and needs an admin's review. This also applies to an online sale or refund whose delivery stopped before it finished.
- An online debt payment saves all its records together or none of them, and creates the fiscal receipt after they are saved. Stopped before the save, it leaves no changes and is run by the next delivery with the same id.
- A sale, a debt payment, a refund, a certificate sale and a certificate redemption applied by the offline queue sync save all their records together or none of them. Such an operation, stopped before it finished, leaves no changes and is run by the next delivery with the same id.
- An operation stopped before the first such step leaves no changes; sending it again with the same id runs it.
- An operation of a version above the one the server supports is not applied and changes no data. The operation stays in the computer's queue and is applied after the server is updated.
- An action without an operation id runs as an ordinary online action.

These till actions accept an operation id:

| Action | Operation kind |
|---|---|
| Sale, including payment from the personal account | `sale` |
| Sale refund | `refund` |
| Debt payment, including from the personal account | `debt_payment` |
| Booking a client for a class | `booking` |
| Creating a client | `client_create` |
| Certificate sale | `certificate_sale` |
| Certificate redemption | `certificate_redeem` |

### Class booking with an operation id

A class booking sent with an operation id is saved once: sending it again with the same id returns the saved result and creates no second booking.

- If the journal row cannot be stored, the client is not booked and the "Вас записано на тренування!" notification is not sent.
- A repeated delivery of the same operation (same id and same content) returns the stored result; the client is not booked again.
- If a delivery stops before the booking is stored, the next delivery with the same id performs the booking again; such an operation does not get the `conflict` result ("Потребує уваги").
- The class change log entry ("+ client name") and the client history entry are written after the booking is stored; a failure of these entries does not undo the booking.
- The booking notification to the client is sent only after the booking is stored.
- Every database write that belongs to the booking is stored in the same transaction: the repeat carried onto the other dates of the workout and, for a no-show on a personal workout, the client debt and the coach salary entry. If the journal row cannot be stored, none of these writes is stored.
- A failure of the no-show debt charge does not undo the booking; in that case there is no debt and no coach salary entry.
- A failure to carry the repeat onto one of the other dates does not undo the booking: only the carry onto that date is not stored; the carry onto the remaining dates is stored.
- The "Звільнилося місце на тренуванні!" notice to the administrator and the class change log entries for the carried dates are written after the booking is stored.
- If the class is deleted before the booking is stored, the operation is not stored in the journal: the next delivery with the same id is performed again.

### Operation format

| Parameter | Value |
|---|---|
| Operation id | UUID |
| Operation fields | `id` (UUID), `kind`, `version`, `occurredAt` (ISO 8601), `payload`, `dependsOn` (UUIDs of earlier queue operations, optional) |
| Operation time | not earlier than 30 days and not later than 5 minutes from the server time |

The refusal codes of online actions and queue operations are in [Refusals of online actions with an operation id](#refusals-of-online-actions-with-an-operation-id), [Operation check refusals](#operation-check-refusals) and [Operations waiting in the queue](#operations-waiting-in-the-queue).

During sync every operation gets its own result:

| Result | Meaning |
|---|---|
| `applied` | the operation is applied (or was applied earlier; the stored result is returned) |
| `rejected` | the operation is refused; sending it again returns the same |
| `conflict` | the operation contradicts changes made meanwhile, or it stopped after a step that cannot be undone; an admin decision is needed |
| `retry` | the operation is not applied now; send it later, the next operations of the queue wait |
| `in_progress` | another delivery is applying the operation |
| `pending` | the operation was not looked at: an earlier operation of the queue is not applied yet |

The `rejected` and `conflict` results carry the `error` field: `code` (the reason code), `message` (the description) and, for some codes, `details` — figures and ids for the administrator's decision (for example, `shortfall`, `available`, `operationId`), and the `reason` field — the reason in Ukrainian from the «What the user sees» column of [Operation sync codes](#operation-sync-codes). The offline till shows `reason` in the **Примітка** column of the **Офлайн-операції** screen.

## Sales sync

Sales, debt payments and shifts made on a computer without internet are applied by the server during the offline queue sync. Each operation is applied fully or not at all: all its records (register transactions, client plans, stock moves, a debt, cash ledger rows, the computer's shift) are saved together or none is saved. Sending an operation again does not duplicate records (see [One-time application of operations](#one-time-application-of-operations)).

### Operation kinds

| Kind | Operation | Records |
|---|---|---|
| `sale` | a sale of plans and goods to one client or without a client: by one payment method, by several payments, with a debt for the rest of the sum, or wholly on debt | client plans; a register transaction per payment; one stock deduction for the whole sale; a debt; cash ledger rows for cash payments |
| `debt_payment` | a payment of an existing debt | a register transaction linked to the debt; the class's paid sum (for a class debt); the debt status; a cash ledger row for cash |
| `shift_open` | a shift opened on the computer | the computer's shift |
| `shift_close` | a shift closed on the computer | the close data in the computer's shift |

The records of a sale are saved in this order: client plans, register transactions, stock deduction, debt, cash ledger rows, offline operation journal record. A failure at any step cancels all records of the operation.

The `dependsOn` field of an operation holds the ids of the earlier queue operations this one was made after (for example, a sale after the `shift_open` of its shift). Queue operations are applied in queue order.

Fields of the `sale` operation:

| Field | Meaning |
|---|---|
| `clientId` | client UUID; required when plans are sold or a debt remains and `clientOperationId` is not sent |
| `clientOperationId` | id of the `client_create` operation of a client created offline (see [Reference to a client created offline](#reference-to-a-client-created-offline)) |
| `clientName` | client name; when the client is found on the server, the transaction stores the full name from the card |
| `plans` | plans: `planId`, `planName`, `price` (unit price), `quantity` |
| `products` | goods: `productId`, `productName`, `price` (unit price), `quantity` |
| `workoutsIds` | ids of the classes the sale belongs to |
| `discount` | discount text, for example `10%` or `200 грн` |
| `price` | the sale sum after the discount |
| `paymentMethod` | payment method of a sale not split into several payments |
| `acquiringPosData` | the terminal's answer for a card payment |
| `payments` | several payments, 2 to 10: `paymentMethod`, `amount` (at least 0.01), `acquiringPosData`, `isPersonalAccount` (`true` — the payment is taken from the personal account); no other fields are allowed in a payment |
| `isPersonalAccount` | `true` — a sale without `payments` is paid from the personal account (see [Payment from the personal account](#payment-from-the-personal-account)) |
| `isCertificate` | `true` — payment for a certificate: a register transaction with the certificate mark |
| `partialAmount` | the sum paid now; the rest of `price` remains a debt |
| `onDebt` | `true` — the sale is wholly on debt |
| `total` | the sum the till received |
| `receiptNo` | the number of the computer's paper receipt, up to 32 characters |
| `shiftOperationId` | the id of the `shift_open` operation of the computer's shift |
| `clientPlanIds` | ids (UUID) of the client plans the sale creates: one per unit of `plans`, in the order of `plans`; optional |

- A payment in `payments` with a field not in the list is refused with the `INVALID_PAYLOAD` code.
- A number of `clientPlanIds` that differs from the number of units of `plans`, an id repeated in `clientPlanIds`, or the id of a plan that exists on the server is refused with the `INVALID_PAYLOAD` code.
- The sum paid now: the sum of `payments`, otherwise `partialAmount`, otherwise `price`; for a sale with `onDebt: true` — `0`.
- The sum of `payments` must equal `partialAmount` (when given) or `price` to the kopeck; otherwise the operation is refused with the `INVALID_PAYLOAD` code.
- `partialAmount` may not exceed `price`; otherwise the operation is refused with the `INVALID_PAYLOAD` code.
- A sale with `onDebt: true` may not contain `payments` or `partialAmount`; otherwise the operation is refused with the `INVALID_PAYLOAD` code.
- When the sum paid now is less than `price`, a debt for the difference is created: on the client of the sale, with the plans and goods of the sale.
- A sale wholly on debt creates no register transactions.
- A sale must contain at least one plan or product, the certificate mark (`isCertificate: true`) or a client name.
- Each plan of the sale is created in the client's card: one per unit of `quantity`.
- `receiptNo` and `shiftOperationId` are stored in every register transaction of the sale.

Payment methods (`paymentMethod`) accepted in offline operations:

| Value | Method |
|---|---|
| `0` | cash |
| `1` | bank transfer (payment by account) |
| `2` | card |

### Operation time

- A register transaction, a stock move, a debt and a client plan store the operation time. For an offline operation it is the computer's time at the moment of the action (`occurredAt`); for an online action it is the time of the server write.
- The date of a register transaction created during the sync equals the operation time.
- Transactions of a day, transactions of a period, the register transaction list and the period cash report are selected and ordered by the operation time. A sale made at 00:30 and synced later is shown in the report of the sale day in the studio time zone.
- A plan with a duration sold offline starts at the beginning of the sale day in the studio time zone; its end date is computed from the start date. The purchase date equals the operation time.
- A one-time plan sold offline is stored with the «Завершений» status and no classes left.
- The cash ledger row of a cash payment is stored with the operation time. When the ledger of the same account already has later rows, the balance of each of them up to the next balance reset is increased by the payment sum. The opening and closing balance of the period cash report follow the ledger rows ordered by the operation time.

### Shift

- A shift opened and closed on a computer without internet does not open or close a shift on the server.
- The automatic shift close closes only the current online shift and does not affect the computer's shift.
- An offline sale and an offline debt payment land in the online shift open at the moment of the operation, whatever day it was opened. When there is none — in a shift of the same day in the studio time zone: the last one opened before the moment of the operation, otherwise the first one opened after it.
- When the day had no shift, the server creates a shift marked «Офлайн»: opened and closed at the moment of the first operation of that day, with no working hours, signed «Офлайн». Further offline operations of that day land in this shift. A shift marked «Офлайн» never becomes the current shift.

The computer's shift is kept for the shifts report apart from the server's shifts. Its id is the id of the `shift_open` operation.

| Operation | Fields | Records |
|---|---|---|
| `shift_open` | `openingCash` — cash at the start of the shift | the computer's shift: open time, user, device, opening cash |
| `shift_close` | `closingCash` — cash at the end of the shift (required); `openOperationId` — the id of the `shift_open` operation; `zReports` — Z-reports: `fiscalNumber`, `register`, `cashRegisterNum`, `at` | close time, closing cash, Z-reports, the id of the close operation |

- A Z-report without `fiscalNumber` is not stored; up to 20 Z-reports are stored, each field up to 128 characters.
- When the `shift_open` operation is not on the server, the computer's shift is created from the close: the open time is the time of the first sale of that shift, otherwise the close time; the opening cash is not known.
- A close without `openOperationId` belongs to a shift opened online and does not change any computer's shift.

### Prices, stock and flags

- Prices and sums of the operation are taken from the computer.
- Product stock may become negative during the sync; the sale is not refused.
- A difference from the server data does not cancel the operation: the operation is applied, and the offline operation journal record stores a flag (the `flags` field).

| Flag | Condition |
|---|---|
| `price_changed` | the price of at least one line differs from the server's plan or product price at the time of the sync |
| `negative_stock` | after the deduction the stock of at least one product of the operation is below zero |
| `total_mismatch` | `total` differs from the sum of the sale's register transactions by more than a kopeck |

- A plan, product or client of the sale that is not on the server is a conflict: the operation is not applied, no records are created.

### Debt payment

- Two payments of the same debt made online and during the sync are applied one after the other.
- An online payment checks the debt and its remaining sum taking the earlier payment into account. When the debt is already paid or deleted, the payment is refused with the message «Борг уже погашено або видалено»; when the sum exceeds the remainder — with the message «Сума перевищує борг». No records and no receipt are created.
- The fiscal receipt of an online debt payment is created after the payment is saved. When the fiscal provider returns an error, the payment stays saved and its transaction is not fiscalized, as a sale whose receipt could not be created.
- A debt payment saved without a fiscal receipt (a fiscal provider error or an interruption after the save) stays saved. Sending it again does not create the receipt. The receipt is created manually with the **Fiscalize** ("Фіскалізувати") button on the transaction (see [Fiscalizing a transaction](/en/menu/pos#_3944-fiscalizing-a-transaction)).
- An offline payment is applied only when the debt is not paid off and the payment does not exceed the remaining debt.
- An offline payment not applied gets the `conflict` result; an admin's decision is needed. The debt is not paid a second time.
- A payment equal to the remaining debt pays the debt off.

### Bank transfer payment

- A transaction paid by bank transfer (`paymentMethod` = `1`), a debt payment included, is stored with the «Очікує на підтвердження» status whatever the computer sent. It is confirmed only in the online admin.
- Transactions paid by cash or card are stored with the «Підтверджено» status.

### What is not done during the sync

- Receipt fiscalization. Receipts are created after the sync (see [Fiscalization after the sync](#fiscalization-after-the-sync)).
- Client notifications: Telegram, push notifications, SMS.
- The admin notification about a product running out.
- The first plan bonus.

After the operation is saved, plans sold by `sale` are registered in the studio network. A registration failure does not cancel the operation; such a plan stays without the network mark and is registered by the next network fill.

### Operations not accepted offline

The server refuses these operations with the `rejected` result and the `OFFLINE_OPERATION_NOT_SUPPORTED` code, even when the computer sent them. No data changes.

| Operation | Kind or sign |
|---|---|
| Refund sent as a sale | `type: "Refund"` in a sale; a refund is sent as the `refund` operation |
| Personal account top-up | `balance_top_up`; `isBalanceTopUp: true` in a sale |
| Refund of a personal account top-up | `refund` of a sale with the account top-up mark |
| Refund of a sale paid through a terminal, and refund through a terminal | `refund` of a sale with terminal data (`acquiringPosData`); `refund` with `refundTransaction.acquiringPosData` |
| Personal account correction | `balance_correction` |
| Bonuses | `bonus` |
| Bank transfer confirmation | `payment_approve` |
| Transaction edit | `transaction_edit` |
| Transaction delete | `transaction_delete` |
| Monobank acquiring | `mono_acquiring` |

### Sales sync codes

The reason codes the server does not apply a sale or a debt payment with, and the text the user sees, are in [Operation sync codes](#operation-sync-codes).

## Class registration and new clients

A client registration for a class and a client creation made on a computer without internet are applied by the server during the offline queue sync. Sending an operation again does not duplicate its records (see [One-time application of operations](#one-time-application-of-operations)).

### Operation kinds

| Kind | Operation | Records |
|---|---|---|
| `client_create` | client creation | client card; loyalty card; entry in the shared clients registry of the studio network |
| `booking` | client registration for a class, including a class of a regular workout not yet created on the server, with one class taken from the client's plan | class client list; plan classes remaining; client plan history line |

### Client creation

Fields of the `client_create` operation:

| Field | Value |
|---|---|
| `name` | first name, required, up to 128 characters |
| `lastName` | last name, up to 128 characters |
| `phone` | phone, up to 32 characters; stored as `0XXXXXXXXX` |
| `email` | email, up to 128 characters |
| `comment` | comment, up to 1024 characters |
| `isCardManual` | `true` — the loyalty card number is set manually |
| `manualCard` | loyalty card number, up to 64 characters; used only with `isCardManual: true` |

- The client is created as in the online admin: loyalty card and the shared clients registry of the studio network. A client known to another studio of the network by phone is created from the network data.
- The operation result is the client id on the server: `{ "clientId": "<UUID>" }`.
- If the studio already has a client with this phone, the client is not created: the operation gets `conflict` with code `POSSIBLE_DUPLICATE`. The conflict message contains the ids of the studio clients with this phone.
- If the manually set card number is already registered to another client, the client is not created: `conflict` with code `CARD_NUMBER_TAKEN`.
- The id of the created client equals the id of the `client_create` operation. A repeated sending of an operation interrupted after the client was created gets `applied` with this client's id; no `POSSIBLE_DUPLICATE` conflict arises for it.

### Reference to a client created offline

- An operation for a client created on a computer without internet carries, instead of the client id, the `clientOperationId` field — the id of the `client_create` operation. The `booking`, `sale` and `certificate_redeem` operations accept this field.
- An operation with `clientOperationId` is applied only after the `client_create` operation it refers to. The `client_create` operation comes before it in the queue; the operation's `dependsOn` field contains the `client_create` operation id.
- If the `client_create` operation is not applied yet, the referring operation gets `retry`, the following operations of the queue get `pending`.
- If the `client_create` operation got `conflict` or `rejected`, the referring operation gets `conflict` with code `OFFLINE_CLIENT_NOT_APPLIED`.
- An operation must not carry both a client id and `clientOperationId`; such an operation is rejected with code `INVALID_PAYLOAD`.

### Class registration

The content of the `booking` operation is the content of the online class booking with additional fields:

| Field | Value |
|---|---|
| `id` | client UUID; not sent when `clientOperationId` is sent |
| `clientOperationId` | id of the `client_create` operation of a client created offline |
| `workoutId` | workout id |
| `date` | class date and time, ISO 8601 |
| `status` | `0` — booked, `2` — visited |
| `paymentStatus` | `plan` — by plan, `payed` — paid, `not_payed` — not paid |
| `clientPlanId` | id of the client plan one class is taken from |
| `saleOperationId` | id of the `sale` operation that paid for the class |
| `redeemOperationId` | id of the `certificate_redeem` operation that created the plan `clientPlanId` (see [Dependent operations](#dependent-operations)) |

- The registration is applied as an online class booking. If the class of a regular workout on this date is not created on the server yet, it is created together with the list of its regular clients; their registrations are kept.
- The class client list, the class taken from the plan and the plan history line are saved together: all or none.
- Taking a class from the plan decreases the classes remaining by one. A plan whose remainder becomes `0` gets the status «Ended». A class of a workout marked as rent takes nothing from the plan.
- A client who already holds a seat in the class (a regular client or a booking through the app) does not take a second seat: the registration changes the status of the booking.
- The seat check and the class registration run one after another with bookings for the same class through the mobile app and QR self check-in.
- The plan must match the workout type: a personal workout takes a plan of type «Personal», any other workout a plan of type «Regular». For a workout marked as rent the plan type and status («New», «Ended») are not checked.
- A plan with the status «New» is activated at the first visit, as at an online check-in: the plan must have a duration other than `0`, a type that matches the workout and classes remaining above `0`. The start date is the operation date in the studio time zone; the end date is the start date plus the plan duration. The activation, the activation line in the plan history and the class taken are saved in the registration transaction. A plan activated before the sync in another way (another class, a QR check-in, an administrator) keeps its start date, end date and activation line; the registration only takes the class.
- The plan validity is checked at the operation time. A plan with the status «Ended» is charged when its end date is not earlier than the operation date and has passed by the sync, and its classes remaining are above `0`. A plan with the status «Ended» without an end date, or with an end date that has not passed by the sync, is not charged: the operation gets the `PLAN_CLOSED` conflict for an administrator to review.
- No notification about the registration is sent to the client or to the coach, as for an online class booking.
- Taking a class from the plan creates a line in the client plan history: the operation time on the computer (`occurredAt`), the class date, the workout, the registration status, the classes remaining after the class is taken and the computer user. The line is shown in the client plan history. A registration that takes nothing from a plan creates no history line.
- A registration with the status `2` (visited) sets the client's last visit date to the operation time on the computer (`occurredAt`) when the last visit date is not set or is earlier than the operation time. A registration with the status `0` (booked) does not change the last visit date.

### Checks during the sync

The checks take into account the records saved by the moment the operation is applied. An operation that fails a check gets `conflict` with the reason code; the class client list and the plan do not change.

The reason codes and the text the user sees are in [Operation sync codes](#operation-sync-codes). A registration paid by a sale with `saleOperationId` that got `conflict` or `rejected` gets the `OFFLINE_SALE_NOT_APPLIED` code; a registration by a plan from a certificate redemption with `redeemOperationId` that got `conflict` or `rejected` gets the `dependency_rejected` code.

- The plan classes remaining do not go below zero during the sync.
- A booking status other than `0` and `2` is rejected with code `INVALID_PAYLOAD`.
- A registration with `paymentStatus: plan` and no `clientPlanId` is rejected with code `INVALID_PAYLOAD`.
- After the write, the change of the plan remainder is passed to the studio network; a plan activated at the registration is passed to the network before the remainder change. A failure to pass it does not cancel the operation.

### Class and client actions not available offline

- Wait list.
- Moving and cancelling classes, coach substitution, room change.
- Creating and editing workouts.
- Automatic registration by the client card from the mobile app.
- Editing and deleting a client.
- Client import and export.
- QR self check-in books the client for the class on the server.

## Personal account, certificates and refunds

Payments from the personal account, certificate sales and redemptions, and refunds made on a computer without internet are applied by the server during the sync of the offline queue. Each operation is applied fully or not at all: if the operation is not applied, none of its records is saved. Sending the operation again does not duplicate records (see [One-time application of operations](#one-time-application-of-operations)).

### Operation time and the "Offline" mark

- Register transactions, personal account history rows, the sale date and the usage date of a certificate, the plans created by a certificate redemption, and stock movements are saved with the operation time on the computer (`occurredAt`).
- A personal account history row and a certificate written during the sync carry the offline operation id (`offlineOperationId`) and are shown with the "Offline" ("Офлайн") mark. A certificate sold offline carries the id of the sale operation; a certificate sold online and redeemed offline carries the id of the redemption operation.
- Reports, the register transaction list and the personal account history count these records by the operation time.
- Fiscal receipts are not created during the sync. The fiscalization state of the transactions is described in [Fiscalization after the sync](#fiscalization-after-the-sync).
- Client notifications (Telegram, push notifications, SMS) are not sent.

### Payment from the personal account

| Operation | Personal account payment mark |
|---|---|
| `sale` | `isPersonalAccount: true` — the whole sale; in a sale with `payments` — `isPersonalAccount: true` in one of the payments |
| `debt_payment` | `isPersonalAccount: true` |
| `certificate_sale` | `isPersonalAccount: true` together with `paymentMethod`, or in one of the `payments` |

- A payment from the personal account must name the client (`clientId` or `clientOperationId`); otherwise the operation is rejected with code `INVALID_PAYLOAD`.
- A sale with `payments` must not carry `isPersonalAccount: true` at the sale level; otherwise the operation is rejected with code `INVALID_PAYLOAD`.
- The sum is taken from the client's balance the same way as an online payment: the balance decrease and the sufficiency check are one database write. The personal account balance does not become negative.
- A register transaction paid from the personal account carries the personal account payment mark and the "Confirmed" status regardless of `paymentMethod`; no terminal data, cash ledger row or fiscal receipt is created for it.
- A "Deduction" row is created in the personal account history: the sum, the names of the plans and products (for a debt payment — with the "(борг)" mark, for a certificate — "Сертифікат") and the link to the register transaction.
- If the balance on the server is smaller than the payment (the money was spent online or through the mobile app while the computer was without internet), the operation gets `conflict` with code `balance_insufficient`; the `details.shortfall` field contains the missing sum. None of the operation's records is saved.

### Certificate sale

The content of the `certificate_sale` operation is the content of the online certificate sale with the payment fields:

| Field | Value |
|---|---|
| `clientId` | client UUID; optional, required for a payment from the personal account |
| `description` | comment |
| `price` | certificate price |
| `plans` | certificate plans: `id` (plan UUID), `quantity` (whole number from 1) |
| `expiresAt` | expiration date, ISO 8601 |
| `duration` | validity in days, from 1 |
| `paymentMethod` | payment method of the whole price |
| `isPersonalAccount` | `true` — the price is paid from the client's personal account |
| `payments` | several payments, 2 to 10: `paymentMethod`, `amount`, `acquiringPosData`, `isPersonalAccount`; no other fields are allowed in a payment; the payments add up to `price` to the kopeck |
| `receiptNo` | number of the computer's paper receipt, up to 32 characters |
| `shiftOperationId` | id of the `shift_open` operation of the computer's shift |

- The certificate id equals the id of the `certificate_sale` operation.
- The certificate number is computed by the online sale rule: `CRT` and the first 10 characters of the SHA-256 value of the string `<clientId>_<certificate id>`, written in base 36 in upper case. If the `clientId` field is not sent, the string has `undefined` in its place; if `null` is sent — `null`.
- If the server already has a certificate with this number, the operation gets `conflict` with code `certificate_number_taken`; the certificate and transactions are not created.
- The certificate is saved with the "Active" status and the sale date equal to the operation time.
- A register transaction with the certificate mark is created for each payment; for a cash payment — a cash ledger row with the description "Сертифікат". An operation without `paymentMethod` and `payments`, or with price `0`, creates no register transactions.
- Operation result: `id`, `certificateNumber`, `transactionIds`.

### Certificate redemption

The content of the `certificate_redeem` operation is the certificate id and the content of the online redemption:

| Field | Value |
|---|---|
| `certificateId` | certificate id; for a certificate sold offline — the id of the `certificate_sale` operation |
| `clientId` | UUID of the client redeeming the certificate; not sent if `clientOperationId` is sent |
| `clientOperationId` | id of the `client_create` operation of a client created offline |
| `status` | `Redeemed`; optional |
| `clientPlanIds` | ids (UUID) of the client plans the redemption creates: one per unit of the certificate's plans, in the certificate's order; optional |

- Redemptions of the same certificate made online and during the sync are applied one after another. A redemption saved online earlier is taken into account: a certificate is redeemed once; the second operation gets the `certificate_already_redeemed` conflict.
- Validity is checked by the calendar day of the operation in the studio time zone: a certificate is valid through the last day of its validity inclusive. A certificate without an expiry date is valid. A certificate with the "Expired" status whose last day of validity is not earlier than the operation day is redeemed.
- The redemption sets the "Redeemed" status, the usage date (the operation time) and the certificate's client. For each unit of the certificate's plans, a client plan is created with the "New" status and the purchase date equal to the operation time. After saving, the plans are sent to the studio network; a sending failure does not cancel the operation.
- A number of `clientPlanIds` that differs from the number of the certificate's plans, an id repeated in `clientPlanIds`, or the id of a plan that exists on the server is rejected with code `INVALID_PAYLOAD`.
- Operation result: `clientPlanIds`.

### Dependent operations

| Operation | Reference | Operation it depends on |
|---|---|---|
| `certificate_redeem` | `certificateId` of a certificate sold offline | `certificate_sale` |
| `booking` on a plan created by an offline certificate redemption | `clientPlanId` — one of the redemption's `clientPlanIds`; `redeemOperationId` — id of the `certificate_redeem` operation | `certificate_redeem` |
| `refund` of a sale made offline | `saleOperationId` | `sale` |

- The operation another operation depends on comes before it in the queue; its id is in the `dependsOn` field.
- If the operation it depends on is not applied yet, the dependent operation gets `retry`, the following operations of the queue get `pending`.
- If the operation it depends on got `conflict` or `rejected`, the dependent operation gets `conflict` with code `dependency_rejected`; the `details.operationId` field contains the id of the operation it depends on.

### Refund

The content of the `refund` operation is the content of the online refund with additional fields:

| Field | Value |
|---|---|
| `transactionId` | id of the sale's register transaction; not sent if `saleOperationId` is sent |
| `saleOperationId` | id of the `sale` operation of a sale made offline |
| `paymentIndex` | position of the register transaction of that sale, from `0` (one transaction per payment, in the order of `payments`); `0` by default |
| `refundTransaction` | the refund: `price` (refund sum, from 0.01), `paymentMethod`, `plans`, `products`, `workoutsIds`, `type` (`Refund`) |
| `receiptNo` | number of the computer's paper receipt, up to 32 characters |
| `shiftOperationId` | id of the `shift_open` operation of the computer's shift |

- A refund is applied the same way as an online refund: the refund register transaction; the refunded products are added to the stock (stock movement "Refund"); the sum is returned to the personal account if the sale was paid from it (history row "Refund"); the refund is added to the sale's list of refunds; for a sale linked to a debt, the paid sum of the class is reduced and a paid debt becomes unpaid again; for cash, a "Refund" cash ledger row is created.
- Client plans do not change on a refund, as on an online refund.
- A refund and other operations on the same sale made online and during the sync are applied one after another. A refund of a sale that is not on the server gets `conflict` with code `TRANSACTION_NOT_FOUND`; no records are created.
- The sum available for refund is the sale sum minus the sums of all its refunds. If the refund sum exceeds the available sum by more than a kopeck, the operation gets `conflict` with code `refund_exceeds_remaining`; the `details.available` field contains the available sum. A refund made both online and offline for the full sale sum is applied once: the second operation gets a conflict with available sum `0`.
- A refund of a personal account top-up, a refund of a sale paid through a terminal and a refund through a terminal (`refundTransaction.acquiringPosData`) are rejected with code `OFFLINE_OPERATION_NOT_SUPPORTED`.
- Operation result: `transactionId` — the id of the refund transaction.

### Personal account, certificate and refund sync codes

The reason codes the server does not apply an operation with, and the text the user sees, are in [Operation sync codes](#operation-sync-codes). For the `dependency_rejected` code the `details.operationId` field holds the id of the operation this one depends on.

## Till work without internet

Without a connection to the server the till performs the actions below using the till data: the last package received together with the operations made at the till after it. Each action becomes one queue operation and is sent to the server once the connection is back.

### Available actions

| Action | What changes in the till data at once |
|---|---|
| Opening and closing the offline shift | The till's current shift |
| Sale of plans, products and single classes; split payment; "pay later" | Client plans, product stock, client debt, shift total |
| Debt payment | Debt balance |
| Payment from the personal account | Personal account balance |
| Certificate sale | Certificate with its number, shift total |
| Certificate redemption | Certificate state, client plans |
| Refund | Refundable amount of the sale, product stock, personal account balance, debt balance |
| Bank transfer payment | Transaction marked "not confirmed" |
| Class registration | Class roster, sessions left on the plan |
| Client creation | Client list |
| Self check-in QR on the reception screen | — |

### Repeated press

Pressing an action button again (including "Pay") does not create a second operation: the till returns the result of the first press.

### Offline shift

- The offline shift is closed until it is opened manually. Payments are accepted only while the offline shift is open.
- The cash in the till is entered at closing. Without an entered amount the shift closes with the expected amount: cash at the start of the shift plus cash payments and minus cash refunds of the shift.
- The X-report of the offline shift is made from the transactions of this shift.

### Document number

A till document has a number like `D1-0005`: the till number and the document's sequence number on that computer. The till number is set when offline mode is enabled (see [Several tills](#several-tills)); document numbers of computers with different till numbers do not coincide.

### Product stock

- Product stock in the till data is the package stock minus the sales and plus the product refunds made at the till.
- A product sale above this stock is not made, as online. Several lines of one product in a sale count together.
- During the sync the sale is accepted even when the server stock becomes negative; the operation gets the `negative_stock` flag (see [Prices, stock and flags](#prices-stock-and-flags)).

### Personal account

- The personal account balance in the till data is the package balance minus payments from the account and plus refunds to the account made at the till.
- A payment from the account above this balance is not made: the till shows the available amount and offers to pay the rest another way or leave a debt. Several account payments of one client together do not exceed the balance.

### Certificates

- The number of a certificate sold at the till is computed by the same rule as on the server; the printed number matches the number on the server.
- Redemption marks the certificate redeemed and creates the certificate's plans for the client. Class registration on such a plan is available at once.

### Refunds

- Refunds are available for sales in the till data (the last 3 days) and for sales made at the till. The available amount is the transaction amount minus the refunds known to the till.
- Money is returned the same way it was paid. A refund to the personal account increases the balance in the till data.
- A product refund returns it to stock. Client plans are not changed by a refund.
- A refund of a debt payment increases the debt balance by the refund amount. A fully paid debt for a class becomes open again after such a refund.

### Class registration

- Registration with a deduction from a plan reduces the sessions left by 1; a plan with the "New" status becomes active, a plan with no sessions left becomes ended.
- A plan sold at the till without internet is available for registration right after the sale.
- A registration paid by a plan requires choosing the client's plan.
- A repeating registration is not available without internet.

### Till refusals

The till refuses with an explanation and does not queue the operation. The codes and messages are in [Till refusal codes](#till-refusal-codes).

### Reports

The "Summary", "Products", "Plans" reports and the X-report for the offline period are made from the transactions of the till data: sales and refunds from the package and those made at the till. The report total equals the total of the operations in the queue and those already synced.

### Self check-in QR

The reception screen shows the code of the current hour from the till data for the chosen set of rooms. Without a code for the current hour (data older than 48 hours or self check-in turned off) the QR is not shown; the message "Самостійний чекін зараз недоступний: у даних каси немає коду на цю годину." is shown instead.

## Going offline and back

### The offline till in the browser

- The offline till opens at `http://127.0.0.1:9899` from the **Відкрити офлайн-касу** button, from the «Сервер FitStudioCRM недоступний» window or from the error window. Its tab is named «Fitshandler Офлайн».
- The offline till is entered without the Google sign-in: it works on behalf of the user who enabled offline mode on the computer.
- The offline till's menu: **Розклад**, **Клієнти**, **Абонементи**, **Товари**, **Сертифікати**, **Каса**, **Звіти**, **Офлайн-операції**. The **Тренування**, **Тренери**, **Зали**, **Налаштування** sections and the **Підтримка**, **Сповіщення** buttons are absent in the offline till.
- Not shown in the offline till: the «Поповнення особового рахунку» sale type; the personal account **Коригувати** button; deleting and restoring a debt; client import and export; the **Підтвердити** button of a bank transfer payment; repeating bookings and the waiting list; the **Скасувати тренування**, **Перейти до тренування** buttons and the class settings; the **Не фіскалізовано** tab, issuing a fiscal receipt and confirming a missing receipt.
- On registration for a regular class the text «Повторювані записи недоступні в офлайн-режимі» (in the client window) or «Повторювані записи й лист очікування недоступні в офлайн-режимі.» (in the class window) is shown.
- Payment methods: cash, card without the terminal, personal account, bank transfer. With a bank transfer payment the message «Оплата рахунком буде підтверджена після синхронізації.» is shown.
- A sale with several payment methods and a certificate sale with its payment go as one operation.
- The offline till's shift opens and closes without the fiscal integration.

### Offline banner

The banner above the offline till's menu is always shown: «Офлайн · дані станом на <date and time> · <state> · <action>» and the link «Несинхронізовані операції: N», which opens the **Офлайн-операції** screen.

| Connection state (see [Connection states](#connection-states)) | State text | Banner colour |
|---|---|---|
| No internet | Немає інтернету | yellow |
| Server unavailable | Сервер FitStudioCRM недоступний | yellow |
| Online | Звʼязок із сервером відновлено | green |
| The offline service does not answer | Офлайн-сервіс не відповідає | red |

| Condition | Action text | Banner colour |
|---|---|---|
| The server does not accept the computer's access | Увімкніть офлайн-режим на цьому компʼютері повторно в онлайн-адмінці | red |
| The server does not accept the queue from this version | Оновіть Device Handler, щоб операції передавались на сервер | red |
| The data are stale (see [Stale data](#stale-data)) | Дані каси застарілі | red |

- With several conditions one action is shown, in the order of the table.
- The data date and time are shown in the studio's time zone.
- The banner refreshes automatically.

### The «Офлайн-операції» screen

- The screen shows the offline till's operations, newest first, in the columns **Час**, **Операція**, **Стан**, **Примітка**. Time is shown in the studio's time zone. The screen refreshes automatically and with the **Оновити** button.

| State | Meaning |
|---|---|
| Очікує синхронізації | the operation is in the queue, not sent to the server yet |
| Синхронізовано | the operation is applied on the server |
| Відхилено сервером | the server rejected the operation; the reason is in the **Примітка** column |
| Потребує уваги | a conflict during the sync |
| Результат невідомий · очікує підтвердження | the operation was handed over from the online admin without a server answer; it is in the offline till's queue |
| Результат невідомий · очікує передачі в чергу | the operation was handed over from the online admin; it is not in the offline till's queue yet (for example, the offline shift is not open) |
| Не прийнято офлайн-касою | the till data do not allow the operation; the **Примітка** column holds the reason and the text «Перевірте операцію в онлайн-адмінці після відновлення звʼязку.» |

- When the offline service does not answer, the text «Офлайн-сервіс не відповідає. Список буде оновлено автоматично.» is shown.

### Back to the online admin

- When the connection state becomes «Online», the offline till shows the «Звʼязок із сервером відновлено» window with the **Пізніше** and **Перейти в онлайн-адмінку** buttons.
- The **Перейти в онлайн-адмінку** button:
  - with the offline shift open, opens the offline shift close; after the close the window is shown again;
  - with the offline shift closed, opens the online admin at the address the offline till was opened from;
  - when the offline shift state could not be read, does nothing.
- When the offline till does not know the online admin's address, the button is not shown; the window holds the text «Відкрийте онлайн-адмінку FitStudioCRM у браузері так, як зазвичай.»
- The **Пізніше** button closes the window; the window is shown again while the connection state stays «Online».
- Queue operations are sent to the server without user action, regardless of the window.

### Reminder about an open offline shift

- The online admin on a computer where this studio's offline till has an open shift shows the «Відкрита офлайн-зміна» window with the **Пізніше** and **Перейти до закриття зміни** buttons.
- The **Перейти до закриття зміни** button opens the offline till in a new tab with the shift close open.
- The **Пізніше** button closes the window; the reminder is shown again until the offline shift is closed.

### Server unavailable mode

The online admin checks the server when the Device Handler is switched on on the computer, offline mode is enabled for this studio and the offline till is running.

- The online admin checks the server regularly. A failed check: the server did not answer or reported it is temporarily unavailable.
- The «Сервер FitStudioCRM недоступний» window is shown after several failed checks in a row.

- One failed check does not show the window; a successful check starts the count again.
- The «Сервер FitStudioCRM недоступний» window holds the text «Сервер FitStudioCRM не відповідає. Роботу можна продовжити в офлайн-касі на цьому компʼютері: вона відкриється в новій вкладці, ця сторінка залишиться відкритою.» and the **Закрити** and **Перейти в офлайн-касу** buttons.
- When there are operations with an unknown result, the window shows their number (see [Operations with an unknown result](#operations-with-an-unknown-result)).
- The **Перейти в офлайн-касу** button opens the offline till in a new tab; the online admin page with unsaved form data stays open.
- After a successful check the window closes. A window closed with **Закрити** is not shown again until the first successful check.
- Going back online follows [Back to the online admin](#back-to-the-online-admin).

### Error window

- The window of a server or connection error shows the text «Спробуйте перезавантажити сторінку.»
- When this studio's offline till runs on the computer, the window also shows «Якщо сервер не відповідає, продовжте роботу в офлайн-касі.» with a link that opens the offline till in a new tab.
- A window with a refusal whose reason the server explained does not show these texts.

### Operations with an unknown result

- Online admin operations with an operation id: sale, refund, debt payment, class registration, client creation, certificate sale and redeem.
- The operation id is created when the action is first sent. Pressing the same action again with the same data sends the same id and the data of the first send; the server applies the operation once and answers a repeated send with the result of the first.
- After the server's answer (a success or a refusal with its reason) the id is forgotten; the next action gets a new id.
- An action without a server answer (no connection, the server did not answer or reported a failure) gets the «Результат невідомий» state. The error window shows the text «Сервер не відповів, тому результат операції невідомий. Повторне виконання тієї самої операції не створить її вдруге.»
- Operations with an unknown result are kept in the computer's browser and handed to the offline till on every move there, with the same id and data. The offline till queues them once the offline shift is open; after the sync the operation exists on the server once — both when the server applied it before the connection was lost and when it did not.
- Operations older than 24 hours are not handed to the offline till.
- A plan sale handed to the offline till that the server has already applied online creates no plans again during the sync. The offline till creates the sale's plans in its data under its own ids; the server's answer to such a sale contains the field `planIdMap` (offline till plan id → client plan id on the server) and the field `clientPlanIds` (plan ids on the server in the order of the sale lines).
- The match is made when, for every plan of the sale, the server has exactly as many plans of that kind for this client as units sold, created no earlier than 10 minutes before the online sale reached the server and no later than 10 minutes after it.
- After an answer with `planIdMap` the server does not look at the rest of the request's operations (status `pending`). The offline till replaces the offline till plan id with the server plan id in the queued operations, the plan in the till data gets the server id, and the queue is sent again. A class registration on such a plan takes the class from the plan on the server; no second plan is created.
- When no match is made, the ids are not changed; a class registration on a plan created by the offline till gets the result `conflict` with the code `PLAN_NOT_FOUND` and is shown on the **Офлайн-операції** screen with the status «Потребує уваги».
- Such a class registration is not corrected automatically: it stays on the [POS → Needs attention](/en/menu/pos#_398-needs-attention) tab of the online admin; the administrator creates the plan for the client by hand and registers the visit again.
- An operation with an unknown result does not need to be repeated by hand.
- When the online admin opens and when the server answers again, the online admin asks the server for the result of every operation with an unknown result and shows a message:

| Server answer | Message | Operation state in the browser |
|---|---|---|
| the operation was applied | «Операцію «<kind>» від <date and time> виконано.» | forgotten |
| the operation was refused or the server never received it | «Операцію «<kind>» від <date and time> не виконано. За потреби виконайте її повторно.» | forgotten |
| the operation stopped after a step that cannot be undone | «Операцію «<kind>» від <date and time> не завершено на сервері. Перевірте її результат перед повторним виконанням.» | forgotten |
| the operation is being applied | no message | stays «Результат невідомий» |

- An operation handed to the offline till stays «Результат невідомий» until the server receives it; once the server has decided, it is forgotten without a message. Its state is shown on the offline till's **Офлайн-операції** screen.
- When the server does not answer the result request, the remaining operations stay «Результат невідомий» until the next check.
- The date and time of the operation are shown in the studio's time zone.

### Needs attention

- Operations the server did not apply during the sync (result `conflict` or `rejected`) or applied with a mark (`price_changed`, `total_mismatch`, `negative_stock`) are shown in the online admin on the [POS → Needs attention](/en/menu/pos#_398-needs-attention) ("Потребує уваги") tab with the reason and the description of the mark.
- The same tab shows the fiscal receipts of offline operations in the state **Sale receipt check needed**, **Fiscalization error** or **Fiscalization result unknown**, and the payments by account that wait for confirmation.
- The administrator resolves an operation with the tab's actions or marks it **Reviewed**; a resolved operation moves to the reviewed list.
- For every operation not applied, one notification is created for the administrators however many times it is synced.

## Fiscalization after the sync

The offline till creates no fiscal receipts, neither without internet nor while the FitStudioCRM server is unavailable: the buyer gets a non-fiscal document with a number (`receiptNo`). The fiscal receipts of the sales and refunds of the offline period are created after the sync, through the server, by the studio's fiscal integration (Checkbox or Vchasno.Kasa), on the [Point of sale → Not fiscalized](/en/menu/pos#_397-not-fiscalized) tab.

### Fiscalization state

| State (`fiscalState`) | Badge | Meaning |
|---|---|---|
| `pending` | **Awaiting fiscalization** ("Очікує фіскалізації") | the transaction waits for a fiscal receipt and is shown on the **Not fiscalized** tab |
| `error` | **Fiscalization error** ("Помилка фіскалізації"); without a provider error text — **Fiscalization result unknown** ("Результат фіскалізації невідомий") | the last attempt failed or ended without a stored receipt; the provider's error text is in `fiscalError`; the transaction is shown on the **Not fiscalized** and **Needs attention** tabs |
| `not_required` | **No fiscalization needed** ("Не потребує фіскалізації") | no receipt is created |
| `needs_check` | **Sale receipt check needed** ("Потребує перевірки чека продажу") | a refund the sale receipt found may include; no return receipt is created until an administrator confirms (see [Fiscalizing a transaction](/en/menu/pos#_3944-fiscalizing-a-transaction)); the transaction is shown on the **Not fiscalized** and **Needs attention** tabs, where the administrator confirms whether the sale receipt includes the refund |
| `fiscalized` | **Fiscalized** ("Фіскалізовано") | the receipt is created |

### Sales

- A sale, debt payment or certificate sale transaction paid in cash, by card or by bank transfer has the state **Awaiting fiscalization** after the sync when the studio has an active fiscal integration at the time of the sync. Without an active fiscal integration no state is set.
- A personal-account payment gets no state and needs no receipt, as online. A transaction with a zero amount gets no state.
- A sale paid in parts has a separate transaction per payment; each transaction is fiscalized with its own receipt for the amount of that payment with its payment method.
- A bank-transfer payment is fiscalized regardless of the payment confirmation.

### Refunds

- A partial refund of a sale not fiscalized yet is allowed. Such a refund gets no receipt of its own and has the state **No fiscalization needed**: the sale receipt is created for the sale amount less the refunds, with the lines less the refunded quantities.
- A full refund of a sale not fiscalized yet: no receipt is created, neither for the sale nor for the refund; both transactions have the state **No fiscalization needed**.
- A refund of a fiscalized sale has the state **Awaiting fiscalization** after the sync. The refund receipt is created through the same fiscal register as the sale receipt, against the sale receipt.
- A refund made after the sale receipt was created for the net amount is fiscalized against that receipt.
- When the fiscal provider already holds a sale receipt created by an earlier attempt before the refund was made, that receipt is stored; the refunds not included in its amount get the state **Awaiting fiscalization** and are fiscalized with return receipts.
- A refund, partial or full, of a sale in the state **Fiscalization error** or with the status **Receipt sent, number unknown** (the sale receipt may have been created at the provider) gets the state **Awaiting fiscalization**; the state of the sale does not change. The rules for a partial and a full refund of a sale not fiscalized yet do not apply to such a sale. After the sale is fiscalized, the refunds included in its receipt amount get the state **No fiscalization needed**, the others are fiscalized with return receipts (see [Fiscalizing a transaction](/en/menu/pos#_3944-fiscalizing-a-transaction)).
- These rules also apply to refunds made online of a sale made offline.

### One receipt per transaction

- At most one fiscal receipt is created for a transaction. A provider error leaves the transaction on the **Not fiscalized** tab in the state **Fiscalization error**; a retry does not create a second receipt.
- The mode of an unavailable FitStudioCRM server fiscalizes the same way: only after the sync, through the server.

## Refusal codes

### Till refusal codes

The till refuses with an explanation and does not queue the operation. The message is shown in the offline till.

| Code | Message | Condition |
|---|---|---|
| `SHIFT_NOT_OPEN` | Відкрийте офлайн-зміну, щоб приймати оплати. / Цю офлайн-зміну не відкрито. | Payment without an open offline shift; closing a shift that is not the open offline shift |
| `SHIFT_ALREADY_OPEN` | Офлайн-зміну вже відкрито. | Opening an offline shift while an offline shift is open |
| `PAYMENT_METHOD_NOT_AVAILABLE_OFFLINE` | Цей спосіб оплати недоступний в офлайн-режимі. | A payment method other than cash, card without a terminal, personal account and bank transfer |
| `BALANCE_INSUFFICIENT` | На особовому рахунку недостатньо коштів: доступно … грн. Оплатіть решту іншим способом або залиште борг. | Account payment above the balance in the till data |
| `INSUFFICIENT_STOCK` | Недостатньо товару на складі: … | A product sale above the stock in the till data |
| `PLAN_EXHAUSTED` | На абонементі не лишилося занять. | Deduction from a plan with no sessions left |
| `PLAN_FROZEN`, `PLAN_EXPIRED`, `PLAN_NOT_FOR_CLASS`, `PLAN_NOT_ACTIVE` | Абонемент заморожено. / Термін дії абонемента минув. / Цей абонемент не діє на це заняття. / Абонемент не активний. | The plan cannot pay for the class |
| `PLAN_NOT_FOUND` | Цього абонемента клієнта немає в даних каси. / Абонемента немає в даних каси. / Абонемента сертифіката немає в даних каси. | The plan is not in the till data: for a class registration, a plan sale, a certificate sale or redemption |
| `PRODUCT_NOT_FOUND` | Товару немає в даних каси. | A sale of a product that is not in the till data |
| `INVALID_PAYLOAD` | Оберіть абонемент, з якого буде списано заняття. / Вкажіть ім'я клієнта. / Сума повернення має бути більшою за нуль. / Оплата з особового рахунку потребує клієнта. / Вкажіть термін дії сертифіката. / Частини оплати не дорівнюють ціні сертифіката. / Продажу, яким оплачено заняття, немає в черзі каси. / Додайте до продажу абонемент, товар або клієнта. / Поле … заповнено некоректно. | The action's data is incomplete or invalid; the text names what to correct |
| `NO_FREE_SEATS` | На занятті немає вільних місць. | All seats of the class are taken |
| `OCCURRENCE_NOT_FOUND`, `OCCURRENCE_CANCELLED` | Заняття немає в даних каси. / Заняття скасовано. | The class is not in the till data or is cancelled |
| `CLIENT_NOT_FOUND` | Клієнта немає в даних каси. | The client is not in the till data |
| `CERTIFICATE_NOT_FOUND` | Сертифіката немає в даних каси. | The certificate is not in the till data |
| `CERTIFICATE_ALREADY_REDEEMED` | Сертифікат уже погашено. | The certificate is redeemed |
| `CERTIFICATE_EXPIRED` | Термін дії сертифіката минув. | The certificate's last valid day in the studio time zone has passed |
| `REFUND_SALE_NOT_FOUND` | Продажу немає в даних каси. | The sale is not in the till data |
| `REFUND_EXCEEDS_REMAINING` | Сума повернення більша за доступну: … грн. | The refund is above the available amount |
| `REFUND_PAID_BY_TERMINAL` | Продаж, оплачений через термінал, повертається лише онлайн. | The sale was paid through a terminal |
| `REFUND_OF_TOP_UP` | Поповнення особового рахунку не повертається в офлайн-режимі. | Refund of a personal account top-up |
| `DEBT_NOT_FOUND` | Боргу немає в даних каси. | The debt is not in the till data |
| `DEBT_OVERPAYMENT` | Сума оплати більша за залишок боргу: … грн. | Payment above the debt balance |
| `DEBT_NOT_SYNCED` | Борг, створений без інтернету, можна оплатити після синхронізації. | The debt was created at the till without internet |
| `CLIENT_NOT_SYNCED` | Сертифікат клієнту, створеному без інтернету, можна продати після синхронізації. | Certificate sale to a client created at the till |
| `POSSIBLE_DUPLICATE` | Клієнт із цим номером телефону вже є в даних каси. | Client creation with an existing phone number |
| `CARD_NUMBER_TAKEN` | Картка з цим номером уже належить іншому клієнту. | The card number belongs to another client |
| `INVALID_OPERATION_ID` | Некоректний ідентифікатор операції. | An action with an operation id that is not a UUID |
| `OPERATION_ID_REUSED` | Цей ідентифікатор операції вже використано для іншої дії. | A repeated action with the same operation id and other data |
| `OFFLINE_NOT_AVAILABLE` | Ця дія недоступна в офлайн-режимі. | An action from the list of actions not available offline |
| `SELF_CHECK_IN_UNAVAILABLE` | Самостійний чекін зараз недоступний: у даних каси немає коду на цю годину. | The reception screen: the till data has no self check-in code for the current hour |

### Operation sync codes

The sync result sets the state of the operation on the **Офлайн-операції** (Offline operations) screen of the offline till and whether it is shown on the [Каса → Потребує уваги](/en/menu/pos#_398-needs-attention) tab of the online admin:

| Result | State on the **Офлайн-операції** screen | **Потребує уваги** tab | Notification to admins |
|---|---|---|---|
| `applied` | Синхронізовано (Synced) | only an operation with the `price_changed`, `total_mismatch` or `negative_stock` mark | no |
| `rejected` | Відхилено сервером (Rejected by the server) | yes, except the `INVALID_ID` and `IDEMPOTENCY_KEY_REUSED` refusals (see [Operation check refusals](#operation-check-refusals)) | yes, except the `INVALID_ID` and `IDEMPOTENCY_KEY_REUSED` refusals |
| `conflict` | Потребує уваги (Needs attention) | yes | yes |
| `retry`, `in_progress`, `pending` | Очікує синхронізації (Waiting for sync) | no | no |

- The reason on the **Потребує уваги** tab, in the notification and in the **Примітка** column of the **Офлайн-операції** screen is the text from the «What the user sees» column.
- The notification to admins: «Офлайн-операцію «<вид>» від <дата й час> не виконано. <причина> Перегляньте розділ Каса → Потребує уваги.» The notification is created once per operation however many times it is synced again.
- A sum from the `details` field is shown on its own line: «Нестача коштів: … грн.» (`shortfall`), «Доступно до повернення: … грн.» (`available`).
- A code not in the table is shown as «Операцію не виконано (код <код>).»

| Code | Result | Operations | Condition | What the user sees |
|---|---|---|---|---|
| `OFFLINE_OPERATION_NOT_SUPPORTED` | `rejected` | any | the operation is not accepted offline (see [Operations not accepted offline](#operations-not-accepted-offline)) | Операція не підтримується сервером. |
| `INVALID_PAYLOAD` | `rejected` | any | the operation content does not match the format | Дані операції некоректні. |
| `CLIENT_NOT_FOUND` | `conflict` | sale, debt payment from the personal account, class registration, certificate redemption | the client was deleted, merged with another client or is not on the server | Клієнта видалено або обʼєднано з іншим клієнтом. |
| `PLAN_NOT_FOUND` | `conflict` | sale, class registration, certificate redemption | the plan is not on the server; for a class registration — also a plan of another client | Абонемента немає на сервері. For a class registration also: «Створіть абонемент клієнту вручну та зареєструйте відвідування повторно.» |
| `PLAN_FROZEN` | `conflict` | class registration | the plan is frozen | Абонемент клієнта призупинено (відпустка). |
| `PLAN_EXHAUSTED` | `conflict` | class registration | the plan has no sessions left | Абонемент вичерпано. |
| `PLAN_EXPIRED` | `conflict` | class registration | the plan's validity ended by the operation time | Строк дії абонемента закінчився. |
| `PLAN_CLOSED` | `conflict` | class registration | the plan was ended before its end date or has no end date | Абонемент закрито. |
| `PLAN_NOT_ACTIVE` | `conflict` | class registration | the plan is not active and is not activated on the first visit | Абонемент неактивний. |
| `PLAN_NOT_FOR_CLASS` | `conflict` | class registration | the plan type does not match the workout type | Абонемент не діє для цього заняття. |
| `WORKOUT_NOT_FOUND` | `conflict` | class registration | the workout is not on the server | Заняття не знайдено. |
| `OCCURRENCE_CANCELLED` | `conflict` | class registration | the class is cancelled | Заняття скасовано. |
| `NO_FREE_SEATS` | `conflict` | class registration | no free seats: the seats are taken, including by bookings through the mobile app and by self check-in by QR code; a class without a set capacity is not limited | Заняття заповнене. |
| `PRODUCT_NOT_FOUND` | `conflict` | sale | a product of the sale is not on the server | Товар не знайдено. |
| `DEBT_ALREADY_PAID` | `conflict` | debt payment | the debt is paid off in full | Борг уже погашено. |
| `DEBT_OVERPAYMENT` | `conflict` | debt payment | the remaining debt is less than the payment | Сума оплати перевищує залишок боргу. |
| `DEBT_FORGIVEN` | `conflict` | debt payment | the debt is forgiven: deleted, or closed without the full payment | Борг списано. |
| `DEBT_NOT_FOUND` | `conflict` | debt payment | the debt is not on the server | Борг не знайдено. |
| `POSSIBLE_DUPLICATE` | `conflict` | new client | the studio already has a client with this phone | Можливий дублікат клієнта: клієнт із таким телефоном уже є. |
| `CARD_NUMBER_TAKEN` | `conflict` | new client | the manually set card number is registered to another client | Номер картки вже призначено іншому клієнту. |
| `balance_insufficient` | `conflict` | payment from the personal account | the personal account balance on the server is smaller than the payment | Недостатньо коштів на особовому рахунку. Нестача коштів: … грн. |
| `certificate_number_taken` | `conflict` | certificate sale | the server already has a certificate with this number | Номер сертифіката вже використовується. |
| `certificate_not_found` | `conflict` | certificate redemption | the certificate is not on the server | Сертифікат не знайдено. |
| `certificate_already_redeemed` | `conflict` | certificate redemption | the certificate is already redeemed | Сертифікат уже погашено. |
| `certificate_expired` | `conflict` | certificate redemption | the last day of the certificate's validity is earlier than the operation day in the studio time zone | Строк дії сертифіката закінчився. |
| `TRANSACTION_NOT_FOUND` | `conflict` | refund | the refunded sale is not on the server | Продаж не знайдено. |
| `refund_exceeds_remaining` | `conflict` | refund | the refund sum exceeds the available sum | Сума повернення перевищує доступну суму. Доступно до повернення: … грн. |
| `dependency_rejected` | `conflict` | an operation that depends on another queue operation | the operation this one depends on was not applied | Не виконано операцію, від якої залежить ця операція. |
| `OFFLINE_CLIENT_NOT_APPLIED` | `conflict` | an operation with a client created offline | the client creation got `conflict` or `rejected` | Не виконано створення клієнта, до якого належить операція. |
| `OFFLINE_SALE_NOT_APPLIED` | `conflict` | a class registration paid by an offline till sale | the sale got `conflict` or `rejected` | Не виконано продаж, яким оплачено операцію. |
| `OPERATION_INTERRUPTED` | `conflict` | a sale or refund started in the online admin; a queue operation stopped during the sync | the operation stopped after a step that cannot be undone | Offline till: state «Потребує уваги», note «Виконання операції перервано. Перевірте її результат.» The **Потребує уваги** tab and the notification: «Виконання операції перервано. Перевірте її результат.» Online admin, for an action started there: «Операцію «<вид>» від <дата й час> не завершено на сервері. Перевірте її результат перед повторним виконанням.» |

The actions an admin resolves an operation with on the **Потребує уваги** tab, and the refusals of these actions, are described in [Каса → Потребує уваги](/en/menu/pos#_398-needs-attention).

### Operation check refusals

The server checks the id, kind, version and time of each operation before applying it. An operation that fails the check gets `rejected`; the data does not change. The offline till shows the «Відхилено сервером» state and the reason in the **Примітка** (Note) column.

- An operation with the codes `INVALID_KIND`, `INVALID_VERSION`, `INVALID_OCCURRED_AT`, `OCCURRED_IN_FUTURE`, `OCCURRED_TOO_LONG_AGO` is stored as a refused offline till operation together with its content: it is shown on the [Каса → Потребує уваги](/en/menu/pos#_398-needs-attention) tab with the reason, and the admins get one notification about the operation. On the tab the operation can only be marked as reviewed.
- An operation without a kind is shown with the kind «Невідома операція». An operation without a valid time, or with a time outside the years 2000–9999, is shown with the time the server received it.
- If the content of a refused operation cannot be stored (for example, a text field holds a character with code 0), the operation is stored without its content: on the **Потребує уваги** tab it is shown with its time, kind, state, reason and user, like other refused operations, and it can only be marked as reviewed; the admins get one notification.
- If a refused operation cannot be stored, the offline till still gets the `rejected` result with its reason, and the next operations of the queue are synced; the operation is not shown on the **Потребує уваги** tab and no notification is created. A repeated delivery of this operation is checked and stored at once, without the `in_progress` result.
- Sending such an operation again returns the stored result; no second record and no second notification are created.
- An operation with the `INVALID_ID` code is not stored: without an id it cannot be recognised when sent again. An operation with the `IDEMPOTENCY_KEY_REUSED` code is not stored: its id belongs to another operation. These operations are not shown on the **Потребує уваги** tab and no notification is created; only the **Офлайн-операції** screen shows the reason.
- If the id of an operation with a check code already belongs to an applied or stored operation, the stored result of that operation is returned.

| Code | Condition | What the user sees |
|---|---|---|
| `INVALID_ID` | the operation id is not a UUID | Ідентифікатор операції некоректний. |
| `INVALID_KIND` | the operation kind is not set or is longer than 32 characters | Вид операції не вказано або він некоректний. |
| `INVALID_VERSION` | the operation version is not a whole number from 1 | Версія операції не підтримується. |
| `INVALID_OCCURRED_AT` | the operation time is not a date | Час операції не вказано або він некоректний. |
| `OCCURRED_IN_FUTURE` | the operation time is later than the server time by more than 5 minutes | Час операції пізніший за час сервера. |
| `OCCURRED_TOO_LONG_AGO` | the operation time is earlier than the server time by more than 30 days | Операцію виконано надто давно для синхронізації. |
| `IDEMPOTENCY_KEY_REUSED` | the operation id was already used for another operation | Ідентифікатор операції вже використано для іншої операції. |

### Operations waiting in the queue

An operation with these codes is not applied now and stays in the queue in the «Очікує синхронізації» state; the next queue operations wait for it. The operation is sent again at the next sync with no user action.

| Code | Condition |
|---|---|
| `OP_VERSION_UNSUPPORTED` | the operation version is above the one the server supports; the operation is applied after the server is updated |
| `OP_KIND_UNSUPPORTED` | the server does not apply this operation kind yet; the operation is applied after the server is updated |
| `RETRY` | the server could not apply the operation for the moment |
| `OPERATION_IN_PROGRESS` | another delivery is applying the operation with this id |

### Access and sync request refusals

| Code or condition | When | What the user sees |
|---|---|---|
| `DEVICE_TOKEN_USER_DISABLED` | enabling offline mode by a user without access to the studio | Ваш обліковий запис у цій студії не має доступу. Офлайн-режим недоступний. |
| the device access is invalid, revoked or expired | sync and data updates | the sync stops; the banner: «Увімкніть офлайн-режим на цьому компʼютері повторно в онлайн-адмінці» (see [Sync stop](#sync-stop)) |
| `DEVICE_MISMATCH` | data of a computer other than the one the access was issued for | the same as for invalid access |
| `INVALID_DEVICE_ID` | enabling offline mode: Device Handler passed an invalid computer id | offline mode is not enabled; the error window is shown |
| `DEVICE_TOKEN_NOT_FOUND`, `INVALID_DEVICE_TOKEN_ID` | revoking a device access that does not exist or is already revoked | the «Доступ пристрою відкликано» message is not shown; the device list refreshes |
| `INVALID_DEVICE_ID`, `INVALID_OPERATIONS` | the server does not accept the sync request from this offline till version | the sync stops, the operations stay in the queue; the banner: «Оновіть Device Handler, щоб операції передавались на сервер» |

### Refusals of online actions with an operation id

An online action with an operation id (see [One-time application of operations](#one-time-application-of-operations)) gets a refusal with a code; the action is not done, and the online admin shows the refusal window.

| Code | Condition |
|---|---|
| `INVALID_OPERATION_ID` | the operation id is not a UUID |
| `IDEMPOTENCY_KEY_REUSED` | the id was already used for another operation |
| `OPERATION_IN_PROGRESS` | another delivery is applying the operation with this id; retry later with the same id |
| `OPERATION_INTERRUPTED` | the operation stopped after a step that cannot be undone; it is not run again; an admin's review is needed |

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.9 Point of sale

> The **Point of sale** page is the cashier's main working area for reviewing transactions, managing cash on hand, and fiscal reports.

![](../../_media/pos-overview.png ':size=400x241')

## 3.9.1 Top bar

> Above the tables there is a top bar with the main actions and the cash status.

**Left — filter and fiscal reports:**

- **Period selector** — a date range picker. All tables (Transactions, Cash balance, Advanced report) are refiltered to the selected range.
- **X-report** ("X Звіт") — an instant fiscal report that does not close the shift (available while the shift is open).
- **Day report** ("Звіт за день") — a summary fiscal report for all transactions of the current calendar day, regardless of shift boundaries.

**Right — cash registers and operations:**

- **Cash accounts list** — each entry shows the account's name and current balance. The Default account is labeled **Main register** ("Основна каса") in this table (in the page's top bar the same account is called **Cash balance**, "Баланс готівки"); other accounts are labeled with their assigned name.
- **+ Add account** ("+ Додати акаунт") — creates a new named cash account (see [3.9.2 Cash accounts](#_392-cash-accounts)).
- **Cash operations** ("Операції з готівкою") — opens a modal window for deposit / withdrawal / expense / transfer (see [3.9.3 Cash operations](#_393-cash-operations)).

---

## 3.9.2 Cash accounts

> A studio can have **one Default account** and any number of **named accounts** (for example, "Конверт оренди" — "rent envelope", "Зарплати" — "payroll"). Physically the money sits in one register — accounts exist only to track what the funds are earmarked for.

**How it works:**

- The **Default account** is created automatically and cannot be deleted.
- **All sales (cash / card / bank transfer) always go to the Default account.** Named accounts do not accept sales directly.
- **Transferring to a named account** is done via **[Cash operations](#_393-cash-operations) → Transfer** ("Переказ") from the Default account.
- **Transfer back to the register (reverse transfer)** — each named account has a **⬅ Transfer to register** ("Перекласти в касу", left-arrow icon) button that transfers all or part of its balance back to the Default account.
- **Delete account** — the **🗑 Delete account** ("Видалити акаунт", trash-can icon) button. If the account has a balance, it is automatically transferred to the Default account before deletion.

**Creating a new account:**

1. Click **➕ Add account** ("Додати акаунт") in the accounts area.
2. Enter a name, then click **✓ Save** (checkmark icon) or **✗ Cancel** (cross icon).

---

## 3.9.3 Cash operations

> The **Cash operations** button opens a modal window with a choice of operation type.

![](../../_media/pos-cash-ops-modal.png ':size=300x181')

**Available operations:**

| Operation | Description |
|---|---|
| **Deposit** ("Внесення") | Adds cash to the Default account (at the start of a shift, etc.). |
| **Withdrawal** ("Інкасація") | Removes cash from the Default account (at the end of a shift, handover to the bank). |
| **Expense** ("Витрата") | Writes off funds from the Default account for a specific expense (optionally with a category). |
| **Transfer** ("Переказ") | Moves an amount from the Default account to one of the named accounts. |

**Fields:**

- **Amount** ("Сума") — required field.
- **Destination account** ("Акаунт призначення") — appears for **Transfer** (choose from the named accounts).
- **Comment** ("Коментар") — text field, added to the entry in Cash balance.

Saving an operation creates matching entries in the **Cash balance** tab with the categories `DEPOSIT`, `WITHDRAW`, `EXPENSE`, `TRANSFER_OUT` / `TRANSFER_IN`.

---

## 3.9.4 Transactions

> The **Transactions** ("Транзакції") tab shows all sales for the selected period.

![](../../_media/pos-transactions.png ':size=420x253')

**Columns:**

- **Date** — date and time of the transaction.
- **Paid** — amount in UAH; refunds are prefixed with `-`.
- **Payment method** — badge:
  - **Personal account** (if the transaction was paid from the client's personal account).
  - **Cash / Card / Bank transfer** — otherwise, according to the payment method.
- **Type** — badge **Sale** / **Refund**.
- **Client** — client's name (for a certificate sale this shows **Certificate**).
- **Created by** — name of the user who processed the transaction.
- **Payment status** — **Confirmed** / **Awaiting confirmation** (for bank-transfer payments under PRRO whose payment has not yet been approved). A bank-transfer payment made without internet has the **Awaiting confirmation** status after the sync regardless of the data the computer sent.
- **Receipt** ("Чек") — the **Show** ("Показати") button opens the transaction's receipt; the **Fiscalize** ("Фіскалізувати") button creates the fiscal receipt of a saved transaction without a receipt (see [Fiscalizing a transaction](#_3942-fiscalizing-a-transaction)).
- **Offline** ("Офлайн") — the mark of a transaction created during the sync of an operation made on a computer without internet: a sale, a debt payment, a personal-account payment, a certificate sale, a refund. The **Date** of such a transaction is the operation time on the computer. See [Sales sync](/en/pages/offline-mode#sales-sync) and [Personal account, certificates and refunds](/en/pages/offline-mode#personal-account-certificates-and-refunds).
- **Actions** (available while the shift is open):
  - **❌ Issue a refund** ("Зробити повернення", red x-in-circle icon) — opens the [refund modal window](#_3941-refunds).
  - **💵 Change payment method** ("Змінити метод оплати", banknote icon) — for correcting a cashier's mistake right after a sale. Disabled if the payment was made from the client's personal account.

### 3.9.4.1 Refunds

> The refund modal window allows:

- **Full refund** — refunds the entire transaction, returning all items to the client.
- **Partial refund** — choose specific items (plans / products) to refund.
- **Refund method** automatically matches the original payment method:
  - Cash → from the Default account;
  - Card → noted in the fiscal record;
  - Personal account → the amount is returned to the client's [personal account](/en/menu/clients#_3-2-11-personal-account).

> ⚠️ A refund **does not return a used session** to the membership. The class took place and the coach ran it, so the deduction stands — only the money comes back.

### 3.9.4.2 Fiscalizing a transaction

> The **Fiscalize** ("Фіскалізувати") button in the **Receipt** column creates the fiscal receipt of a saved transaction that has no receipt.

**Access:** the SuperAdmin, Admin and Manager roles.

**The button is shown when all conditions are met:**

- the transaction is a sale (type **Sale** or no type), a debt payment included; for a refund the button is not shown: the receipt of a refund made offline is created on the [Not fiscalized](#_397-not-fiscalized) tab;
- the payment is not from the personal account;
- the transaction has no fiscal receipt;
- the transaction does not have the state **No fiscalization needed**;
- the transaction does not have the status **Receipt sent, number unknown** (see below);
- the studio has an active fiscal integration (enabled and configured);
- the operation time of the transaction is not earlier than the time of the studio's first fiscalized sale (the earliest sale transaction with a fiscal receipt). If the studio has no fiscalized sale, the button is not shown. This condition applies only to the manual receipt; the automatic receipt of a sale or a debt payment does not check it. A transaction in the state **Awaiting fiscalization** or **Fiscalization error** is not limited by this condition.

**Execution:**

- After confirmation in the **Fiscalization** ("Фіскалізація") window, the server creates the receipt through an active fiscal integration. When the studio has several active fiscal integrations, choosing the **Fiscal register** ("Фіскальна каса") in the **Fiscalization** window is mandatory; until then the confirm button is disabled. A request without a chosen register creates the receipt through the first active fiscal integration, as the automatic receipt of a debt payment does. The transaction id is passed to the provider as the receipt id.
- The receipt amount is the sale amount less the refunds made before the receipt; the receipt lines are the sale lines less the refunded quantities. A sale refunded in full before the receipt gets no receipt and gets the state **No fiscalization needed**.
- Refunds included in the sale receipt amount get no receipt of their own and have the state **No fiscalization needed**; a request for their receipt is refused with `RECEIPT_NOT_REQUIRED`. A refund made after the sale receipt was created is fiscalized with a return receipt against the sale receipt.
- When the fiscal provider already holds a sale receipt created by an earlier attempt before the refunds were made, that receipt is stored. The refunds not included in its amount get the state **Awaiting fiscalization**, are listed on the [Not fiscalized](#_397-not-fiscalized) tab and are fiscalized with return receipts. No second sale receipt is created.
- When the provider does not report the amount of the sale receipt found, or that amount does not equal the sale amount less any number of the earliest refunds, all refunds of the sale without their own receipt get the state **Sale receipt check needed** ("Потребує перевірки чека продажу"). No return receipt is created for them; a request for it is refused with `REFUND_NEEDS_CHECK`. An administrator checks the sale receipt in the Checkbox cabinet and confirms whether it includes the refund: an included refund gets the state **No fiscalization needed**, a refund not included gets the state **Awaiting fiscalization** and is fiscalized with a return receipt.
  - Request: `POST /transactions/:id/fiscal-receipt/refund-check`, body `{ included }` (`true` — the sale receipt includes the refund, `false` — it does not). Response: `{ id, fiscalState }`. Error codes: 403 (the role is not SuperAdmin, Admin or Manager), 400 `REFUND_CHECK_ANSWER_REQUIRED` «Зазначте, чи враховано повернення в чеку продажу» (`included` not given), 409 `REFUND_CHECK_NOT_NEEDED` «Повернення не потребує перевірки чека продажу» (the refund does not have the state **Sale receipt check needed**).
- For the **Checkbox** integration a transaction in the state **Fiscalization error** is fiscalized only after the provider answers the request for the receipt with the transaction id: a receipt found is stored. When the request fails, `FISCAL_RESULT_UNKNOWN` is returned, no new receipt is created and the state of the transaction does not change.
- A sale refunded in full that awaits its receipt after the sync: for the **Checkbox** integration the server asks the provider for the receipt with the transaction id. A receipt found is stored, and the refunds not included in its amount get the state **Awaiting fiscalization**. When there is no receipt, the sale and its refunds get the state **No fiscalization needed**. When the request to the provider fails, `FISCAL_RESULT_UNKNOWN` is returned and the states do not change. For the **VchasnoKasa** integration a sale with the status **Receipt sent, number unknown** is not fiscalized until the missing receipt is confirmed (see **Status «Receipt sent, number unknown»** below); after the confirmation the sale and its refunds get the state **No fiscalization needed**.
- Before the receipt is created, the transaction is locked and the conditions are checked again. At most one receipt is created for a transaction: a repeated click or a simultaneous action of another user is refused with `RECEIPT_ALREADY_ISSUED`.
- For a **Checkbox** integration, before the receipt is created the server asks the provider for a receipt with the transaction id. When such a receipt exists and is fiscalized, it is saved on the transaction and no new receipt is created. When the request to the provider fails, the receipt is created. When the receipt with the transaction id has the status `ERROR` in Checkbox, the request is refused with `RECEIPT_REJECTED_AT_PROVIDER`: Checkbox does not accept another receipt with the same id. When the receipt did not get a fiscal number within the wait (15 s), the request is refused with `RECEIPT_PENDING_AT_PROVIDER`; a retry is allowed. For a **VchasnoKasa** integration this request is not made.
- For a **VchasnoKasa** integration, before the request to the provider the server saves a sent mark (`fiscalSentAt`) on the transaction in a separate write. The mark stays even when the later write of the receipt onto the transaction fails.
  - The provider answered with a refusal (an error text in the answer or HTTP 4xx other than 408) — the mark is removed, `FISCAL_PROVIDER_ERROR` is returned, a retry is allowed.
  - The request was not sent to the provider (the fiscal integration settings were not read or the receipt data was not built) — the mark is removed, `FISCAL_PROVIDER_ERROR` is returned, a retry is allowed.
  - No answer from the provider (timeout, HTTP 408, network error, HTTP 5xx) — the mark stays, `FISCAL_RESULT_UNKNOWN` is returned.
  - The receipt was created but not written onto the transaction — the mark stays.
- During a sale with a **VchasnoKasa** integration, when no answer to the receipt request comes from the provider (timeout, HTTP 408, network error, HTTP 5xx), the sale is saved without a receipt with the sent mark and has the status **Receipt sent, number unknown**. When the provider answered with a refusal or the request was not sent, the sale is saved without the mark. For a **Checkbox** integration the mark is not set. A refund receipt does not get the mark.
- The fiscal receipt of an online debt payment, created automatically after the payment is saved, is created the same way: with the transaction lock and the repeated check of the conditions. When the receipt was already created with the **Fiscalize** button, a second receipt is not created, and the other way round.
- Once created, the receipt is saved on the transaction, the **Fiscalization** column shows **Fiscalized**, and the receipt window opens.
- Request: `POST /transactions/:id/fiscal-receipt`, body `{ fiscalProviderId }` (the id of the chosen fiscal register; optional: without it the receipt is created through the first active fiscal integration). Response: the receipt data in the same format as `GET /transactions/:id/receipt`.

**Status «Receipt sent, number unknown»** ("Чек надіслано, номер невідомий"):

- The transaction has a sent mark and no fiscal receipt. The **Fiscalization** column shows the badge **Receipt sent, number unknown**; the **Fiscalize** button is not shown.
- A repeated receipt for such a transaction is not allowed: the server returns `RECEIPT_SENT_NUMBER_UNKNOWN`, no request is made to the provider. Checking for the receipt in the Vchasno.Kasa cabinet is mandatory.
- The **Confirm the receipt is missing** ("Підтвердити відсутність чека") button in the **Receipt** column (the SuperAdmin and Admin roles), after confirmation in the **Missing fiscal receipt** ("Відсутність фіскального чека") window, removes the mark. After that the **Fiscalize** button is shown again under the conditions above.
- Confirming a missing receipt is not allowed when the receipt exists in the Vchasno.Kasa cabinet: a repeated receipt gives a second fiscal receipt.
- Request: `POST /transactions/:id/fiscal-receipt/not-issued`. Response: `{ id, fiscalSentAt }`. For a transaction without the mark the request changes nothing. Error codes: 403 (the role is not SuperAdmin or Admin), `TRANSACTION_NOT_FOUND`, `TRANSACTION_NOT_FISCAL_KIND`, `RECEIPT_ALREADY_ISSUED`.

**Error codes:**

When several conditions are not met, the code of the first of them in the order of the table rows is returned.

| HTTP | Code | Message | Condition |
|---|---|---|---|
| 403 | — | — | the user's role is not SuperAdmin, Admin or Manager |
| 404 | `TRANSACTION_NOT_FOUND` | «Транзакцію не знайдено» | the transaction does not exist |
| 400 | `TRANSACTION_NOT_FISCAL_KIND` | «Для цієї транзакції фіскальний чек не створюється» | a personal-account payment, or a refund without a link to its sale |
| 409 | `RECEIPT_ALREADY_ISSUED` | «Фіскальний чек для цієї транзакції вже створено» | the transaction already has a fiscal receipt |
| 409 | `RECEIPT_NOT_REQUIRED` | «Транзакція не потребує фіскалізації: продаж повернено до створення чека» | the transaction has the state **No fiscalization needed** |
| 409 | `REFUND_NEEDS_CHECK` | «Не визначено, чи враховано це повернення в чеку продажу. Перевірте чек продажу в кабінеті Checkbox і підтвердьте, чи враховано в ньому повернення» | the refund has the state **Sale receipt check needed** |
| 400 | `FISCALIZATION_NOT_ENABLED` | «Фіскалізацію не налаштовано» | the studio has no active fiscal integration |
| 409 | `SALE_NOT_FISCALIZED` | «Продаж, до якого виконано повернення, ще не фіскалізовано. Спочатку фіскалізуйте продаж» | a refund whose sale has no fiscal receipt |
| 400 | `FISCAL_CARD_NOT_ACTIVE` | «Обрану фіскальну касу не підключено або вимкнено» | the chosen fiscal register is not an active fiscal integration of the studio |
| 400 | `FISCAL_CARD_REQUIRED` | «Оберіть фіскальну касу» | group fiscalization on the [Not fiscalized](#_397-not-fiscalized) tab: the studio has several active fiscal integrations and none is chosen |
| 400 | `TRANSACTION_BEFORE_FIRST_FISCAL_SALE` | «Фіскальний чек вручну створюється лише для продажів, здійснених не раніше першого фіскалізованого продажу студії» | the operation time of the transaction is earlier than the time of the studio's first fiscalized sale, or the studio has no fiscalized sale |
| 409 | `RECEIPT_SENT_NUMBER_UNKNOWN` | «Чек для цієї транзакції вже надіслано до фіскального сервісу, номер чека невідомий. Перевірте наявність чека в кабінеті Вчасно.Каса» | the transaction has the status **Receipt sent, number unknown** |
| 409 | `RECEIPT_REJECTED_AT_PROVIDER` | «Фіскальний сервіс відхилив чек цієї транзакції. Повторне створення чека для неї неможливе: зверніться до служби підтримки Checkbox» | the receipt with the transaction id has the status `ERROR` in Checkbox |
| 409 | `RECEIPT_PENDING_AT_PROVIDER` | «Чек цієї транзакції ще обробляється фіскальним сервісом. Повторіть спробу пізніше» | the receipt with the transaction id in Checkbox did not get a fiscal number within 15 s |
| 502 | `FISCAL_PROVIDER_ERROR` | «Фіскальний сервіс повернув помилку: <текст провайдера>. Чек не створено» | the fiscal provider returned an error; the transaction stays without a receipt |
| 502 | `FISCAL_RESULT_UNKNOWN` | «Не вдалося перевірити наявність чека у фіскальному сервісі. Повторіть спробу пізніше» | Checkbox: a sale refunded in full, or a transaction in the state **Fiscalization error**; the request for the receipt with the transaction id to the provider failed |
| 502 | `FISCAL_RESULT_UNKNOWN` | «Фіскальний сервіс не підтвердив створення чека. Чек міг бути створений: перевірте його наявність у кабінеті Вчасно.Каса» | VchasnoKasa: no answer from the provider; the transaction gets the status **Receipt sent, number unknown** |

---

## 3.9.5 Cash balance

> The **Cash balance** ("Баланс готівки") tab shows all fund movements across all accounts.

![](../../_media/pos-cash-balance.png ':size=420x253')

**Columns:**

- **Date / time**
- **Account** — Default or the named account's name
- **Type** — DEPOSIT / WITHDRAW / EXPENSE / TRANSFER_OUT / TRANSFER_IN / RESET
- **Amount** (signed: `+` for an inflow, `–` for a write-off)
- **Balance** — after the operation
- **Created by** — cashier's name
- **Comment**

All movements are sorted by date (descending by default).

---

## 3.9.6 Advanced report

> The **Advanced report** ("Розширений Звіт") tab is a detailed financial report for the selected period, grouped by payment method.

![](../../_media/pos-advanced-report.png ':size=420x253')

**Report sections:**

- **Cash** — table of transactions paid in cash. Columns: Time, Client, Type (sale/refund), Plans (names/count), Products (names/count), Amount.
- **Card** — the same, for card payments.
- **Bank transfer** — the same, for bank-transfer payments.
- **Balance operations** — movements across [cash accounts](#_392-cash-accounts): Time, Operation type (DEPOSIT/WITHDRAW/EXPENSE/TRANSFER_IN/TRANSFER_OUT/RESET), Account, Amount, Comment.

Each section has its own subtotal (sum of the "Amount" column).

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

---

## 3.9.7 Not fiscalized

> The **Not fiscalized** ("Не фіскалізовано") tab shows the sales, debt payments and refunds made in [offline mode](/en/pages/offline-mode#fiscalization-after-the-sync) that wait for a fiscal receipt after the sync. The tab is shown when the studio has an active fiscal integration; the tab name carries the number of such operations.

**Columns:**

- **Operation time** — the operation time on the computer in the studio time zone.
- **Type** — **Sale** or **Refund**.
- **Client** — the client's name.
- **Receipt amount** — for a sale: the sale amount less the refunds made before the receipt; for a refund: the refund amount.
- **Payment method** — the actual payment method of the transaction. A sale paid in parts shows one row per payment; each payment gets its own receipt for its amount with its payment method.
- **Document** — the number of the non-fiscal document the offline till issued.
- **State** — **Awaiting fiscalization** ("Очікує фіскалізації"), **Fiscalization error** ("Помилка фіскалізації"), **Fiscalization result unknown** ("Результат фіскалізації невідомий") or **Sale receipt check needed** ("Потребує перевірки чека продажу"); under the error badge, the error text of the fiscal provider. The state `error` without a provider error text is shown with the neutral badge **Fiscalization result unknown**.
- For a refund in the state **Sale receipt check needed**, the **Fiscalize** button is not shown; users with the role SuperAdmin, Admin or Manager see the buttons **Included in the sale receipt** ("Враховано в чеку продажу") and **Not included in the sale receipt** ("Не враховано в чеку продажу"). Each button opens the confirmation window «Перевірка чека продажу» with the buttons **Confirm** ("Підтвердити") and **Cancel** ("Скасувати"). After confirmation the request `POST /transactions/:id/fiscal-receipt/refund-check` is made (see [Fiscalizing a transaction](#_3942-fiscalizing-a-transaction)): a refund included in the sale receipt gets the state **No fiscalization needed** and leaves the tab; a refund not included gets the state **Awaiting fiscalization** and is fiscalized with a return receipt. The message «Рішення щодо повернення збережено» (The decision on the refund is saved) is shown.

**Fiscalization:**

- The **Fiscalize** button in a row creates the receipt of that operation. The **Fiscalize selected** ("Фіскалізувати вибрані") button creates the receipts of the operations ticked in the first column one after another: sales first, then refunds. Ticked refunds in the state **Sale receipt check needed** are not included in these receipts and are not counted on the button. At most 50 operations are chosen at once.
- When the studio has several active fiscal integrations, choosing the **Fiscal register** above the table is mandatory; until then the buttons are inactive. A refund is fiscalized through the fiscal register of its sale's receipt regardless of the choice.
- The receipt is created in the current shift of the fiscal register, also for operations of a closed shift. The receipt carries the line «Продаж в офлайн-режимі <date and time>, документ <number>» (for a refund, «Повернення в офлайн-режимі …»).
- Afterwards the number of receipts created and the number not created with the text of the first error are shown. When processing the selected operations takes too long, some operations are not processed: the number of unprocessed operations is shown, they stay on the tab and are fiscalized by running again. An operation with a created receipt leaves the tab and has the badge **Fiscalized** in the **Fiscalization** column of the **Transactions** tab.
- An operation for which the fiscal provider returned an error stays on the tab in the state **Fiscalization error** with the error text. A retry does not create a second receipt (see [Fiscalizing a transaction](#_3942-fiscalizing-a-transaction)).
- A refund is fiscalized only after its sale. For a refund whose sale awaits its receipt (the state **Awaiting fiscalization** or **Fiscalization error**), the sale is fiscalized first under the rules of [fiscalizing a transaction](#_3942-fiscalizing-a-transaction). When the refund needs no receipt after that, it gets the state **No fiscalization needed** and no refund receipt is created. A refusal of the sale receipt is returned as the refusal for the refund. For a refund whose sale has no receipt and does not await one, the request is refused with `SALE_NOT_FISCALIZED`.
- The conditions and error codes for each operation are the same as for [fiscalizing a transaction](#_3942-fiscalizing-a-transaction).

**The «Fiscalization» column of the «Transactions» tab** shows for operations made offline their state: **Awaiting fiscalization**, **Fiscalization error**, **Fiscalization result unknown**, **Sale receipt check needed**, **No fiscalization needed** ("Не потребує фіскалізації") or **Fiscalized**.

**Requests:**

- `GET /transactions/awaiting-receipt` — the operations waiting for a receipt, earliest first: `data` (transactions with the fields `fiscalState`, `fiscalError`, `receiptAmount`) and `fiscalCards` (the active fiscal registers: `id`, `label`, `type`).
- `POST /transactions/fiscal-receipts`, body `{ transactionIds, fiscalProviderId }`. Response: an array of `{ id, ok, code?, message? }`, one item per operation; an operation whose processing was not started has `ok: false` and the code `RECEIPT_NOT_ATTEMPTED` «Транзакцію не оброблено: вичерпано час обробки. Повторіть фіскалізацію». An empty list or more than 50 operations is refused with 400 `RECEIPT_GROUP_SIZE` «Оберіть від 1 до 50 транзакцій»; no receipt is created.

## 3.9.8 Needs attention

> The **Needs attention** ("Потребує уваги") tab shows the operations that need an administrator's action after the sync of the [offline till](/en/pages/offline-mode#needs-attention). The tab is shown in the online admin; the offline till has no such tab.

**Fiscal receipts** ("Фіскальні чеки"; the block is shown when the studio has an active fiscal integration):

- The operations of the [Not fiscalized](#_397-not-fiscalized) tab in the state **Sale receipt check needed**, **Fiscalization error** or **Fiscalization result unknown**. Operations in the state **Awaiting fiscalization** are not shown in the block.
- The columns, buttons and fiscal register choice are the same as on the [Not fiscalized](#_397-not-fiscalized) tab. The buttons **Included in the sale receipt** and **Not included in the sale receipt** are shown to users with the role SuperAdmin, Admin or Manager.
- When there are no such operations, the text «Немає фіскальних чеків, що потребують уваги» (No fiscal receipts need attention) is shown.

**Awaiting confirmation** ("Очікують підтвердження"):

- Payments by account taken by the offline till that wait for the confirmation that the money arrived, earliest first. Columns: **Operation time**, **Client**, **Amount**, **Document**.
- The **Confirm** ("Підтвердити") button opens the window «Підтвердження оплати» (Payment confirmation) with the buttons **Confirm** and **Cancel**. After confirmation the transaction is confirmed by the same request as the confirmation button of the **Transactions** tab (`PATCH /transactions/:id`), leaves the list, and the message «Оплату підтверджено» (Payment confirmed) is shown.
- When there are no such payments, the text «Немає оплат, що очікують підтвердження» (No payments await confirmation) is shown.

**Offline till operations** ("Операції офлайн-каси"):

- The offline till operations the server did not apply during the sync (result `conflict` or `rejected`) or applied with a mark (`price_changed`, `total_mismatch`, `negative_stock`), newest first; at most 200 operations. Online admin operations with an operation id are not listed.
- Columns: **Time** ("Час"; the operation time at the offline till in the studio time zone), **Operation** ("Операція"), **State** ("Стан"), **Reason** ("Причина"), **User** ("Користувач"; the user the operation was made under at the offline till), **Actions** ("Дії"). The **Refresh** ("Оновити") button reads the list again.

| State | Meaning |
|---|---|
| Не виконано: конфлікт (Not applied: conflict) | result `conflict`: the operation was not applied, it contradicts changes made on the server |
| Відхилено сервером (Refused by the server) | result `rejected`: the operation was not applied |
| Виконано з розбіжністю (Applied with a difference) | result `applied` with a mark: the operation was applied, the result differs from what the offline till showed |

- The **Reason** column holds the description of the reason code (see [Sales sync codes](/en/pages/offline-mode#sales-sync-codes), [Checks during the sync](/en/pages/offline-mode#checks-during-the-sync), [Personal account, certificate and refund sync codes](/en/pages/offline-mode#personal-account-certificate-and-refund-sync-codes)), the amounts from `details` («Нестача коштів: <amount> грн.» — shortfall, «Доступно до повернення: <amount> грн.» — available for refund) and the description of each mark:

| Mark | Text |
|---|---|
| `negative_stock` | Залишок товару на складі відʼємний. (The product stock is below zero.) |
| `price_changed` | Ціна відрізняється від ціни в каталозі. (The price differs from the catalogue price.) |
| `total_mismatch` | Сума операції відрізняється від суми на сервері. (The operation total differs from the server total.) |

- A code without a description is shown as «Операцію не виконано (код <code>).».
- A class registration with the code `PLAN_NOT_FOUND` also carries the text «Створіть абонемент клієнту вручну та зареєструйте відвідування повторно.» (Create the plan for the client by hand and register the visit again.)

**Resolving actions** (the **Actions** column):

| Operation and reason | Buttons |
|---|---|
| Class registration, `NO_FREE_SEATS` (class full) | **Register over capacity** ("Зареєструвати понад місткість"), **Take the registration off** ("Зняти реєстрацію") |
| Class registration, plan used up, expired, suspended, not active, closed, not valid for the class or missing (`PLAN_*`) | **Take from another plan** ("Списати з іншого абонемента"), **Record as debt** ("Оформити борг"), **Take the registration off** |
| New client, `POSSIBLE_DUPLICATE` | **Merge with a client** ("Обʼєднати з клієнтом"), **Keep as a separate client** ("Залишити окремим клієнтом") |
| Sale or debt payment from the personal account, `balance_insufficient` | **Record the shortfall as debt** ("Оформити нестачу боргом"), **Refuse the operation** ("Відхилити операцію") |
| Certificate redeem, `certificate_already_redeemed` or `certificate_expired` | **Record a plan sale** ("Оформити продаж абонемента"), **Record as debt**, **Refuse the operation** |
| Refund, `refund_exceeds_remaining` | **Refund the available amount** ("Повернути доступну суму"), **Refuse the operation** |
| Any operation, `dependency_rejected`, `OFFLINE_CLIENT_NOT_APPLIED` or `OFFLINE_SALE_NOT_APPLIED` | **Apply again** ("Виконати повторно"), **Refuse the operation** |
| Operation applied with the mark `price_changed` | **Confirm the price** ("Підтвердити ціну") |

- The **Reviewed** ("Переглянуто") button is shown in every row. Its confirmation window for an operation not applied says «Операцію «<operation>» від <date and time> не виконано на сервері. Після позначки «Переглянуто» вона залишиться невиконаною й перейде до списку переглянутих.» (the operation stays not applied and moves to the reviewed list); for an operation applied with a mark — «Операцію «<operation>» від <date and time> буде позначено як переглянуту й перенесено до списку переглянутих.».
- Every action without a choice opens a confirmation window with the buttons **Confirm** and **Cancel**. **Take from another plan** (choice of a client plan with classes left, in the state Active or New), **Merge with a client** (choice of a studio client with the same phone) and **Record a plan sale** (choice of the payment method: cash or card) open a choice window with the buttons **Cancel** and **Confirm**; **Confirm** is inactive until a choice is made.
- The actions that apply the operation (**Register over capacity**, **Take from another plan**, **Record as debt**, **Record a plan sale**, **Record the shortfall as debt**, **Refund the available amount**, **Keep as a separate client**, **Apply again**) apply it the same way as the offline till sync, with the same checks, under the same operation id:
  - **Register over capacity** — the registration without the free seat check.
  - **Take from another plan** — the class is taken from the chosen client plan.
  - **Record as debt** for a registration — the registration with the payment status «Не оплачено» (not paid) without taking a class from a plan, and the client debt «Борг за тренування: <name>» for the price of the plan of the class category (0 UAH when the category has no plan).
  - **Record a plan sale** and **Record as debt** for a certificate — a sale of the certificate's plans to the client at catalogue prices, dated at the moment of resolving: paid by the chosen method or wholly on debt. The certificate is not redeemed.
  - **Record the shortfall as debt** — the personal account pays the balance it holds at the moment of resolving, the rest of the sale is recorded as debt; a debt payment pays the balance held, the rest of the debt stays. The personal account balance does not go below zero. When the account holds nothing, a debt payment is refused with the code `OFFLINE_RESOLVE_NOTHING_TO_APPLY`.
  - **Refund the available amount** — a refund of the amount still refundable; the refund never exceeds the sale amount less earlier refunds.
  - **Keep as a separate client** — the client is created without the phone check.
  - **Apply again** — the operation is applied unchanged, after the operation it depends on is resolved.
- **Merge with a client** — no new client is created; the offline till operations that name this client apply to the chosen studio client (those already refused — through **Apply again**).
- **Confirm the price**, **Take the registration off**, **Refuse the operation** and **Reviewed** change no data. Money given out of the till in an offline shift stays in that shift's report.
- After a successful action the message «Рішення щодо операції збережено» (The decision on the operation is saved) is shown and the operation moves to the **Reviewed operations** ("Переглянуті операції") list.
- When the operation cannot be applied the chosen way (for example, the chosen plan is suspended), the server's refusal is shown; the operation stays on the list with the new reason.
- When another user is resolving the operation at the same moment, the request is refused with 409 `OFFLINE_ATTENTION_BEING_RESOLVED` «Цю операцію саме зараз вирішує інший користувач». An action the operation does not offer, or resolving it again, is refused with 409 `OFFLINE_ATTENTION_NOT_RESOLVABLE` «Операцію вже вирішено або її не можна вирішити в такий спосіб».

**Reviewed operations:**

- Operations marked **Reviewed** or resolved, last resolved first; at most 200. Columns: **Time**, **Operation**, **State**, **Reason**, **Decision** ("Рішення"; the action name and the user who took it).

**Notifications:**

- For every offline till operation the server did not apply, one notification is created for the administrators: «Офлайн-операцію «<operation>» від <date and time> не виконано. <reason> Перегляньте розділ Каса → Потребує уваги.» The date and time are in the studio time zone. Syncing the same operation again creates no second notification.

**Requests:**

- `GET /offline/attention` — open operations, newest first; `GET /offline/attention?reviewed=true` — reviewed ones. Fields: `id`, `kind`, `deviceId`, `status`, `operationAt`, `performedBy`, `performedByName`, `flags`, `error` (`code`, `message`, `details`), `reasons` (the texts of the **Reason** column), `actions` (available actions: `declined`, `price_confirmed`, `over_capacity`, `other_plan`, `as_debt`, `sell_plan`, `shortfall_debt`, `refund_available`, `merge`, `keep_separate`, `retry`), `options` (`plans` — plans for `other_plan`; `clients` — clients for `merge`), `reviewedAt`, `reviewedBy`, `resolution`.
- `POST /offline/attention/:id/resolve`, body `{ action, clientPlanId?, clientId?, paymentMethod? }`; `action` is one of `actions` or `reviewed`. `clientPlanId` is required for `other_plan`, `clientId` for `merge`, `paymentMethod` (`0` — cash, `2` — card) for `sell_plan`; without them the request is refused with 400 `INVALID_RESOLUTION`. Response: `{ id, resolution }`.
- `GET /offline/attention/awaiting-approval` — payments by account of the offline till that wait for confirmation.
- Roles: SuperAdmin, Admin, Manager; any other role is refused with 403.

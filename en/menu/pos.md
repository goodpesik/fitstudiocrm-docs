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
- **Offline** ("Офлайн") — the mark of a transaction created during the sync of an operation made on a computer without internet. The **Date** of such a transaction is the operation time on the computer. See [Sales sync](/en/pages/offline-mode#sales-sync).
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

- the transaction is a sale (type **Sale** or no type), an online debt payment included; for a refund the button is not shown, and a refund receipt is not created manually;
- the payment is not from the personal account;
- the transaction was created online, not by the sync of an operation made on a computer without internet;
- the transaction has no fiscal receipt;
- the studio has an active fiscal integration (enabled and configured);
- the operation time of the transaction is not earlier than the time of the studio's first fiscalized sale (the earliest sale transaction with a fiscal receipt). If the studio has no fiscalized sale, the button is not shown. This condition applies only to the manual receipt; the automatic receipt of a sale or a debt payment does not check it.

**Execution:**

- After confirmation in the **Fiscalization** ("Фіскалізація") window, the server creates the receipt through the first active fiscal integration, as during a sale. The transaction id is passed to the provider as the receipt id.
- Before the receipt is created, the transaction is locked and the conditions are checked again. At most one receipt is created for a transaction: a repeated click or a simultaneous action of another user is refused with `RECEIPT_ALREADY_ISSUED`.
- For a **Checkbox** integration, before the receipt is created the server asks the provider for a receipt with the transaction id. When such a receipt exists, it is saved on the transaction and no new receipt is created. When the request to the provider fails, the receipt is created. For a **VchasnoKasa** integration this request is not made.
- The fiscal receipt of an online debt payment, created automatically after the payment is saved, is created the same way: with the transaction lock and the repeated check of the conditions. When the receipt was already created with the **Fiscalize** button, a second receipt is not created, and the other way round.
- Once created, the receipt is saved on the transaction, the **Fiscalization** column shows **Fiscalized**, and the receipt window opens.
- Request: `POST /transactions/:id/fiscal-receipt`. Response: the receipt data in the same format as `GET /transactions/:id/receipt`.

**Error codes:**

When several conditions are not met, the code of the first of them in the order of the table rows is returned.

| HTTP | Code | Message | Condition |
|---|---|---|---|
| 403 | — | — | the user's role is not SuperAdmin, Admin or Manager |
| 404 | `TRANSACTION_NOT_FOUND` | «Транзакцію не знайдено» | the transaction does not exist |
| 400 | `TRANSACTION_NOT_FISCAL_KIND` | «Для цієї транзакції фіскальний чек не створюється» | a refund, a personal-account payment, or a transaction created by the sync of an offline operation |
| 409 | `RECEIPT_ALREADY_ISSUED` | «Фіскальний чек для цієї транзакції вже створено» | the transaction already has a fiscal receipt |
| 400 | `FISCALIZATION_NOT_ENABLED` | «Фіскалізацію не налаштовано» | the studio has no active fiscal integration |
| 400 | `TRANSACTION_BEFORE_FIRST_FISCAL_SALE` | «Фіскальний чек вручну створюється лише для продажів, здійснених не раніше першого фіскалізованого продажу студії» | the operation time of the transaction is earlier than the time of the studio's first fiscalized sale, or the studio has no fiscalized sale |
| 502 | `FISCAL_PROVIDER_ERROR` | «Фіскальний сервіс повернув помилку. Чек не створено» | the fiscal provider returned an error; the transaction stays without a receipt |

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

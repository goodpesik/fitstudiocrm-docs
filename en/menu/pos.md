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
- **Payment status** — **Confirmed** / **Awaiting confirmation** (for bank-transfer payments under PRRO whose payment has not yet been approved).
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

> ⚠️ If a session from the plan has already been used, the refund creates a compensating entry in the plan's [history](/en/menu/clients#_3-2-5-history).

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

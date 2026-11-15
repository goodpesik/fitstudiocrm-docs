<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.9 Point of sale

> The **Point of sale** page is the cashier's main working area for reviewing transactions, managing cash on hand, and fiscal reports.

![](../../_media/pos-overview.png ':size=400x241')

## 3.9.1 Top bar

> Above the tables is the top bar with the main actions and the cash status.

**Left — filter and reports:**

- **Period selection** — a date range picker. The **Transactions**, **Cash balance** and **Advanced report** tables show data for the selected range.
- **X Звіт** (X report) — the **X звіт** report built from the transactions of the current shift, without closing it.
- **Звіт за день** (day report) — the **Звіт за день** report built from all transactions of the first day of the selected period, regardless of shift boundaries.

The **X Звіт** and **Звіт за день** buttons are shown only while a shift is open. The report contains the **Одержано по формах оплати** (received by payment form) block: **Оплата картою** (card), **Готівка** (cash), **Оплата на рахунок** (bank transfer), **Повернення** (refunds), **Загальний оборот** (total turnover), **Кількість чеків** (number of receipts).

**Right — cash accounts and operations:**

- **List of cash accounts** — each shows its name and current balance. The main account is labelled **Баланс готівки** (cash balance); in the [Cash balance](#_395-cash-balance) table and in the [Advanced report](#_396-advanced-report) it is shown as **Основна каса** (main cash desk), the others by their given names.
- **Add account** ("Додати акаунт", "+" icon) — creates a new named cash account (see [3.9.2 Cash accounts](#_392-cash-accounts)).
- **Cash operations** ("Операції з готівкою") — opens a modal window for deposit, collection, expense and transfer (see [3.9.3 Cash operations](#_393-cash-operations)).

---

## 3.9.2 Cash accounts

> A studio has **one main account** (**Основна каса**) and may have any number of **named accounts** (for example, "Rent envelope", "Salaries"). The accounts record the purpose of funds held in one physical cash desk.

**Rules:**

- The **main account** is created automatically; it cannot be deleted.
- **All cash sales and refunds are recorded on the main account.** Named accounts do not accept sales directly.
- **Transfer to a named account** — via **[Cash operations](#_393-cash-operations) → Transfer** from the main account.
- **Move to cash desk** ("Перекласти в касу") — each named account has the **Move to cash desk** button (arrow icon), which opens the window "Перекласти в касу з «<name>»" with the fields **Введіть суму переказу** (transfer amount) and **Коментар** (optional) and the **Відміна** / **Перекласти** buttons. The amount is transferred to the main account.
- **Delete account** ("Видалити акаунт", trash-can icon). After confirmation ("Видалити акаунт "<name>"? Якщо є баланс — він буде переведений до Основної каси.") the account balance is transferred to the main account and the account is deleted.

**Creating a new account:**

1. Click **Add account** in the accounts area.
2. Enter the **Account name** ("Назва акаунту"), click **Save** (check-mark icon) or **Cancel** (cross icon).

---

## 3.9.3 Cash operations

> The **Cash operations** button opens the modal window of the same name with a choice of operation type.

![](../../_media/pos-cash-ops-modal.png ':size=300x181')

**Available operations:**

| Operation | Description | Amount field |
|---|---|---|
| **Deposit** ("Внесення") | Adds cash to the main account. The **Скинути баланс** (reset balance) toggle sets a new cash balance instead of adding (operation "Скидання балансу"). | "Введіть суму яку треба додати до поточного балансу" / "Введіть новий баланс готівки" |
| **Collection** ("Інкасація") | Takes cash out of the main account. | "Введіть суму інкасації" |
| **Expense** ("Витрата") | Writes off from the main account for an expense. | "Введіть суму витрати" |
| **Transfer** ("Переказ") | Moves an amount from the main account to one of the named accounts (the **Оберіть акаунт** field). | "Введіть суму переказу" |

**Fields:** the amount (an integer, required) and **Comment** ("Коментар", added to the **Cash balance** record). Buttons: **Відміна** (cancel), **Зберегти** (save).

**Checks:**

- "Баланс не може бути меньшим за 0" (the balance cannot be below 0);
- "Вказана сума інкасації більша за поточний баланс" (collection exceeds the balance);
- "Сума переказу більша за поточний баланс" (transfer exceeds the balance);
- "Оберіть акаунт" (choose an account) — for a transfer without a selected account.

Saving creates a record on the **Cash balance** tab with the matching type: **Внесення**, **Інкасація**, **Витрата**, **Переказ (вихід)** / **Переказ (вхід)**, **Скидання балансу**.

---

## 3.9.4 Transactions

> The **Transactions** ("Транзакції") tab shows all register transactions for the selected period. The table is paginated (10, 20 or 50 rows, 50 by default).

![](../../_media/pos-transactions.png ':size=420x253')

**Columns:**

| Column | Content |
|---|---|
| **Date** | Date and time of the transaction. A debt payment has the **Оплата боргу** (debt payment) badge. |
| **Paid** ("Сплачено") | Amount in UAH; refunds have the `-` prefix. |
| **Discount** ("Знижка") | The discount applied to the transaction. |
| **Payment method** | **Особовий рахунок** (personal account) if paid from the client's account; otherwise **Готівка** / **Картка** / **Безготівкова** (cash / card / bank transfer). |
| **Type** | **Продаж** (sale) / **Повернення** (refund) / **Поповнення особового рахунку** (personal account top-up). |
| **Client** | The client's surname and first name; for a certificate sale — **Сертифікат**. |
| **Created by** | The user who made the transaction. |
| **Payment status** | **Підтверджено** (confirmed) or, for a bank transfer not yet confirmed by the studio, **Очікує на підтвердження** (awaiting confirmation) with the **Підтвердити** (confirm) button. |
| **Plans** ("Абонементи") | Names of the sold plans or "--". |
| **Products** ("Товари") | Names of the sold products or "--". |
| **Receipt** ("Чек") | The **Показати** (show) button — opens the [receipt window](#_3943-receipt). |
| **Fiscalization** ("Фіскалізація") | Two badges: **Еквайрінг** / **Без еквайрінгу** (whether the payment went through a payment terminal) and **Фіскалізовано** / **Не фіскалізовано** (fiscalized / not fiscalized). |
| **Status** | **Повне повернення** (full refund) / **Часткове повернення** (partial refund) and the actions on the sale. |

**Actions** (in the **Status** column, for sales without a full refund, only while a shift is open):

- **Make a refund** ("Зробити повернення") — opens the [refund modal window](#_3941-refunds). Not available for a personal account top-up.
- **Change payment method** ("Змінити метод оплати") — opens the **Замінити метод оплати** window. On replacement the system automatically refunds the current transaction and creates a new one with the new payment method (buttons **Закрити** / **Замінити**). Disabled for payments from the personal account and for personal account top-ups.

### 3.9.4.1 Refunds

> The **Refund** ("Повернення") modal window holds a table of the transaction items with the columns **Name**, **Quantity**, **Refund** ("Повернути").

- Items to refund are marked with the **Refund** toggle; the quantity of each item is set within the sold quantity.
- Refunding all items is a **full** refund, some of them a **partial** one. After a partial refund the remaining items can be refunded later.
- The discount field (**Знижка (сума знижки)**, or **Знижка (%)** with the **Відсотки %** toggle) reduces the refund amount.
- **До повернення** — the total to refund.
- The **Підтверджую повернення** (I confirm the refund) toggle is required.
- The **Повернути кошти** (refund money) button is disabled when the refund amount is 0, the confirmation toggle is off, or the refund amount exceeds the main account balance (message "Недостатньо коштів в касі", not enough cash); the last condition does not apply to transactions paid from the personal account.
- Refunding a transaction paid from the personal account credits the amount to the client's [personal account](/en/menu/clients#_3-2-11-personal-account).
- Refunding a sold product increases its stock.

> ⚠️ A money refund **does not return the deducted session** to the plan: the deduction for the session that took place remains, only the money is returned.

### 3.9.4.2 Card payment

> A payment by the **Card** method (in a sale, registration, debt payment) is processed as follows:

- If no payment terminal is connected on this device, the payment is recorded without a terminal; in the **Fiscalization** column the transaction has the **Без еквайрінгу** badge.
- If a terminal is connected, the **Оплата** (payment) window opens: the choice of **Термінал** and **Мерчант** (terminal and merchant, when there are several) and the **Оплатити карткою** (pay by card) button, then "Виконуйте інструкції на терміналі…" (follow the terminal instructions) with the amount, and after success "Оплату проведено" (payment completed).
- If the terminal returns an error, the **Повторити** (retry) and **Провести вручну** (record manually) buttons are available. **Провести вручну** records the card payment without terminal data.

### 3.9.4.3 Receipt

> The **Показати** button in the **Receipt** column opens the receipt window titled **Фіскальний чек** (fiscal receipt) or **Товарний чек (не фіскальний)** (sales receipt, non-fiscal).

- The window holds the receipt text (when available), the badges **Фіскалізовано** / **Не фіскальний** and **Готівка** / **Без еквайрингу**, and the fiscal number ("Фіск. № …") for a fiscal receipt.
- The **Друкувати** (print) button sends the receipt to the receipt printer through the device manager (notification "Надіслано на друк"; when the printer is unavailable — "Принтер недоступний"). The button is disabled when the manager and a receipt printer are not connected in the settings.

---

## 3.9.5 Cash balance

> The **Cash balance** ("Баланс готівки") tab shows all movements on all cash accounts.

![](../../_media/pos-cash-balance.png ':size=420x253')

**Columns:**

| Column | Content |
|---|---|
| **Operation date** ("Дата операції") | Date and time |
| **Created by** | The user who made the operation |
| **Type** | **Продаж**, **Повернення**, **Внесення**, **Інкасація**, **Витрата**, **Переказ (вихід)**, **Переказ (вхід)**, **Скидання балансу** |
| **Account** ("Рахунок") | **Основна каса** or the name of a named account |
| **Comment** | Comment on the operation |
| **Operation amount** ("Сума операції") | Amount in UAH |
| **Total balance** ("Загальний баланс") | Balance after the operation |
| **Edit** ("Редагувати") | The SuperAdmin and Admin roles can change the record's **Comment** |

If there are no records, "Не знайдено жодного запису" is shown.

---

## 3.9.6 Advanced report

> The **Advanced report** ("Розширений Звіт") tab is a detailed financial report for the selected period, grouped by payment method.

![](../../_media/pos-advanced-report.png ':size=420x253')

**Report content:**

- **Баланс початок дня** and **Баланс кінець дня** (opening and closing balance) — the cash balance in UAH.
- Sections **Готівка**, **Картка**, **Безготівкова**, **Особовий рахунок** — transactions paid by the corresponding method. Columns: **Time** (a debt payment has the **Оплата боргу** badge), **Client**, **Discount**, **Type**, **Plans**, **Products**, **Amount**. Each section can be collapsed and has the line "Підсумок: N грн" (subtotal).
- **Операції з балансом** (balance operations) — movements on the [cash accounts](#_392-cash-accounts) with the **Тип операції** (operation type) and **Рахунок** (account) filters. Columns: **Time**, **Operation type**, **Account**, **Comment**, **Amount**; the line "Разом (після фільтрів):" (total after filters) holds the sum of the filtered operations.

If there are no operations, "Немає операцій" is shown.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.2 Clients

## 3.2.1 Client table

> The client table contains:

![](../../_media/clients-table.png ":size=200x121")

- **Name**
- **Phone**
- **Status** (active/inactive)
- **Active bookings** — shown in the format:  
  `Date, time, Workout name, Coach, Room — Status`
- **Status**:
  - **Planned** (green) — the client is booked for a workout
  - **Attended** (blue) — the client has been checked in for a workout
  - **Cancelled** (red) — the workout was cancelled, or the client cancelled it in time
  - **No-show** (orange) — the client did not come to the workout, or cancelled it too late
- **Plan** — shows the client's active plan, plus the number of single sessions (if purchased and not yet used).  
  If the client has plans, an **Edit** ("Редагувати") button (pencil icon) is available, which opens the [Editing plans](#_3-2-4-editing-plans) page.

![](../../_media/clients-plans.png ":size=150x27")

- **Card** — the client's card number
- **Actions** — available options:
  - **[History](#_3-2-5-history)** ("Історія") ![](../../_media/customers-transactions.png ":size=40x32")
  - **[Edit](#_3-2-6-editing-a-client)** ("Редагувати") ![](../../_media/customers-edit-button.png ":size=40x35")
  - **[Sale](#_3-2-7-sale)** ("Продаж") ![](../../_media/customers-sell.png ":size=40x38")
  - **[Booking](#_3-2-8-booking)** ("Запис") ![](../../_media/customer-booking.png ":size=40x40")
  - **[Registration](#_3-2-9-registration)** ("Реєстрація") ![](../../_media/customer-registration.png ":size=40x32")
  - **[Delete](#_3-2-10-deleting-a-client)** ("Видалити") ![](../../_media/customer-remove.png ":size=40x33")

---

## 3.2.2 Creating a client

> The **Add client** ("Додати клієнта") button is at the top left.

![](../../_media/add-customer.png ":size=230x149")

> Clicking it opens the **New client** ("Новий клієнт") modal window:

![](../../_media/add-customer-modal.png ":size=230x139")

- Client name
- Date of birth
- Phone
- Email
- Comment — a free-text note about the client
- Card generation and the **Enter card number manually** ("Ввести номер карти мануально") toggle work together:
  - If the toggle is off — the system automatically generates a digital card for the client.
  - If it is on — the field label changes to **Client card**, and the number must be entered manually: the scanner is disabled in the create/edit client window.

---

## 3.2.3 Scanning a card

> Scan the client's card with the scanner (from the physical card, a phone screen, or the mobile app).  
> Scanning works on any page, except when the create or edit client modal window is open.

- If the scan succeeds — the **[Registration](#_3-2-9-registration)** modal window opens.
- If the data is not recognized — a message appears:

![](../../_media/wrong-scan.png ":size=180x68")

---

## 3.2.4 Editing plans

> Clicking the plan-editing button opens a modal window:

![](../../_media/edit-customer-plans.png ":size=160x96")

**Contains:**

- Purchase date
- Name
- Status:
  - Active (green)
  - Inactive (gray)
  - Suspended (orange)
  - Ended (red)
- Type
- Sessions (remaining)
- Validity period
- Expiration date
- Actions:
  - Suspend (long-term plans only)
  - Activate (for a suspended or inactive plan)
- Edit (lets you change the number of sessions and the expiration date for an active plan)

> After changes are made, the **Save** button becomes active. Clicking it saves the changes and closes the window.

---

## 3.2.5 History

> Clicking the **History** button opens a modal window:

![](../../_media/client-transactions.png ":size=160x96")

- Contains the history of session movements across the client's plans, and the reason for each deduction.
- The date range can be changed with the date picker.

---

## 3.2.6 Editing a client

> Clicking the **Edit** button opens a window similar to the client-creation one, but with all fields pre-filled.  
> Only the **Client card** field cannot be edited, if the number was generated automatically.

---

## 3.2.7 Sale

![](../../_media/customer-sell-modal.png ":size=140x84")

**The sale modal window contains:**

- A filter by plan type
- A list of available plans
- Payment method
- A quantity control
- A discount field
- The amount due

---

## 3.2.8 Booking

![](../../_media/customer-book.png ":size=200x121")

- The **Current bookings** ("Поточні записи") tab shows the client's active bookings.
- If the workout is recurring, you can cancel only the nearest occurrence or all occurrences.
- If the workout is one-time, only a single cancel button is available.

**"Create booking" tab:**

![](../../_media/customer-book-1.png ":size=100x60")

- Choose a date — a list of workouts appears.
- Turn on the **Select** toggle to add a workout.

![](../../_media/customer-book-2.png ":size=100x65")

- The selected workout appears in the list at the top.
- The **Repeat** toggle determines whether the booking repeats.

### 3.2.8.1 No spots available

> If a workout is full, it is marked in red. Hovering over it shows the tooltip _"No spots available"_.

![](../../_media/client-book-2.png ":size=100x41")

- An administrator can still book/check in the client anyway.
- Booking is not possible through the mobile app.

### 3.2.8.2 Client vacation

![](../../_media/client-vacation-1.png ":size=100x60")

- Lets you add a vacation period for the client.
- During this period, the system does not create bookings for the client.

![](../../_media/client-vacation-2.png ":size=100x60")

- The vacation period is set by choosing a date range in the calendar.
- It can be removed.

---

## 3.2.9 Registration

- If the client has active bookings, the current day's workouts are shown.
- Unneeded ones can be removed.

![](../../_media/client-registration-1.png ":size=100x60")

- If there is an active plan, the **Registration** button is active and the amount due is 0.
- Clicking it checks the client in and deducts a session from the plan.

![](../../_media/client-registration-2.png ":size=100x60")

- If there are no plans, click **Add plan**.
- A single session or a plan can be purchased.

**`Warning! You cannot sell more single sessions than are needed for the selected workouts.`**

![](../../_media/client-registration-3.png ":size=100x60")

- The **Pay later** toggle — for deferred payment.
- In that case, the client is marked with a debt flag.

![](../../_media/client-dept.png ":size=230x26")

![](../../_media/client-registration-4.png ":size=100x60")

- If the client has no bookings, a workout can be chosen from the **Available workouts** list.
- Booking is also possible even if the client already has planned bookings.

![](../../_media/client-registration-5.png ":size=100x60")

- If there are inactive plans, they can be activated.
- If single sessions were purchased in advance, they can be used.

**Plan information:**

- If a plan is about to expire, the system shows a warning.

![](../../_media/client-registration-6.png ":size=100x79")

**Add product:** — lets you add a product to the transaction, even if the workout registration itself is being paid for from a plan.

### 3.2.9.1 Registering for a personal workout

> Personal workouts have a **fixed price for the whole workout** (not per client). In the registration modal window, a different payment method applies to them — with partial payments and automatic debt tracking shared across all booked clients.

**Specifics:**

- The **Workout price** column shows the **amount still owed** for this workout — not the plan price, but the actual remaining balance for that specific session.
- The amount field next to **Payment method** allows **free-form entry** — the cashier enters whatever amount the client is paying right now (for example, a partial amount).

![](../../_media/client-registration-personal-2x-partial-payment.png ":size=500x301")

**Partial payment and debt shared between clients:**

> If a workout is for 2+ people and one of the booked clients pays **partially**, the system automatically calculates the **debt for the entire workout** and shows it to all the other booked clients. As soon as the studio has received the full workout price across all the clients combined, the debt closes automatically.

Example: a personal workout for 2 people, priced at **UAH 1300**. The first client (`client 5`) pays **UAH 500** in cash. When opening [Registration](#_3-2-9-registration) for the second client (`тест бонус`) for that same workout:

- a red badge at the top of the modal window reads **"Warning!!! The client has a debt: UAH 800"** (1300 − 500);
- the **Workout price** column also shows **UAH 800** — the amount still owed for the workout to be paid in full.

![](../../_media/client-registration-personal-2x-second-client-debt.png ":size=500x301")

> ℹ️ A [Client debt](#_3-2-12-client-debt) record is created for both the first and the second client, for the same remaining amount — either of them can pay it off (in cash, by card, from the [Personal account](#_3-2-11-personal-account), or via a plan). Once paid in full, the record is automatically closed for all participants.

---

## 3.2.10 Deleting a client

- A client with status **Active** cannot be deleted.
- The client must first be deactivated, after which the **Delete** button becomes available.

---

## 3.2.11 Personal account

> Every client has a **Personal account** (wallet) — a place for advance deposits that can be used to pay for plans / products / single sessions. The balance is shown in the client's row in the table and in the client's mobile app.

![](../../_media/client-balance-row.png ":size=200x121")

### 3.2.11.1 Topping up the account

> Top-ups are made through the **Sale** modal window:

1. Click ![](../../_media/customers-sell.png ":size=30x28") in the client's row.
2. Choose **Account top-up** in the sale-type filter.
3. Enter the top-up amount, choose the payment method (Card / Cash / Cashless).
4. Click **Pay**.

![](../../_media/client-balance-topup.png ":size=500x301")

> ℹ️ A top-up is fiscalized as a regular transaction (if PRRO is active). The amount is credited immediately.

### 3.2.11.2 Paying from the account

> When selling a plan/product, or during a client's [Registration](#_3-2-9-registration), **"Personal account — X UAH"** appears in the list of payment methods, where X is the current balance.

![](../../_media/client-balance-pay.png ":size=500x301")

- Choose **Personal account** as the method (full payment), or enter an amount as a partial payment via **Split payment** together with Cash/Card.
- If the entered amount exceeds the balance, the modal window shows an error and the **Pay** button is disabled.
- The transaction **is not fiscalized** (because the funds were already fiscalized at top-up).

### 3.2.11.3 Account history

> The ![](../../_media/customers-transactions.png ":size=30x24") button opens the **History** modal window with two tabs: **Plans** and **Personal account**. The second tab shows all balance movements.

![](../../_media/client-balance-history.png ":size=500x301")

**Account history columns:**

| Column          | Description                                                              |
| ---------------- | ----------------------------------------------------------------- |
| **Date**         | Time of the operation                                                      |
| **Operation type** | Top-up / Deduction / Refund                                |
| **Amount**         | `+N UAH` (credit, green) or `−N UAH` (deduction, red) |
| **Description**             | The plan/product name, or "--" for a top-up                 |
| **Created by**     | The name of the administrator who performed the operation                                    |

> 📱 The client sees their account and its full history in the mobile app, on the **Profile → Account** tab.

---

## 3.2.12 Client debt

> If a client registers for a workout or buys a product using the **Pay later** toggle, the system creates a debt record. A **Debt** badge appears next to the client's name.

### 3.2.12.1 Debt icon

> Clients with active debt have a **yellow "Debt" badge** next to their name in the table row. An additional `Debt Payment` (`pi-wallet`) button appears in the **Actions** column.

### 3.2.12.2 Paying off debt

> Clicking the **Debt Payment** button opens the **Debt payment** modal window:

![](../../_media/client-debt-modal.png ":size=500x301")

**Modal window structure:**

1. **Active debts table** — columns: Date • Description • Amount • Status • Actions.
   - **Description** — what the debt is for (for example, "Debt for workout: Fly-stretching").
   - **Amount** — in sessions or in UAH (depending on the debt type).
   - **Status** — Awaiting payment / Paid.
   - **Close with plan** — a button next to a workout-debt row; deducts the debt from the client's active plan (without a cash payment).
   - **🗑 Delete** (trash icon) — delete the debt without payment (SuperAdmin/Admin only).

2. **"Purchase a plan to pay off debt" section** — sells a plan while simultaneously deducting the debt from it:
   - **Choose a plan** — a dropdown list of the studio's plans.
   - **Payment method** (Cash / Card / Personal account) + amount.
   - **Split payment** — adds a second payment method (split pay).
   - **Discount (discount amount)** + **Percent %** toggle.
   - **Amount due** — the final amount.
   - **Pay** — creates a plan-sale transaction, credits the plan to the client, and closes the debt(s) at the same time.

> ℹ️ If the debt is for a product (not a workout), it is usually paid in cash without purchasing a plan.

---

## 3.2.13 Search and filter

![](../../_media/clients-search.png ":size=150x55")

- Search is available across all fields: name, phone, card number, and so on.
- Clients can be filtered by workout.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

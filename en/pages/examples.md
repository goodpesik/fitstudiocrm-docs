[Back to home](/en/)

# 5. Examples and Tips

---

## 5.1 Group Personal Workouts

> Case: a personal workout for two or more clients, where the coach receives a **fixed amount for the workout itself** (not a multiplier based on the number of clients).

**Steps:**

1. **Create a [plan](/en/menu/plans)** with the type **Personal** and a price that *each* participating client pays (this is their ticket to a single session).
2. **Create a [category](/en/login/settings#categories)** for this type of workout:
   - **Rate type = За тренування** (Per workout, `PerWorkout`) — the coach is credited a fixed amount regardless of the number of participants.
   - **Base rate** — the amount the coach receives for a held session.
   - **Membership** — you must link the personal plan you just created. Without the link the **Зберегти** (Save) button is active, but the server rejects saving with the message «Абонемент обов'язковий для типу 'За тренування'» (A membership is required for the 'Per workout' type).
3. **Create a workout** on the [Workouts](/en/menu/workouts) page:
   - The **Персональне** (Personal) switch — on.
   - **Максимальна кіл-сть людей на тренуванні** (Maximum number of people per workout) — set `2` or more.
   - **Category** — select the one created above.
   - The **Виберіть клієнта** (Select a client) field is shown for personal workouts and is not required: clients can be booked later.
4. **Book the clients** via [Booking](/en/menu/clients#_328-booking) or [Registration](/en/menu/clients#_329-registration). Each client's session is deducted from their own personal plan.

> ℹ️ If the coach receives an amount **proportional to the number of clients**, choose the **За людину** (Per person, `PerPerson`) rate type and set the base rate **per client**. Linking a plan is optional for this type.

> ℹ️ The rate and calculation type are taken from the **workout category**. The rate is not set on the coach's card.

---

## 5.2 Masterclass

> Case: a one-time event (masterclass) with a limited number of participants, paid from the participants' plans.

**Steps:**

1. **If needed, create a [coach](/en/menu/coaches)** for the instructor.
2. **Create a [plan](/en/menu/plans)** with the type **Personal** and a price equal to the participation cost for the client.
3. **Create a [category](/en/login/settings#categories)** for the masterclass:
   - **Rate type**:
     - **За тренування** (`PerWorkout`) — a fixed fee for the instructor for the held event; you **must link the plan** from step 2 to the category;
     - **За людину** (`PerPerson`) — the instructor is paid for each participant; linking a plan is optional.
   - **Base rate** — according to the model.
4. **Create a [workout](/en/menu/workouts)** on a specific date:
   - The **Персональне** switch — on, **Регулярне** (Regular) — off.
   - **Максимальна кіл-сть людей на тренуванні** — the maximum number of participants.
   - **Category** — select the one created above.
5. **Book the clients** for the masterclass. The client field in the workout form is optional; clients can be added later via [Booking](/en/menu/clients#_328-booking) or [Registration](/en/menu/clients#_329-registration).

> ℹ️ Masterclass plans can be sold **in advance**. A purchased personal plan is inactive until registration; in the registration window it is activated with the **Активувати** (Activate) switch in the **Неактивні абонементи клієнта** (Client's inactive memberships) block, and the session is deducted.

---

## 5.3 Registration with a Previously Purchased Single-Session Plan

> Scenario: a client previously purchased a **single-session personal plan** (the session has not yet been used), and you are now registering them for a workout using this plan.

**In the [Registration](/en/menu/clients#_329-registration) modal window:**

- If the client has unused single-session plans, they are shown in the **Разові абонементи клієнта** (Client's single-session memberships) block with the **Використовувати** (Use) switch.
- Turning on **Використовувати** for a plan:
  - the plan is used for this registration instead of buying a new one;
  - the sale row of a new plan in the payment block can be removed;
  - the **До сплати** (Amount due) total becomes `0 UAH`;
  - the client is registered without payment, the session is deducted from the existing plan.
- If more single-session plans are selected than workouts, registration is blocked with the message «Вибрано надлишок разових абонементів» (Too many single-session memberships selected).

> ℹ️ If the client has a debt, the window shows the warning «Увага!!! У клієнта є борг: <amount>» (Attention!!! The client has a debt) — see [Client debt](/en/menu/clients#_3212-client-debt).

> ℹ️ The **Розділити оплату** (Split payment) button splits the amount between payment methods; the «Особовий рахунок — N грн» (Personal account — N UAH) method is available if the [personal account](/en/menu/clients#_3211-personal-account) balance is greater than 0.

> ℹ️ If **Сплатити пізніше** (Pay later) is on with a non-zero amount, the **Оплата** (Payment) window with the text «Ви впевнені що хочете продовжити?» (Are you sure you want to continue?) opens before registration; the amount is recorded as the client's debt — see [Debts](/en/pages/processing#_613-debts).

---

[Back to home](/en/)

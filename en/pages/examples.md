[Back to home](/en/)

# 5. Examples and Tips

---

## 5.1 Group Personal Workouts

> Case: a personal workout for two or more clients, where the coach receives a **fixed amount for the workout itself** (not a multiplier based on the number of clients).

**Steps:**

1. **Create a [plan](/en/menu/plans)** with the type **Personal** and a price that *each* participating client pays (this is their ticket to a single session).
2. **Create a [category](/en/login/settings#categories)** for this type of workout:
   - **Rate type = Per Workout** (`PerWorkout`) — the coach will be credited a fixed amount, regardless of the number of participants.
   - **Base rate** — the amount the coach receives for a conducted session.
   - **Plan** — you must link the personal plan you just created. Without this link, the **Save** button remains active, but saving will fail with a server error: "A plan is required for the 'Per Workout' type."
3. **Create the workout** on the [Workouts](/en/menu/workouts) page:
   - The **Personal** toggle — enabled.
   - **Maximum number of people per workout** — set to `2` or more.
   - **Category** — select the one created above.
   - The client selection field appears for Personal workouts, but it is **not required** — you can leave it empty and add clients later.
4. **Book the clients** via [Booking](/en/menu/clients#_3-2-8-booking) or [Registration](/en/menu/clients#_3-2-9-registration). Each client's session is deducted from their own personal plan.

> ℹ️ If, for a group-personal workout, the coach receives an amount **proportional to the number of clients** (for example, X UAH per person) — use `PerPerson` as the rate type instead, and set the base rate **per client**. Linking a plan for `PerPerson` is optional.

> ℹ️ The rate and calculation type are always taken from the **workout category**. The rate is no longer set on the coach's card.

---

## 5.2 Masterclass

> Case: a one-time event / masterclass with a fixed number of participants, which needs to be held once and deducted from the participants' plans.

**Steps:**

1. **If needed, create a [coach](/en/menu/coaches)** (if this is a new guest instructor).
2. **Create a [plan](/en/menu/plans)** with the type **Personal** and a price equal to the participation cost for the client.
3. **Create a [category](/en/login/settings#categories)** for the masterclass:
   - **Rate type**:
     - `PerWorkout` — if the instructor has a fixed fee for holding the event (in this case, you **must link the plan** from step 2 to the category);
     - `PerPerson` — if the instructor is paid per participant (linking a plan is optional).
   - **Base rate** — according to the chosen model.
4. **Create the [workout](/en/menu/workouts)** for a specific date:
   - The **Personal** toggle — enabled, **Regular** — disabled.
   - **Maximum number of people per workout** — the maximum number of event participants.
   - **Category** — select the one created above.
5. **Book the clients** for the masterclass. The client field in the workout form is optional — clients can be added later via [Booking](/en/menu/clients#_3-2-8-booking) or [Registration](/en/menu/clients#_3-2-9-registration).

> ℹ️ Masterclass plans can be sold **in advance**. A purchased plan of type *Personal* will be *inactive* until registration — when registering the client, the admin activates it and deducts the session.

---

## 5.3 Registration with a Previously Purchased Single-Session Plan

> Scenario: a client previously purchased a **single-session personal plan** (the session has not yet been used), and you are now registering them for a workout using this plan.

**In the [Registration](/en/menu/clients#_3-2-9-registration) modal window:**

- In the **Payment:** section, a plan to be purchased "on the fly" is selected by default — it is not empty and cannot be deleted immediately unless there is an alternative.
- If the client has unused single-session personal plans, they are shown in the **Client's Single-Session Plans** section with a **Use** column.
- Turning on the **Use** toggle for an existing plan:
  - puts it into active use for this registration,
  - in the **Payment:** section, the new sale row can be deleted (the button becomes active),
  - the **Amount Due** becomes `0 UAH`,
  - the client is registered without any transactions — the old plan is deducted instead of purchasing a new one.

> ℹ️ If the client still has a **debt** (monetary or in workouts), a warning appears at the top of the modal in the [Client Debt](/en/menu/clients#_3-2-12-client-debt) block.

> ℹ️ If the workout is **personal** and you want to accept payment partly by cash / card and partly from the [Personal Account](/en/menu/clients#_3-2-11-personal-account) — a row with method selection appears above the **Payment:** section. For group workouts, this row is not shown.

> ℹ️ If you enable **Pay Later** with a non-zero amount — before the final confirmation, a modal appears: "Are you sure the client will come to pay?" with a summary.

---

[Back to home](/en/)

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.1 Schedule

> The **Schedule** tab

![](../../_media/schedule-main.png ':size=400x241')

> The schedule is displayed as a calendar. By default, the current week is shown.

**Elements:**

- **Date picker** — lets you choose a specific date. After selecting a date, the week containing that date is shown.
- To the left and right of the date picker are the back «<<» and forward «>>» buttons, which let you move between weeks.
- **Filter** button

![](../../_media/scedule-filter.png ':size=300x181')

  - Lets you filter what is displayed in the schedule.
  - Filter by room.
  - Filter by coach.
  - Filter by workout type (Regular, Personal, Rental).

- **Download PNG** button — after clicking, downloads an image of the schedule with the items shown in the calendar, taking the selected filters into account.

---

![](../../_media/schedule-card.png ':no-zoom')

> A workout card contains:

- The workout name.
- The workout time.
- The coach's name, or **Rental**.

> Hovering over any cell (empty or containing a workout, if the cell is in the future or belongs to the current day)  
> shows a button that lets you add a workout.

![](../../_media/add-workout.png ':size=150x100')

[More about creating a workout](/en/menu/workouts#_3-3-1-create-a-workout)

> Clicking a workout card opens a modal window with details and actions.

![](../../_media/schedule-card-details.png ':size=420x253')

**Modal window header:**

- The workout name.
- Badges: **workout type** (group / personal / rental). For recurring workouts, there is also a **Recurring** badge and the **days of the week**; one-time workouts have no mode badge.
- **Go to workout** button — opens the [Workouts](/en/menu/workouts) page at the specific record.
- **⚙ Settings** button (gear icon) — see [Settings button](#settings-button).

**Workout information:**

- The coach's avatar and name (the avatar is shown if it is set on the [coach's card](/en/menu/coaches#_3-4-1-coach-card)).
- The workout date and time. If a substitute coach has been assigned, "Substitute: Substitute_name" is shown next to it.
- The room.

**Counters:**

| Field | What it counts |
|---|---|
| **Planned to attend** | Clients with status **Planned**. |
| **Attended** | Clients checked in via **Registration** (status **Attended**). |
| **Cancelled** | Clients with status **Cancelled**, plus those marked **No-show** whose session was not deducted from their plan. |
| **No-show** | Clients who missed the workout (status **No-show**). A session is deducted from their plan. |
| **Waiting list** | Clients in the queue (status **Waiting list**) — they will be added automatically once a slot opens up. |
| **Spots remaining** | `workoutCapacity − (Planned + Attended)`, and if the workout has not taken place yet, reserved spots are additionally subtracted. Clients on the waiting list do not take up a spot. Shown only if a maximum capacity is set. |
| **Reserved spots** | Clients with a repeat-booking setting configured — potentially booked automatically. Visible only for future recurring workouts. |
| **Credited to coach** | How many clients / workouts will be credited to the coach for payroll, taking the [minimum count and capacity-cap settings](/en/login/settings#features) into account. |

**Main actions:**

- **Cancel workout** button (in the window header, next to the gear button) — shows the ["Are you sure you want to continue?"](../_modals/are-you-sure-modal.md ':include') confirmation modal window. If confirmed, the workout is cancelled for that day. A personal training prepayment is credited to the client's personal account under the rules of [Personal training prepayment](#personal-training-prepayment).

  > ⚠️ If at least one client is already checked in for the workout (the **Visited** status), the **Cancel workout** button is disabled. A prepayment does not affect whether the button is available.

- **Book a client** toggle — see [Book a client](#book-a-client).
- Settings button — see [Settings button](#settings-button).

### Personal training prepayment

> For a personal training the window shows the training price and the prepayment state.

| Field | What it shows |
|---|---|
| **Training price** | The price of the plan set in the training's [category](/en/login/settings#categories). If the category has no plan or the plan price is 0, **Price not set** is shown instead. |
| **Prepayment** | `X of Y UAH`, where X is the amount already paid for this training and Y is the training price. With no payments — **none**. |

The **Make a prepayment** button opens the **Training prepayment** window:

- **Client** — the client the prepayment is made for. Only clients with the **Planned** status are available. With one such client it is selected automatically; with several the client is picked from the list.
- **Prepayment amount, UAH** — any amount greater than 0 and not greater than **Left to pay** (the training price minus what is already paid).
- **Payment method** — cash, card, bank transfer or the client's personal account; the payment can be split across several methods. No discount applies to a prepayment.

The **Make a prepayment** button in the window first checks the prepayment on the server; only after a successful check does a card payment go through the terminal. Then a sale is recorded on the register: a transaction of the **Personal training prepayment** type is created, a fiscal receipt is issued. The prepayment amount is added to the amount paid for the training. A bank transfer is added to the amount paid for the training at once, before the transfer is confirmed in the register.

If the server refuses the prepayment during the check, the terminal is not called and the system shows the reason. If with a split payment some payments are saved and a following payment is not, the system shows the sum of the saved payments and reports only the card payments for which no transaction was created.

The **Make a prepayment** button on the training card is disabled when:

| Condition | Hint above the button |
|---|---|
| The training price is not set | — (**Price not set** is shown instead of the price) |
| No client with the **Planned** status is booked | **Add a client first** |
| The training is cancelled | **Тренування скасовано** (The training is cancelled) |
| The training start time has come or passed, including a past training opened in edit mode | **Тренування вже розпочалося** (The training has already started) |
| The training is paid in full | **The training is paid in full** |
| The shift is not open | **Open a shift first** |

The server also refuses a prepayment for a training that has already started.

**Prepayment rules:**

- The total prepayment for a training cannot exceed its price. The server refuses a prepayment above the remaining amount, also when two payments are made at the same time.
- When the client is [registered](/en/menu/clients) on a prepaid training, the client's prepayment is deducted from the price of the plan sold for the training: only the remainder is due.
- A prepayment amount is at least 0.01 UAH, in whole kopecks.
- When the training is cancelled (with **Cancel workout**, by deleting or deactivating the workout, by shortening the repeat period, by clearing the schedule), the prepayment is credited automatically to the [personal account](/en/menu/clients) of the client who made it. The amount paid for the training is reduced by the returned amount.
- When a client is removed from the training, their booking is cancelled, or they are moved to another training, while the training itself is not cancelled, that client's prepayment is credited to their personal account in the same way as on a training cancel. The prepayments of other clients stay on the training.
- When a client gets the **Не відвідано** (Not visited) status, the prepayment counts as the no-show payment. The no-show debt (see the setting for automatic no-show debt on a personal training) is created only for the difference between the training price and the prepayment; when the prepayment covers the price, no debt is created.
- When the client holds a plan with a duration and that plan covers the prepaid training at [registration](/en/menu/clients), the prepayment is credited automatically to the client's personal account. The amount paid for the training is reduced by the credited amount.
- A cash or card prepayment is credited to the personal account as a top-up. A prepayment from the personal account goes back to the personal account as a refund. In the personal account history the operation is described as **Повернення передоплати за персональне тренування** (Prepayment returned for a personal training).
- A bank-transfer prepayment is credited to the personal account only when the transfer has been confirmed in the register. An unconfirmed transfer is cancelled together with the training or with the client leaving it: nothing is credited to the personal account, the register shows the payment status **Скасовано** (Cancelled), and the transfer cannot be confirmed afterwards.
- When the client who made a prepayment is deleted from the system, the prepayment stays an open transaction in the register and can be refunded through the register.
- A register refund of a prepayment transaction reduces the amount paid for the training. A prepayment already credited to the personal account cannot be refunded through the register. A refund and a credit of the same prepayment cannot run at the same time: the second operation sees the result of the first.
- The **Change payment method** action in the register is available for a prepayment transaction not yet credited to the personal account and without refunds, except a prepayment from the personal account. The server checks the new transaction before the old one is refunded; when the check fails, the payment method is not changed. The new transaction stays a prepayment for the same training, including after the training has started. The credit rules on cancel follow the new payment method: for a bank transfer, only once the transfer is confirmed.

### Book a client

> Activating it shows a select field for choosing a client

![](../../_media/schedule-card-details-2.png ':size=400x241')

> after selecting

![](../../_media/new-client-1.png ':size=300x181')

- **Duplicate booking** toggle — sets the booking to repeat automatically
- **Confirm booking** button — after clicking, the client is booked for the selected workout

> The **+ New client** option is also available

![](../../_media/add-client-select.png ':size=400x241')
![](../../_media/new-client-2.png ':size=100x59')

> after selection, the client is booked for the workout

### Settings button

![](../../_media/schedule-card-details-3.png ':size=400x241')

> The gear button opens a popup with actions for the workout:

- **Cancel workout** — cancels this workout for this day (returns the deducted session to the plan of booked clients; credits a personal training prepayment to the client's personal account — see [Personal training prepayment](#personal-training-prepayment)).
- **Substitute coach** — opens a select field with coaches; after choosing one, a **Save substitute coach** button appears. While a substitute is active, a **Remove substitute** button is available.

  ![](../../_media/substitute-2.png ':size=300x181')
- **Change room** — opens a select field with rooms; the change applies only to this date.
- **Change workout time** — opens a time picker for moving the workout to another time within this date.
- **Change workout category** — changes the category (affects the coach's payroll calculation for this occurrence).

> All of these actions apply **only to the specific date**; the recurring workout template is not changed. To change the template, edit it on the [Workouts](/en/menu/workouts) page.


### Clients

> If clients are booked for the workout, their names are shown as a list at the bottom of the modal window. Each name is a clickable badge colored by status.
> Clicking a name opens a **context menu**, whose set of options depends on the client's current status and on whether the workout has already taken place.

**Statuses and badge colors:**

| Color (severity) | Status | Description |
|---|---|---|
| Gray (`secondary`) | **Planned** | The client is booked but not yet checked in. |
| Green (`success`) | **Attended** | The client has been checked in for the workout. |
| Red (`danger`) | **Cancelled** | The client or an administrator cancelled the booking in time. |
| Orange (`warn`) | **No-show** | The client did not come, or cancelled after the allowed cancellation window. A session has been deducted from the plan. |
| Blue (`info`) | **Waiting list** | The client is in the queue, waiting for a slot to open up. |
| Yellow | **Reserved** | Not a real status — it is a future automatic booking from a [client with a repeat-booking setting](/en/menu/clients#_3-2-8-booking). Visible only for future workouts. |

**Context menu — options by status:**

- **Planned** → "Cancel booking"; "Check in client" (only if the workout is today).
- **Attended** → "Undo check-in" — returns the status to Planned and returns the deducted session to the client's plan (for correcting cashier mistakes).
- **Cancelled** → "Change status to Attended" — does not affect the plan.
- **No-show** → "Change status to Attended", "Change status to Cancelled" (returns the session to the plan, if it was deducted).
- **Waiting list** → "Remove from waiting list".
- **Reserved** → "Cancel the reservation" — the client will not be booked automatically for the selected date.

> ℹ️ When **booking a client once** for a specific occurrence of a recurring workout: if the client repeats only on certain days of the week (e.g. Tuesday), then on a day that is not in their `repeatDays` (e.g. Thursday) the client has status **Paused**, but the administrator can **book them for that one occurrence** via the [Choose a client](#book-a-client) combo box — the status changes to **Planned** for that specific day only, without affecting the recurring schedule.

### Reserved spots

If a workout is recurring and has clients booked with the duplicate-booking setting enabled, then for future occurrences of that workout, reserved spots become available. Reserved spots show the clients who are potentially going to be booked for this workout automatically. The number of spots remaining for the workout is shown taking the reserved count into account, to prevent overbooking.

![](../../_media/schedule-card-details-4.png ':size=70x88')
![](../../_media/schedule-card-details-5.png ':size=70x82')
![](../../_media/schedule-card-details-6.png ':size=70x82')
![](../../_media/schedule-card-details-7.png ':size=70x87')

**`Important! If at least one person is already checked in for the workout, it cannot be cancelled!`**

---

## Studio closures

> The **Studio closures** button on the schedule's top panel opens a popup for managing the days when the studio is closed (holidays, technical breaks, etc.).

### How to add a closure

1. Click **Studio closures**.
2. Click **Add exception** — a row with a date picker appears.
3. Choose a date.
4. You can add several dates in a row.
5. Click **Save**.

![](../../_media/schedule-holidays-popover.png ':size=300x181')

### What happens on save

- A background job starts (the [background jobs modal](/en/pages/processing#_6-5-background-tasks) is shown).
- All workouts on the selected dates are **cancelled** automatically; the dependent client bookings get status **Cancelled**.
- The list of closures is saved in the studio settings.

### How to remove a closure

1. Open the **Studio closures** popup.
2. Click **🗑 Delete** (trash icon) on the row with the relevant date.
3. Click **Save**.

> ⚠️ Removing a closure **restores** the workouts and bookings for that date — also via a background job.

> ℹ️ Past dates remain in the list for the record, but cannot be edited (`minDate` limits the picker to today's date).

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

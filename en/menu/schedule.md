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

- **Cancel workout** button (in the window header, next to the gear button) — shows the ["Are you sure you want to continue?"](../_modals/are-you-sure-modal.md ':include') confirmation modal window. If confirmed, the workout is cancelled for that day.

  > ⚠️ If at least one person is already checked in for the workout, it cannot be cancelled.

- **Book a client** toggle — see [Book a client](#book-a-client).
- Settings button — see [Settings button](#settings-button).

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

- **Cancel workout** — cancels this workout for this day (returns the deducted session to the plan of booked clients).
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

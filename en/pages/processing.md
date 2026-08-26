[Back to home](/en/)

# 6. Information on How the System Processes Workout Visits, Plan Deductions, Reminders, and More

## 6.1 Workout Recurrence

> If a workout is recurring, the system automatically creates a workout instance in the calendar on the recurrence date.

> If a client's booking is recurring, the system automatically creates a new workout booking for the client at **5:00 AM the next day** after the workout takes place.


``` For example: The workout takes place on Tuesdays and Thursdays. The client is booked on a workout with recurrence enabled. The workout took place on Tuesday, July 8, 2025. At 5 AM on July 9, 2025, the system will automatically create a booking for the client for the same workout, which will take place on Thursday, July 10, 2025```

## 6.2 Deducting Workout Visits

> At the moment of registering for a workout with an active plan, the system automatically deducts a number of sessions equal to the number of sessions selected for attendance.

> If a client does not show up for a workout, or cancels it later than the maximum allowed cancellation window, the system will automatically deduct **1 session** from the active plan for each such session.  
> The deduction happens at **5:00 AM the next day**.

---

## 6.3 Calculating Coach Salaries

> The system selects all of the coach's workouts for the current period, groups them **by workout category** (the category assigned on the workout itself), and calculates pay depending on the rate type **of that category**.

> ℹ️ **All calculation parameters (rate type + base rate) are defined exclusively on the workout category** ([Settings → Categories](/en/login/settings#categories)). There are no individual rates set on a coach or on a specific workout.

- **Rate type `PerPerson` ("Per Person")**
  For each workout in the category, the system counts the number of clients who actually attended (status `Visited`) plus clients with status `Unvisited` whose session was deducted from the plan (canceled late). If this is fewer than the **Minimum Number of Clients** ([Settings → Features](/en/login/settings#features)), the minimum is used instead. If it is more than `workoutCapacity` and the corresponding toggle is enabled, it is capped at capacity. The sum across workouts × the category's `baseRate` = the salary for this category.

- **Rate type `PerWorkout` ("Per Workout")**
  The system counts the number of **conducted** workouts in the category (workouts with at least one client with status `Visited`). Number of workouts × the category's `baseRate` = the salary for this category.

> The total salary = the sum across all categories in which the coach had workouts during the period.

---

## 6.4 Calculating Administrator Salaries

> Salary = `hours worked × hourly rate` + the sum of bonuses accrued for the period.

- **Hours worked** — the sum of hours from all of the admin's closed [Shifts](/en/menu/reports#_3-8-2-shifts) within the selected range. An admin can edit hours **only for their own closed** shifts.
- **Hourly rate** — set in [Settings → Users](/en/login/settings#users) individually for each admin (the **Hourly Rate** field).
- **Bonuses** — accrued according to the rules in [Settings → Features → Administrator Bonuses](/en/login/settings#administrator-bonuses). Each bonus is a condition (event type) × amount × filter (new client / all).
- **Summary** — shown on the [Reports → Admin Salaries](/en/menu/reports#_3-8-5-administrator-payroll) page.

---

## 6.5 Background Tasks

> Some actions in the system trigger a **background task** on the server, because they may take anywhere from a few seconds to a few minutes and require updating a large number of records. While it runs, a progress modal window opens for the user.

**Examples of actions that trigger a background task:**

- Adding or removing a date in **[Studio Days Off](/en/menu/schedule#studio-closures)** — the system goes through all recurring workouts and adds/removes exceptions for the selected date, moving dependent bookings to "Canceled" status / back to "Planned".
- Clearing workouts (via the admin panel → "Clear Workouts") — deletes all workouts that have not taken place and unbooks clients.
- Changing the studio's time zone (potentially affects all future workouts).

**Progress modal:**

- The title describes the type of task (for example, "Updating studio days off").
- A progress bar shows `X / N` processed items.
- While the task is not finished, the modal **cannot be closed**, so the user cannot leave the system in a partially processed state.
- Once finished, a **Close** button appears, and the data on the current page is reloaded.

> ⚠️ Do not close the browser tab while the task is running — this will not stop it on the server, but you will not see when it finishes, and the corresponding data will not update automatically in your interface.

---

## 6.6 Class reminders

> There are **two reminders, and they are independent**. This is the most important thing to know: one is set by the client for themselves, the other by the studio for everyone else.

### The in-app reminder, set by the client

A client with the app installed and notifications enabled chooses how many hours in advance to be reminded — in the [Notifications](/en/mobile/notifications) section, from 1 to 24 hours. This costs the studio nothing.

### The reminder for everyone else, set by the studio

For clients without the app there is a separate studio setting — **Remind about a visit** ("Нагадувати про візит") on the [Mobile Application](/en/login/settings#mobile-application) tab. The channel is chosen automatically:

1. If the client has ever signed in through the Telegram bot, the message goes **to Telegram**. Free of charge.
2. If not, and the studio has SMS enabled and monthly quota left, an **SMS** is sent. This is charged.
3. If neither applies, no reminder is sent.

> ⚠️ The studio setting **does not affect clients who have the app** — they have their own. Changing this field will therefore change nothing for anyone already using the app.

### The night pause

Reminders are not sent **between 22:00 and 06:00**, whatever the channel and whatever the client asked for. If the calculated reminder time falls inside that window, the reminder is not sent at all — it is not postponed until the morning. This matters for early classes: a "2 hours before" reminder for a 07:00 class falls at 05:00 and will not fire.

### The monthly SMS limit

The limit is **shared across all of the studio's SMS**: both visit reminders and the confirmation codes for guest bookings. Once it is used up, guest bookings can only be confirmed through Telegram, and SMS reminders stop being sent. The remaining amount is shown next to the "Remind about a visit" field.

---

## 6.7 Membership expiry

Each night the system sets a membership to **Ended** when its end date has passed or all its sessions have been used. Memberships of the "Rent" type are closed by date only.

The client receives no separate notification of the expiry itself. About 12 hours beforehand one warning notification is sent, and only to clients who have the app installed. A client without the app finds out when they try to book.

---

## 6.8 Client vacation and the "Paused" status

When the nightly job creates the next class of a recurring schedule and sees that the date falls within a [client's vacation](/en/menu/clients), it does not skip the client silently: the booking is created with the **Paused** status. No session is deducted from the membership and no place is taken.

That is why a client may see an otherwise puzzling "Paused" status in the app — the reason is the vacation the studio entered for that date.

---

## 6.9 Removal from a recurring booking after misses

If the corresponding rule is enabled in [Settings → Features](/en/login/settings#features), a client who misses the configured number of classes in a row is removed from the recurring booking automatically. The administrator receives a notification. After that the client can only be booked manually.

---

[Back to home](/en/)

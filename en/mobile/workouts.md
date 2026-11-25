<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.5 Workouts

> The **Workouts** tab shows the studio schedule for the selected day. A client books, cancels and restores bookings and leaves the wait list; a coach and an administrator view the schedule, create workouts and manage them.

The schedule for a user without a client card in the studio is described in [7.2 Registration and Studio Selection](/en/mobile/registration#_721-booking-request).

---

## 7.5.1 Choosing a Day

- The **«Workouts»** heading and, under it, a button with the studio name and the month — opens the **«Select a day»** calendar with the **«Today»** button.
- The week strip: tapping a day opens it; the arrows switch the week. A dot under a day marks a day on which the user has their own booking. The day is also changed by swiping the screen left or right.
- Available date range:
  - **Client:** from today to **+15 days**.
  - **Coach / Admin:** past days without limit and up to **+30 days** ahead.
- The strip days, «today», the available date range and studio days off follow the [studio time zone](/en/login/settings#studio-time-zone) regardless of the phone's time zone.
- The day heading: weekday, date and number of workouts (for example, «Saturday, 17 October · 4 classes»).
- The **«My workouts»** filter (client and coach) shows only own bookings or own workouts.
- On a studio day off, «The studio is closed on this day» is shown; the **«Create»** button is not shown.
- An empty day — «No workouts on this day»; with the filter on — «No active bookings for this date» (client) or «You have no workouts on this day.» (coach).

---

## 7.5.2 Workout Card (Client)

The card shows the start time, the room, the coach photo or initial with the coach rating, the workout name and the line «Coach: {name}». For a workout with a limited number of seats — an occupancy bar and «Seats: {free} of {total}».

The bottom of the card shows the booking state:

| State | Meaning |
|---|---|
| **Book** (button) | Booking is available. |
| **You are booked ✓** | The client is booked; the card menu has **«Cancel booking»**. |
| **Wait list** | The client is on the wait list; the card menu has **«Leave the wait list»**. |
| **Стати в лист очікування** (Join the waiting list, button) | There are no free seats; the button adds the client to the waiting list, see [7.5.5](#_755-wait-list). |
| **No seats left** | There are no free seats while a workout is chosen in a [registration request to the studio](/en/mobile/registration); the waiting list is not available in this mode. |
| **you have another booking at this time** | The client has a booking for a workout that overlaps in time. |
| **paused** | The booking is paused for this day (client vacation). |
| **canceled** | The workout was cancelled by the studio or the client's booking for it was cancelled; if the booking can be restored, the card menu has **«Restore booking»**. |
| **booking unavailable** | The workout has already started or passed. |

Under the card of an upcoming workout the client is booked for — the **«Add to calendar»** button: adds the class to the phone calendar. Error — «Could not add the class to the calendar».

Under the schedule — the note: «Important!!! If you have recurring workouts, automatic booking for them happens the day after the current workout date.»

---

## 7.5.3 Booking a Workout (Client)

1. Select a day and tap **«Book»** on the workout card.
2. The app checks that booking is still available. If not — the window «Booking for this workout is no longer available» with the **«Got it»** button; the schedule is refreshed.
3. In the **«Workout booking»** window check the client, workout, coach, room, date and time → **«Continue»** (or **«Cancel»**).
4. After a successful booking, the **«You are booked for the workout»** window is shown with the class details and the **«Done»** button. The studio administrators receive a notification about the booking.
5. If the booking got the **Waiting list** status, the **«Вас додано до листа очікування»** (You have been added to the waiting list) window is shown instead of **«You are booked for the workout»**, with the text «Вільні місця на цьому занятті першочергово надаються клієнтам з листа очікування. Вас додано до листа очікування.» (Free seats in this class are given first to clients on the waiting list. You have been added to the waiting list.) and the class details.

A booking made in the app by a client of the studio does not require administrator confirmation: the seat is taken immediately. Confirmation is required for bookings from the [public studio page](/en/mobile/guest) (if turned on) and for [requests from users without a client card](/en/mobile/registration).

If the server refuses the booking (no seats, the client is already booked, the workout is cancelled), the reason is shown in an error window and the schedule is refreshed.

> ℹ️ The deduction from the plan is not shown at the moment of booking. The number of workouts left is shown on [Home](/en/mobile/home) and in [Account](/en/mobile/account).

---

## 7.5.4 Cancelling and Restoring a Booking (Client)

**Cancellation.** Available for a booking with the **Planned** status for a workout that has not started yet.

1. Card menu (bin icon) → **«Cancel booking»**.
2. The **«Cancel workout»** window shows the class details → **«Continue»**.
3. Result — «Workout booking canceled»; error — «Could not cancel the booking. Try again or contact the studio.»

> ⚠️ **A late cancellation deducts the workout.** If the studio has set [«Мінімальний час до відміни тренування»](/en/login/settings#minimum-time-before-workout-cancellation) (Minimum time before workout cancellation), the client has an active plan with workouts left, and less than that time remains before the start, the cancellation window shows «Since you are cancelling less than {N} h before the session, it will be deducted from your subscription.» A booking cancelled within an hour after it was made is not deducted.

**Restoring.** Available for one's own cancelled booking (statuses **Canceled**, **Missed**, **Registration canceled**) if the workout is not cancelled by the studio, more than an hour remains before the start and there is a free seat. A booking cancelled from the wait list returns to the wait list regardless of the number of seats.

1. Card menu → **«Restore booking»**.
2. The **«Restore booking»** window: «Restore your booking for this class?» → **«Continue»**.
3. Result — «Booking restored»; error — «Could not restore the booking. The class may be full, or less than an hour is left before it starts.»

---

## 7.5.5 Wait List

- A client gets on the wait list when an administrator books them for a workout without free seats (see [Schedule](/en/menu/schedule)), or by themselves from the app.
- **Joining the wait list:** for a workout without free seats the card shows the **«Стати в лист очікування»** (Join the waiting list) button → the **«Запис до листа очікування»** (Joining the waiting list) window → **«Continue»**. The **«Вас додано до листа очікування»** (You have been added to the waiting list) window is shown with the text «На занятті немає вільних місць. Вас додано до листа очікування.» (The class has no free seats. You have been added to the waiting list.) and the class details (when the studio has the automatic move from the waiting list switched on, «Після звільнення місця Вас буде записано автоматично.» (Once a seat becomes free, you will be booked automatically.) is added to the text); the booking gets the **Waiting list** status. No administrator confirmation is required; the studio receives the «Запис до листа очікування» notification.

| Condition | Result |
|---|---|
| The class has already started | The client is not added: «Заняття вже розпочалося, запис до листа очікування недоступний» (The class has already started; joining the waiting list is not available). |
| The client is already on the wait list of this class | A second place is not added: «Ви вже перебуваєте в листі очікування на це заняття» (You are already on the waiting list for this class). |
| The class is cancelled | The client is not added: «Заняття скасовано» (The class is cancelled). |
| The client has no booking on this class, or has a booking with the status **Canceled**, **Missed**, **Registration canceled** or **Left the waiting list** | Joining the wait list is allowed; the existing booking gets the **Waiting list** status. |
| The client has a booking on this class with the status **Planned**, **Attended** or **Paused** | The client is not added to the wait list, the existing booking is not changed: «Ви вже записані на це заняття» (You are already booked for this class). |
| A seat is free at the moment of confirmation | The client is booked into the free seat, as with the **«Book»** button. |

- When the studio has the automatic move from the waiting list switched on, while the wait list of a workout is not empty, a new booking by the client for that workout gets the **Waiting list** status and joins the end of the queue, even if the workout has a free seat. When the automatic move is off, the free seat goes to the client who books first, whether or not there are clients on the wait list.
- A client on the wait list does not take a seat in the workout's seat count.
- **Leaving the wait list:** card menu → **«Leave the wait list»** → the **«Leave the wait list»** window: «Leave the wait list for this class? Your place in the queue will be released.» → **«Continue»**. Result — «You have left the wait list»; error — «Could not leave the wait list. Try again or contact the studio.» The client's history gets an entry with the **Left the waiting list** status.
- If automatic moving from the waiting list is enabled in the studio settings, when a seat frees up on a workout that has not started, the first client in the queue automatically gets the **Planned** (Заплановано) status and a message about the booking — as a push notification, or through Telegram or SMS if push notifications do not reach the client (see [Schedule — Waiting list](/en/menu/schedule#waiting-list)). If automatic moving is off, the studio administrator changes the status of a client on the waiting list.

---

## 7.5.6 Coach Schedule

- The schedule shows all studio workouts for the selected day; the **«My workouts»** filter — only the coach's workouts.
- The **«Add schedule to calendar»** button subscribes the phone calendar to the coach's schedule. On iOS the subscription opens in the device calendar, on other devices in Google Calendar.
- The coach calendar link is unique and cannot be derived from the studio and coach identifiers. After the system update the link changes: a subscription to the previous link keeps updating for 30 more days and then stops updating. A coach subscribed to the calendar must subscribe again — with the **«Add schedule to calendar»** button or with the **«Subscribe to the new calendar»** button in the notification.
- Every coach receives the notification «The class calendar link has been updated. If you are subscribed to the calendar, tap «Subscribe to the new calendar» to keep the schedule updating.» once, with the **«Subscribe to the new calendar»** button.
- The card of an own workout shows the number and names of clients by status: **Planned**, **Attended**, **Not attended**, **Canceled**, **Wait list** (rows with zero are not shown), and **«Spots left:»** and **«Credited to coach:»**. For a regular workout — «Repeats every: {days}». For a rental — the **«Rent»** badge.

---

## 7.5.7 Creating a Workout (Coach / Admin)

The **«Create»** button is available to an administrator and a coach; to a coach — only for today and future days. On a studio day off the button is not shown.

The **«New class»** screen (with the date of the selected day):

1. **Admin** selects the **Coach** (the **«Select a coach»** window with search) and sets the **«Personal»** switch («One participant»). A coach creates only a personal workout.
2. Choose a room and a time — free time slots are grouped by room. If there are no slots — «Cannot create a workout on the selected day».
3. **«Selected client(s)»** → **«Add client»** — the **«Select a client»** window with search. Selected clients are shown as chips; tapping a chip removes the client.
4. **Category** — the **«Select a category»** window; if there is one category, it is selected automatically.
5. The button suggests the next step («Choose a hall and a time», «Add a client», «Choose a category») and, once everything is filled in, becomes **«Create · {room}, {time}»**.
6. The **«Create workout»** window shows the room, coach, date, time and clients → **«Continue»**.
7. Result — **«Done»**: «Workout created successfully».

The created workout is named «Personal workout (app)» or «Workout (app)».

> ⚠️ If the slot in this room has just been taken, the error window «🙀 🙀 🙀 Darn!!! Someone just created a workout in this hall at the selected time 🤬🤬🤬» is shown with the **«Got it»** button.

---

## 7.5.8 Workout Actions (Coach / Admin)

The gear button on the card opens the **«Workout actions»** window. For a coach, actions are available for their own upcoming workouts; for an administrator — for all upcoming workouts not cancelled by the studio.

- **«Change time»** — free time slots → **«Save»** → the **«Change workout time»** confirmation (with the new time). Result — «Workout time changed». Empty — «No available time slots».
- **«Change room»** — free rooms → **«Save»** → the **«Change workout room»** confirmation (with the new room). Result — «Workout room changed». Empty — «No available rooms».
- **«Cancel workout»** — the **«Cancel workout»** window with the class details → **«Cancel workout»**. Result — «Workout canceled»; error — «Could not cancel the workout. Try again.» The cancellation day is determined in the studio time zone. If the class on this date is already cancelled, the date is not a day the series runs on, or the cancellation is not executed, the error is shown and the workout state does not change. Booked clients receive a cancellation message (see [Messages to clients](/en/pages/processing#_614-messages-to-clients)).

---

## 7.5.9 Booking a Client by the Administrator

In the **«Workout actions»** window of an upcoming, not cancelled workout the administrator has the **«Book a client»** switch.

1. Turn on **«Book a client»**.
2. **«Select a client»** — a list with search; clients busy at this time are not shown. Clients on this workout's wait list are highlighted in blue with the **«(waitlist)»** mark. An empty list — «No available clients».
3. For a regular workout the **«Repeat»** switch is available — booking for the series.
4. **«Book»** → confirmation in the **«Workout booking»** window.
5. Result — **«Done»**: «Client booked successfully».

The administrator books a client also for a workout without free seats.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

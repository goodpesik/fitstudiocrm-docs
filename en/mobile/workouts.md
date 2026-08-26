<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.5 Classes

> The **Classes** tab is the main working screen. The client books and cancels bookings; the coach and admin see the schedule and can create classes and book clients.

<!-- TODO: screenshot of the Classes tab (client) -->

---

## 7.5.1 Choosing a Day

- At the top — the date picker **"Choose a day"** ("Виберіть день"). You can also switch days by swiping the screen left or right, or with the ‹ › buttons next to the title.
- The available date range depends on the role:
  - **Client:** from today to **+15 days**.
  - **Coach / Admin:** up to **+30 days** (admin can also look a few days into the past).
- Title **"Classes for: {date}"** ("Тренування на: {дата}").
- On the studio's day off, instead of the create button, **"The studio is closed this day"** ("В цей день у студії вихідний") is shown.

---

## 7.5.2 Booking a Class (Client)

The client has two tabs: **"My Classes"** ("Моі тренування") (their bookings for the selected day) and **"Book"** ("Записатися") (all classes available for booking).

### Statuses on the Class Card

On the **"My Classes"** tab, each card has a status:

| Status | Meaning |
|---|---|
| **Planned** | active booking (can be cancelled) |
| **Visited** | class attended |
| **Cancelled** | booking cancelled |
| **Paused** | booking paused |
| **Waiting List** | you are in the queue (no spots yet) |

On the **"Book"** tab, the card shows whether you can book:

- **"book"** (green) — the class is available, tap to book it.
- **"you are already booked for this class"**, **"no spots available"**, **"you have another booking at this time"**, **"booking not available"** (past), **"cancelled"**, **"paused"** — cannot book.

<!-- TODO: screenshot of a class card with the "book" status -->

### How to Book

1. Go to the **"Book"** tab and select a day.
2. Find a class with the **"book"** status and tap it (or tap the menu icon → **"Book a Class"** ("Записатися на тренування")).
3. In the **"Class Booking"** ("Запис на тренування") window, check the details (class, coach, room, date, time) → **"Continue"** ("Продовжити").
4. A confirmation appears: **"Booking confirmed"** ("Запис записано на тренування").

> If there are no available classes on the selected date — **"No classes available for booking"** ("Немає жодного тренування доступного для запису").

> ⚠️ If while you were deciding someone else took the spot — on confirmation you'll see **"This class is no longer available for booking"** ("Запис на це тренування більше не доступний").

### Waiting List

> When all spots are taken, the class shows **"no spots available"**. If the studio uses a waiting list, your booking may get the **"Waiting List"** status — when a spot frees up, the administrator can move you to confirmed.

### How to Cancel a Booking

1. On the **"My Classes"** tab, find a booking with the **"Planned"** status.
2. Tap the menu icon on the card → **"Cancel Booking"** ("Скасувати запис").
3. In the **"Class Cancellation"** ("Відміна тренування") window, confirm → **"Continue"** ("Продовжити").
4. **"Booking cancelled"** ("Запис на тренування скасовано") appears.

> ⚠️ **A late cancellation deducts the class.** If you cancel later than the time before the start set by the studio (the [minimum time to cancel a class](/en/login/settings#minimum-time-before-workout-cancellation) parameter), the class will be deducted from the membership as **"Not Attended"**. Check with the studio for how much time you have to cancel free of charge.

> ℹ️ A deduction from the membership is not shown at the moment of booking. The remaining classes are visible on [Home](/en/mobile/home) and in [Account](/en/mobile/account) (membership card and the **History** tab).

> ℹ️ **Recurring classes:** automatic booking for the next class in a series happens the day after the current class's date.

---

## 7.5.3 Coach's Schedule

> A coach sees the **"My Classes"** and **"Schedule"** tabs.

- **"My Classes"** — the coach's classes for the selected day. Empty → **"You have no classes on this day"** ("В вас немає тренувань у цей день").
- **"Schedule"** — all of the studio's classes for the day.
- The **"Add Schedule to Calendar"** ("Додати розклад у календар") button adds the coach's schedule to their phone's own calendar (Apple Calendar / Google Calendar).

For the coach, the class card shows a summary by client: **Planned**, **Visited**, **Cancelled**, **Not Attended**, **Waiting List**, **"Spots remaining"** ("Місць лишилося"), and **"Credited to coach"** ("Зараховано тренеру").

---

## 7.5.4 Creating a Class (Coach / Admin)

> The **"Create Class"** ("Створити тренування") button is available to the coach and admin (except on the studio's days off).

1. **Admin** first selects a coach (**"Choose Coach"** ("Виберіть тренера") → **"Select Coach"** ("Вибрати тренера")) and, if needed, turns on the **"Personal"** ("Персональне") toggle.
2. Choose a **free time slot** — they are grouped by room.
3. Add clients: **"Choose Client"** ("Виберіть клієнта") → **"Add Client"** ("Додати клієнта"). Selected clients appear as chips under **"Selected Client(s)"** ("Вибраний(і) клієнт(и)") (clients already booked at that time are not available).
4. Choose a **category** (**"Choose Category"** ("Виберіть категорію")); if there is only one category, it is selected automatically.
5. **"Create Class"** ("Створити тренування") → in the **"Class Creation"** ("Створення тренування") window, check the room, coach, date, time, and clients → **"Continue"** ("Продовжити").
6. **"Class created successfully"** ("Тренування успішно створено") appears.

> ⚠️ If the slot in this room was just taken — an error appears stating the time is already taken. Choose a different slot.

---

## 7.5.5 Changing the Time / Room and Cancelling a Class (Coach / Admin)

> On the card of an upcoming class, the coach (for their own classes) and the admin have these actions available:

- **"Change Time"** ("Змінити час") — choose another free time slot → **"Save"** ("Зберегти") → confirm. Empty → **"No time slots available"** ("Немає доступних часових слотів").
- **"Change Room"** ("Змінити зал") — choose another free room → **"Save"** ("Зберегти") → confirm. Empty → **"No rooms available"** ("Немає доступних залів").
- **"Cancel Class"** ("Відмінити тренування") — cancels the class for everyone booked (**"Class cancelled"** ("Тренування скасовано")).

---

## 7.5.6 Booking a Client as Administrator

> On the card of an upcoming class, the admin has a **"Book Client"** ("Записати клієнта") toggle.

1. Turn on the **"Book Client"** ("Записати клієнта") toggle.
2. **"Choose Client"** ("Виберіть клієнта") — clients unavailable (booked at that time) are not shown; clients on the **waiting list** are highlighted in blue with the label **"(waiting list)"** ("(лист очікування)"), so the admin can confirm them.
3. For a recurring class, you can turn on the **"Repeat"** ("Повторювати") toggle — the booking will repeat across the series.
4. **"Book"** ("Записати") → confirm in the **"Class Booking"** ("Запис на тренування") window.
5. **"Client booked successfully"** ("Клієнта успішно записано") appears.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

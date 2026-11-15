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
- **"Join the waiting list"** ("Стати в лист очікування") — the class has no free spots; tap it to take a place on the waiting list (see [Waiting List](#waiting-list)).
- **"no spots available"** — the class has no free spots while a class is chosen in a registration request to the studio; the waiting list is not available in this mode.
- **"you are already booked for this class"**, **"you have another booking at this time"**, **"booking not available"** (past), **"cancelled"**, **"paused"** — cannot book.

<!-- TODO: screenshot of a class card with the "book" status -->

### How to Book

1. Go to the **"Book"** tab and select a day.
2. Find a class with the **"book"** status and tap it (or tap the menu icon → **"Book a Class"** ("Записатися на тренування")).
3. In the **"Class Booking"** ("Запис на тренування") window, check the details (class, coach, room, date, time) → **"Continue"** ("Продовжити").
4. A confirmation appears: **"Booking confirmed"** ("Запис записано на тренування").

> If there are no available classes on the selected date — **"No classes available for booking"** ("Немає жодного тренування доступного для запису").

> ⚠️ If while you were deciding someone else took the spot — on confirmation you'll see **"This class is no longer available for booking"** ("Запис на це тренування більше не доступний").

### Waiting List

When all spots are taken, the class card on the **"Book"** tab shows the **"Join the waiting list"** ("Стати в лист очікування") button.

1. Tap **"Join the waiting list"**.
2. In the **"Joining the waiting list"** ("Запис до листа очікування") window, tap **"Continue"**.
3. The app shows the **"You have been added to the waiting list"** window; the booking gets the **"Waiting List"** status. No administrator confirmation is required; the studio receives the **"Запис до листа очікування"** notification.

Limits:

| Condition | Result |
|---|---|
| The class has already started | the client is not added: **"Заняття вже розпочалося, запис до листа очікування недоступний"** |
| The client is already on the waiting list of this class | a second place is not added: **"Ви вже перебуваєте в листі очікування на це заняття"** |
| The class is cancelled | the client is not added: **"Заняття скасовано"** |
| The client has an entry on this class with a status other than **"Cancelled"** (for example, **"Planned"** or **"Attended"**) | the client is not added to the waiting list, the existing entry is not changed: **"Ви вже записані на це заняття"** |
| A spot is free at the moment of confirmation | the client is booked into the free spot, as with the **"Book"** button |

> A place on the waiting list is not counted as a taken spot. When a spot frees up on a class that has not started, the first client in the queue automatically gets the **"Planned"** status and a message about the booking — as a push notification, or through Telegram or SMS if push notifications do not reach the client. While the waiting list of a class is not empty, a new booking for that class gets the **"Waiting List"** status and joins the end of the queue, even if the class has a free spot If the booking got the **"Waiting List"** status, the app shows the **"You have been added to the waiting list"** window instead of **"You are booked for the workout"** (see [Schedule — Waiting list](/en/menu/schedule#waiting-list)).

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

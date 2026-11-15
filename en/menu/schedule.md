<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.1 Schedule

> The **Schedule** ("Розклад") tab

![](../../_media/schedule-main.png ':size=400x241')

> The schedule is displayed as a calendar. By default, the current week is shown in the general view.

## Schedule toolbar

**Elements:**

- **Month calendar** ("Календар місяця") — the button opens a panel with the current month's calendar to the left of the grid; days with scheduled workouts are marked. Picking a day in the panel shows that day or week. The panel is closed with the **Hide calendar** ("Сховати календар") button. The panel state is remembered on this computer. On screens narrower than 900 px the panel is not shown.
- **Filter** ("Фільтрувати") — display filters:

![](../../_media/scedule-filter.png ':size=300x181')

  - **Room** ("Зал") — workouts held in the selected rooms (taking a room change for a specific date into account).
  - **Coach** ("Тренер") — workouts of the selected coaches (taking a coach substitution for a specific date into account); rentals are shown regardless of the coach filter.
  - **Workout type** ("Тип тренування") — Regular, Personal, Rent.

- **Day** / **Week** ("День" / "Тиждень") — the grid view (general view only).
- **General** / **By coach** / **By room** ("Загальний" / "По тренеру" / "По залу") — the schedule breakdown. The **By coach** and **By room** breakdowns show one day: a separate column for each coach leading a workout that day (taking substitutions into account) or for each room. Workouts without a coach (rentals) are shown in the **Без тренера** (no coach) column. The selected breakdown is remembered on this computer.
- **Collapse parallel workouts** ("Згортати паралельні тренування") — shown for the **Week** view in the general breakdown when the studio has three rooms or more. Values: **Не згортати** (do not collapse) or a number from 2 to (number of rooms − 1) — how many simultaneous workouts a cell shows side by side; the rest are collapsed under the "+N · Деталі" button, which opens the **Заняття в цей час** (classes at this time) window with the list of workouts. The default is 2. The value is remembered on this computer.
- The «<<» and «>>» buttons on either side of the date picker — go to the previous / next week (in the **Day** view and in the **By coach** / **By room** breakdowns — to the previous / next day). Picking a date shows the week (day) containing it.
- **Download PNG** ("Завантажити PNG") — downloads an image of the week's schedule with the selected filters applied.
- **Studio closures** ("Вихідні студії") — see [Studio closures](#studio-closures).

The grid shows the studio's working hours; the current time is marked by a red line with the time (when it falls within the grid hours). The **Нагору** (to top) button returns a scrolled grid to the top. If a day has no workouts, "Цього дня тренувань немає" (no workouts this day) is shown, or "Немає тренувань за фільтром" (no workouts for the filter) when the workouts are hidden by the filters.

---

## Workout card

![](../../_media/schedule-card.png ':no-zoom')

> A workout card contains:

- The workout name.
- The workout time.
- The coach's name, or **Оренда** (rent). If a coach substitution is set for the date, the name of the main coach and the name of the substitute are shown.

The card colour is the coach's colour, and for a workout without a coach — the room's colour.

> For the SuperAdmin and Admin roles, hovering over a grid cell (empty or with a workout, if the cell belongs to the current day or a future time) shows the **Запланувати** (schedule) button. It opens a choice of **Тренування** (workout) or **Оренда** (rent); the **Оренда** button is available only while a shift is open (tooltip "Відкрийте зміну для створення оренди", open a shift to create a rental).

![](../../_media/add-workout.png ':size=150x100')

[More about creating a workout](/en/menu/workouts#_331-create-a-workout)

---

## Workout window

> Clicking a workout card opens a modal window with details and actions. If the workout from a link is not found, "Тренування не знайдено" — "Схоже, його скасували або перенесли." (workout not found, it was probably cancelled or moved) is shown.

![](../../_media/schedule-card-details.png ':size=420x253')

**Window header:**

- The workout name.
- Badges: **workout type** (group / personal / rent). Regular workouts additionally have the **Регулярне** (regular) badge and "Відбувається: <weekdays>" (takes place on).
- The **Go to workout** ("Перейти до тренування") button — opens the [Workouts](/en/menu/workouts) page on this workout.
- The **Cancel workout** ("Скасувати тренування") button — see [Cancelling a workout](#cancelling-a-workout).
- The **Workout settings** ("Налаштування тренування", gear icon) button — see [Workout settings](#workout-settings).

**Workout information:**

- The coach's avatar and name (the avatar is shown if set in the [coach card](/en/menu/coaches#_341-coach-card)). If a substitution is set for the date, the main coach's name is crossed out and the substitute's name is shown next to it.
- For a regular workout — "Дата тренування: <date>" (workout date) and the time.
- "Зал: <name>" (room, taking a room change into account).

**Counters:**

| Field | What it counts |
|---|---|
| **Запланували відвідати** (planned to attend) | Clients with the **Planned** status. |
| **Резерв місць** (reserved spots) | Clients with a booking repeat set who will be booked automatically. Shown for future recurring workouts that have no bookings created for the date yet. |
| **Місць лишилося** (spots left) | The workout capacity minus clients with the **Planned** and **Visited** statuses; for a future recurring workout — also minus the reserved spots. Shown when a capacity is set and the workout can be changed. |
| **Відвідано** (visited) | Clients checked in to the workout (**Visited** status). |
| **Відмінено** (cancelled) | Clients with the **Cancelled** status. |
| **Не відвідано** (not visited) | Clients with the **Not visited** status. |
| **Зараховано тренеру** (credited to the coach) | How many clients / workouts will be credited to the coach for payroll, taking the [minimum and maximum settings](/en/login/settings#features) into account. |

### Cancelling a workout

- The **Cancel workout** button opens the [confirmation window](../_modals/are-you-sure-modal.md ':include'). After confirmation, "Тренування успішно оновлено" (workout updated) is shown.
- For a regular workout only this date is cancelled; a one-time workout is deleted.
- The button is disabled when at least one client is checked in, and is not shown for an already cancelled workout.
- Booked clients are sent a class cancellation notice, see [Client notifications](#client-notifications).

### Book a client

> The **Book a client** ("Записати клієнта") toggle shows the **Choose a client** ("Виберіть клієнта") field.

![](../../_media/schedule-card-details-2.png ':size=400x241')

> after selecting

![](../../_media/new-client-1.png ':size=300x181')

- The **Duplicate booking** ("Дублювати запис", for a regular workout) toggle sets the booking to repeat automatically. When the workout has no free spots, the label is extended with "(Лист очікування НЕ дублюється)" (the waiting list is not duplicated).
- If several following workouts are full, the **Обмеження повтору** (repeat restriction) window with the **Записати з <date>** button is shown; if no following workout has free spots — the **Неможливо поставити повтор** (cannot set a repeat) window.
- The **Confirm booking** ("Підтвердити запис") button books the client for the workout.
- The **Waiting list** ("Лист очікування") button — shown when there are no free spots; adds the client to the waiting list.

> The **New client** ("Новий клієнт") button in the picker opens the **New client** window with the **Прізвище** (surname) and **Імʼя клієнта** (first name, required) fields; the created client is booked for the workout at once.

![](../../_media/add-client-select.png ':size=400x241')
![](../../_media/new-client-2.png ':size=100x59')

> ℹ️ A client who repeats only on some weekdays (for example, Tuesday) has the **Paused** status on other days (for example, Thursday). The administrator can book them once through the **Choose a client** field: the status for that date changes to **Planned** without changing the repeat.

### Workout settings

![](../../_media/schedule-card-details-3.png ':size=400x241')

> The gear button opens a panel with actions on the workout for this date:

- **Edit** ("Редагувати") — a toggle for a past workout; allows changing client bookings and statuses on a past workout. Without it a past workout is view-only.
- **Coach substitution** ("Заміна тренера") — a coach picker; after selection the **Зберегти заміну тренера** (save substitution) button appears. When a substitution is active, the **Видалити заміну** (remove substitution) button is available. Not shown for a rental.

  ![](../../_media/substitute-2.png ':size=300x181')
- **Room change** ("Заміна Зала") — a room picker; the **Зберегти заміну залу** (save room change) button. If all rooms are taken at this time, "На цей час всі зали зайнято. Ви можете зробити перерозподіл залів" (all rooms are taken, you can redistribute rooms) and the **Зробити перерозподіл залів** (redistribute rooms) button are shown.
- **Change workout time** ("Змінити час тренування") — choosing a new time within this date; the **Зберегти зміни** (save changes) button.
- **Change workout category** ("Змінити категорію тренування") — choosing a category (affects the coach's pay for this session); the **Зберегти заміну категорії** (save category change) button.

> All these actions apply **only to the specific date**; the recurring workout template is not changed. The template is changed on the [Workouts](/en/menu/workouts) page.

### Clients

> Booked clients are shown at the bottom of the window as badges. A client with a debt for this workout has an icon with the tooltip "Борг за це тренування" (debt for this workout). Clicking a badge opens the client's action panel.

**Statuses and badge colours:**

| Colour | Status | Description |
|---|---|---|
| Primary | **Planned** ("Заплановано") | The client is booked but not checked in yet. |
| Green | **Visited** ("Відвідано") | The client has been checked in to the workout. |
| Red | **Cancelled** ("Відмінено") | The booking is cancelled. |
| Purple | **Not visited** ("Не відвідано") | The client did not come or cancelled later than allowed; a session has been deducted from the plan. |
| Blue | **Waiting list** ("Лист очікування") | The client is on the waiting list. |
| Orange | **Reserved** ("Резерв") | A future automatic booking of a [client with a booking repeat](/en/menu/clients#_328-booking); shown only for future workouts. |

**Client action panel:**

- **Go to client** ("Перейти до клієнта") — opens the [client table](/en/menu/clients#_321-client-table) with this client.
- "Поточний статус: <status>" (current status).
- **Check in client** ("Зареєструвати клієнта") — opens [Registration](/en/menu/clients#_329-registration); available for a workout of the current day with an open shift, if the client is not checked in yet and not on the waiting list.
- **Cancel check-in** ("Відмінити реєстрацію") — for a checked-in client with an open shift.
- **Change status** ("Змінити статус") — a choice of a new status (**Заплановано**, **Відвідано**, **Відмінено**, **Не відвідано**, **Лист очікування**; the current status is not in the list) or **Видалити клієнта з тренування** (remove the client from the workout), and the **Зберегти** (save) button. After the change, "Статус оновлено" (status updated) is shown. Removal requires confirmation ("Ця опція повністю видаляє запис про клієнта на цьому тренуванні.", this option removes the client's booking for this workout completely); for a repeating booking the options **Видалити тільки з цього заняття** (remove from this session only) and **Видалити з цього і всіх наступних** (remove from this and all following) are offered.

For a past workout without the **Edit** toggle on, and for a cancelled workout, status actions are not available.

> ℹ️ A client on the waiting list is not moved to a booking automatically: when a spot frees up, the administrator changes their status to **Planned**.

### Reserved spots

For future dates of a recurring workout with clients booked with a repeat, reserved spots are shown — the clients who will be booked for the workout automatically. The number of free spots is shown with the reserve taken into account.

![](../../_media/schedule-card-details-4.png ':size=70x88')
![](../../_media/schedule-card-details-5.png ':size=70x82')
![](../../_media/schedule-card-details-6.png ':size=70x82')
![](../../_media/schedule-card-details-7.png ':size=70x87')

**`Important! If at least one client is already checked in for the workout, it cannot be cancelled.`**

---

## Client notifications

> When a class is cancelled, a client's booking is cancelled, a class is rescheduled, or a booking is confirmed, the system notifies the client.

The channels are checked in this order; the message is sent through the first one available:

1. Push notification in the mobile app — if the client uses the app.
2. The studio's Telegram bot — if the client has connected the bot.
3. The Fitshandler Telegram account — to the phone number from the client card.
4. SMS — only if the corresponding SMS kind is enabled in the [settings](/en/login/settings).

- The texts of the class-cancellation and booking-cancellation messages are set in the [settings](/en/login/settings); Telegram messages additionally contain the workout name and a link to the app.
- SMS length is not limited: a long text is sent as several SMS.
- Sent messages are recorded in the [Reports → SMS](/en/menu/reports#_387-sms) report.

---

## Studio closures

> The **Studio closures** ("Вихідні студії") button on the schedule toolbar opens a panel for managing the days when the studio is closed (holidays, technical breaks, etc.).

### How to add a closure

1. Click **Studio closures**.
2. Click **Add exception** ("Додати виключення") — a row with the **День коли студія не працює** (day the studio is closed) field appears.
3. Choose a date (not earlier than today).
4. Add other dates if needed.
5. Click **Save** ("Зберегти").

![](../../_media/schedule-holidays-popover.png ':size=300x181')

### What happens on save

- A background task starts (the [background tasks modal](/en/pages/processing#_65-background-tasks) is shown).
- All workouts on the selected dates are **cancelled** automatically; client bookings get the **Cancelled** status.
- The list of closures is saved in the studio settings. Closure days are not marked in the month calendar.

### How to remove a closure

1. Open the **Studio closures** panel.
2. Click **Delete** (trash icon) on the row with the relevant date.
3. Click **Save**.

> ⚠️ Removing a closure **restores** the workouts and bookings for that date — also via a background task.

> ℹ️ Past dates remain in the list; only dates from today onward can be selected.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

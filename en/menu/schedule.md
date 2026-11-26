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
- For a regular or personal workout — "Дата тренування: <date>" (workout date) and the time.
- "Зал: <name>" (room, taking a room change into account).

**Counters:**

| Field | What it counts |
|---|---|
| **Запланували відвідати** (planned to attend) | Clients with the **Planned** status. |
| **Резерв місць** (reserved spots) | Clients with a booking repeat set who will be booked automatically. Shown for future recurring workouts that have no bookings created for the date yet. |
| **Місць лишилося** (spots left) | The workout capacity minus clients with the **Planned** and **Visited** statuses; for a future recurring workout — also minus the reserved spots. Clients with the **Waiting list** status do not take up spots. Shown when a capacity is set and the workout can be changed. |
| **Відвідано** (visited) | Clients checked in to the workout (**Visited** status). |
| **Відмінено** (cancelled) | Clients with the **Cancelled** status. |
| **Не відвідано** (not visited) | Clients with the **Not visited** status. |
| **Лист очікування** (waiting list) | Clients with the **Waiting list** status. If automatic moving is enabled in the studio settings, when a spot frees up the first client in the queue is moved to the **Planned** status automatically, see [Waiting list](#waiting-list). |
| **Зараховано тренеру** (credited to the coach) | How many clients / workouts will be credited to the coach for payroll, taking the [minimum and maximum settings](/en/login/settings#features) into account. |

### Cancelling a workout

- The **Cancel workout** button opens the [confirmation window](../_modals/are-you-sure-modal.md ':include'). After confirmation, "Тренування успішно оновлено" (workout updated) is shown.
- For a regular workout only this date is cancelled; a one-time workout is deleted.
- The cancellation day is determined in the studio time zone ([Studio Time Zone](/en/login/settings#studio-time-zone)), regardless of the time zone of the computer the action is made from. The calendar day selected in the schedule is cancelled.
- The success message is shown only when the workout is actually cancelled. In the other cases no exception is recorded, the workout state does not change, and the system shows a message:

| Situation | Message |
|---|---|
| The workout on the selected date is already cancelled | «Заняття на обрану дату вже скасовано.» (The class on the selected date is already cancelled.) |
| After the cancellation the workout on the selected date does not have the «Скасовано» (cancelled) status | «Не вдалося скасувати заняття на обрану дату. Спробуйте ще раз.» (Could not cancel the class on the selected date. Try again.) |
| The selected date is not a day the series runs on (the series weekday within the repeat period) | «Заняття не проводиться в обрану дату.» (The class does not run on the selected date.) |
| A request without a date | «Не вказано дату заняття.» (The class date is not specified.) |
| A request to cancel one date of a one-time workout | «Заняття не є регулярним.» (The class is not recurring.) |
| The workout is not found (for example, it was deleted) | «Заняття не знайдено.» (The class is not found.) |
- The button is disabled when at least one client is checked in, and is not shown for an already cancelled workout. A prepayment does not affect whether the button is available.
- A personal training prepayment is credited to the client's personal account under the rules of [Personal training prepayment](#personal-training-prepayment).
- Booked clients are sent a class cancellation notice, see [Client notifications](#client-notifications).

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

The **Make a prepayment** button in the window first checks the prepayment on the server; only after a successful check does a card payment go through the terminal. Then a sale is recorded on the register: a transaction of the **Personal training prepayment** type is created, a fiscal receipt is issued. The prepayment amount is added to the amount paid for the training when the transaction is saved. A bank transfer is added to the amount paid for the training at once, before the transfer is confirmed in the register. The cash-operations record of a cash prepayment is created after the transaction is saved; when the transaction is not saved, no record is created.

From the server check until the transaction is saved, the prepayment amount is held on the training: other prepayments for this training cannot exceed the remaining amount together with the hold. The hold is removed when the transaction is not saved, and stops counting 10 minutes after it was created.

If the server refuses the prepayment during the check, the terminal is not called and the system shows the reason. With a split payment the sum of all payments is checked together: when it exceeds **Left to pay**, the system shows the message **Сума перевищує неоплачену частину вартості тренування** (The amount exceeds the unpaid part of the training price), and no payment is made. If with a split payment some payments are saved and a following payment is not, the system shows the sum of the saved payments and reports only the card payments for which no transaction was created.

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
- When the client holds a plan with a duration and that plan covers the prepaid training at [registration](/en/menu/clients), the prepayment is credited automatically to the client's personal account. A plan covers the training when it is active or not yet started, has a duration, is of the **Personal** type or has no type, and its validity period contains the training date (a plan whose start date is no later than one day after the training also covers it). The client must be booked on the training with the **Planned** or **Visited** status; the prepayment of a client with the **Не відвідано** (Not visited) status is not credited. The amount paid for the training is reduced by the credited amount.
- A cash or card prepayment is credited to the personal account as a top-up. A prepayment from the personal account goes back to the personal account as a refund. In the personal account history the operation is described as **Повернення передоплати за персональне тренування** (Prepayment returned for a personal training).
- A bank-transfer prepayment is credited to the personal account only when the transfer has been confirmed in the register. An unconfirmed transfer is cancelled together with the training or with the client leaving it: nothing is credited to the personal account, the register shows the payment status **Скасовано** (Cancelled), and the transfer cannot be confirmed afterwards.
- When the client who made a prepayment is deleted from the system, the prepayment stays an open transaction in the register and can be refunded through the register.
- A register refund of a prepayment transaction reduces the amount paid for the training. A prepayment already credited to the personal account cannot be refunded through the register. A refund and a credit of the same prepayment cannot run at the same time: the second operation sees the result of the first.
- The **Change payment method** action in the register is available for a prepayment transaction not yet credited to the personal account and without refunds, except a prepayment from the personal account. The change is one operation on the server: the server checks the old transaction (an open prepayment of this client for this training, without refunds, not from the personal account) and the new one, records the new transaction first, then refunds the old one. When the check fails, the payment method is not changed. When the new transaction is recorded and the refund of the old one fails, the new transaction stays and the system shows the message **Передоплату за новим методом оплати проведено, але попередню операцію не повернуто. Виконайте її повернення вручну.** (The prepayment by the new payment method is recorded, but the previous operation is not refunded. Refund it manually.); the old transaction is refunded through the register. When no server answer is received, the system shows the message **Не вдалося змінити метод оплати передоплати. Перед повторною спробою перевірте операції каси.** (The payment method of the prepayment could not be changed. Check the register operations before trying again.) The new transaction stays a prepayment for the same training, including after the training has started. The credit rules on cancel follow the new payment method: for a bank transfer, only once the transfer is confirmed.

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

- Without internet a client is booked for a class in the offline till by the rules of [Offline mode](/en/pages/offline-mode#class-registration-and-new-clients).

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

> ℹ️ If automatic moving is enabled in the studio settings, when a spot frees up a client on the waiting list is moved to the **Planned** status automatically, see [Waiting list](#waiting-list).

### Waiting list

- A client with the **Waiting list** status does not take up a spot. The number of free spots is calculated the same way on the server, in the client app, on the public schedule and in the admin window: `workoutCapacity − (Planned + Attended)`.
- The queue is served in the order clients joined the waiting list: the client who joined earlier is moved first. A client who returns to the waiting list joins the end of the queue.
- The automatic move from the waiting list is performed only when the **Автоматично переводити клієнтів із листа очікування в запис (після звільнення місця на тренуванні)** (Automatically move clients from the waiting list into a booking (when a place on the workout becomes free)) toggle is on in [Settings → Features](/en/login/settings#features). The toggle is off by default. The rules of the automatic move and the messages about it described in this section apply only when the toggle is on.
- When the toggle is off, clients stay on the waiting list until an administrator changes their status manually. When a spot frees up on a workout that has not started and is not cancelled and the waiting list is not empty, the studio receives the notification «Звільнилося місце на тренуванні!» (a spot has freed up on the workout) with the workout details (workout, coach, time, room).
- When a spot frees up on a workout that has not started and is not cancelled (a booking is cancelled, a client is removed from the workout, a status changes from **Planned** or **Attended** to another one, the capacity is increased), the system automatically moves the first client on the waiting list to the **Planned** status. This repeats while free spots and waiting clients remain.
- If the move did not happen right after the spot freed up, the spot is given to the first client on the waiting list within 5 minutes: every 5 minutes the system checks the workouts that have not started and start no later than 30 days ahead, and performs the move on every workout with a free spot and a non-empty waiting list.
- If the move of a particular client fails, that client stays on the waiting list and the free spot is given to the next client in the queue.
- The move applies to this workout only: the client's bookings on other dates, including those made by a repeat setting, do not change. The same plan and change-log rules apply as for a manual status change by an administrator. The change log names «система» (system) as the author.
- No automatic move is performed for a workout without a set capacity, or for a workout that has started, has ended or is cancelled.
- Each client is moved from the waiting list at most once. The automatic move never makes the number of clients with the **Planned** and **Attended** statuses exceed the workout capacity, including when several spots free up at the same time.
- With the switch on, while the waiting list of a workout is not empty, a new booking for that workout (from the app, from the web page, a restored cancelled booking, a client added by an administrator with the **Planned** status) gets the **Waiting list** status and joins the end of the queue, even if the workout has a free spot. The free spot is given to the first client on the waiting list. A manual status change by an administrator for a client already on the workout is not subject to this rule.
- With the switch off, a new booking for a workout with a free spot (from the app, from the web page, a restored cancelled booking, a client added by an administrator with the **Planned** status) gets the **Planned** status whether or not there are clients on the waiting list. The free spot goes to the client whose booking is made first.
- After the move the client receives the push notification «Звільнилося місце: Вас переведено з листа очікування та записано на тренування.» (in English: "A place has become available: you have been moved from the waiting list and booked for the workout."). A client whom push notifications do not reach receives «<studio name> - Вас записано на тренування <date>.» (in English: "<studio name> - You are booked for <date>.") through the cascade: the studio Telegram bot → the Fitshandler Telegram account → SMS. An SMS is sent only if SMS sending is enabled for the studio and the limit is not used up.
- The studio receives the notification «Клієнта переведено з листа очікування на тренування» (client moved from the waiting list to the workout) with the client and workout details.
- A client who already has the **Planned** or **Attended** status on a workout keeps this status when booked for the same workout again (added again by an administrator, a request approved again) and is not moved to the waiting list.
- A client whose booking got the **Waiting list** status instead of **Planned** receives the following message:

| Where the booking comes from | Message to the client |
|---|---|
| The client app | A window with the heading «Вас додано до листа очікування» (in English: "You have been added to the waiting list"), the text «Вільні місця на цьому занятті першочергово надаються клієнтам з листа очікування. Вас додано до листа очікування.» and the workout details. The «Вас записано на тренування» message is not shown. |
| The client app, the «Стати в лист очікування» ("Join the waiting list") button on a class with no free places | A window with the heading «Вас додано до листа очікування» (in English: "You have been added to the waiting list"), the text «На занятті немає вільних місць. Вас додано до листа очікування.» (in English: "The class has no free places. You have been added to the waiting list.") and the workout details; with the automatic move on, «Після звільнення місця Вас буде записано автоматично.» (in English: "Once a place becomes free, you will be booked automatically.") is added to the text. No administrator confirmation is required. The studio receives the «Запис до листа очікування» notification with the client and workout details. Joining is not available for a class that has already started or is cancelled, for a client who is already on the waiting list of this class, and for a client who has an entry on this class with the status **Planned**, **Attended** or **Paused** (the message «Ви вже записані на це заняття», in English: "You are already booked for this class"). A client with no entry on this class, or with an entry with the status **Cancelled**, **Not Attended**, **Registration Cancelled** or **Left the waiting list**, may join the waiting list (see [App — Wait List](/en/mobile/workouts#_755-wait-list)). |
| The app, a client booked by an administrator | The window «Клієнта додано до листа очікування.» (in English: "The client has been added to the waiting list.") |
| The studio public page | «Вас додано до листа очікування. Вільні місця на цьому занятті першочергово надаються клієнтам з листа очікування.» (in English: "You have been added to the waiting list. Free places in this class are offered first to clients on the waiting list.") |
| Approval of a request from the public page | Instead of «<studio name> - Вас записано на тренування <date>.» the client receives «<studio name> - Вашу заявку прийнято. Вас додано до листа очікування на тренування <date>.» (in English: "<studio name> - Your request has been accepted. You have been added to the waiting list for the workout on <date>."); when automatic moving is on, «Після звільнення місця Вас буде записано автоматично та повідомлено.» (in English: "Once a place becomes available, you will be booked automatically and notified.") is added to the text. The message is sent through the cascade: the studio Telegram bot → the Fitshandler Telegram account → SMS. |
| An administrator changes the status to **Waiting list** | The push notification «Вас додано до листа очікування на тренування.» (in English: "You have been added to the waiting list for the workout."). A client whom push notifications do not reach receives «<studio name> - Вас додано до листа очікування на тренування <date>.» through the same cascade. When automatic moving is on, «Після звільнення місця Вас буде записано автоматично та повідомлено.» (in English: "Once a place becomes available, you will be booked automatically and notified.") is added to both texts. If the client returned to the waiting list herself in the app, no message is sent. |

- An SMS in the cascade is sent only if SMS sending is enabled for the studio and the limit is not used up.
- A failure to send a message does not cancel the move.

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

### If the save does not complete

The list of closures and the workout schedule of those days are saved together. A save has exactly two results: saved, or not saved.

| State | Message | Workout schedule | List of closures |
|---|---|---|---|
| Saved | — | Changed for the selected dates | The selected list |
| The request is refused | **Вихідні дні не збережено** (closures not saved) | Unchanged | Saved list |

- In the **Вихідні дні не збережено** state the panel and the calendar show the saved list of closures and the workout schedule stays unchanged. Clicking **Save** again sends the save anew.
- There is no state in which the workout schedule is changed and the list of closures is not saved.
- **Save** is unavailable while a save is in progress. At most one save of the closures runs at a time; clicking during a save sends no requests and does not change the panel.
- Reloading the page during a save does not affect its result.
- Saving the same list of closures again does not change the workout schedule a second time.

### How to remove a closure

1. Open the **Studio closures** panel.
2. Click **Delete** (trash icon) on the row with the relevant date.
3. Click **Save**.

> ⚠️ Removing a closure **restores** the workouts and bookings for that date — also via a background task.

> ℹ️ Past dates remain in the list; only dates from today onward can be selected.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

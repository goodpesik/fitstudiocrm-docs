[Back to home](/en/)

# 6. Information on How the System Processes Workout Visits, Plan Deductions, Reminders, and More

## 6.1 Workout Recurrence

> If a workout repeats, the system automatically creates a workout instance in the calendar on the repeat date.

> The nightly job (every night) creates, for every held session of a regular workout, the next session according to the repeat schedule. Clients with a recurring booking are carried over to the next session with the **Заплановано** (Planned) or **Призупинено** (Paused) status (see [6.8](#_68-client-vacation-and-the-paused-status)).

``` Example: a workout takes place on Tuesdays and Thursdays. A client is booked with a repeat. The workout took place on Tuesday. The next night the system creates the client's booking for the same workout on Thursday.```

## 6.2 Deducting Workout Visits

> On registration for a workout with an active membership, the system deducts from the membership the number of workouts equal to the number selected for attendance.

> The nightly job sets bookings of past sessions that are still **Заплановано** to **Не відвідано** (Not visited). For each such session, **1 workout** is deducted from the active membership of the matching type (personal — for a personal workout, regular — for the others). If there is no active membership, the session is marked unpaid.

> If a client cancels a booking later than the [Minimum Time Before Workout Cancellation](/en/login/settings#minimum-time-before-workout-cancellation) allows, the workout is also deducted from the membership as **Не відвідано**.

---

## 6.3 Calculating Coach Salaries

> The system takes all of the coach's workouts for the selected period, groups them **by workout category** (the category assigned to the workout) and calculates by the rate type of **that category**.

> ℹ️ **All calculation parameters (rate type and base rate) are set only on the workout category** ([Settings → Categories](/en/login/settings#categories)). There are no individual rates for a coach or for a single workout.

- **Rate type «За людину»** (Per person, `PerPerson`)
  For each workout of the category, the number of clients with the `Visited` status and clients with the `Unvisited` status from whom a workout was deducted (late cancellation) is counted. If the number is below the **Minimum Number of Clients** ([Settings → Features](/en/login/settings#features)), the minimum is used. If it exceeds the workout's maximum number of people and the **Враховувати максимальну к-сть людей при підрахунку зарплат** switch is on, it is capped at the maximum. Sum over workouts × the category base rate = salary for the category.

- **Rate type «За тренування»** (Per workout, `PerWorkout`)
  The number of workouts of the category for which the coach is paid is counted: sessions attended by at least one client, and sessions without clients that had late cancellations with a membership deduction. Number of workouts × the category base rate = salary for the category.

> Total salary = the sum over all categories in which the coach had workouts during the period.

---

## 6.4 Calculating Administrator Salaries

> Salary = `hours worked × hourly rate` + the sum of bonuses accrued for the period.

- **Hours worked** — the sum of hours of all the administrator's closed [shifts](/en/menu/reports#_382-shifts) in the selected period.
- **Hourly rate** — set for each user on the [Users](/en/login/users) page (field **Ставка за годину**, Hourly rate).
- **Bonuses** — accrued by the rules in [Settings → Features → Administrator Bonuses](/en/login/settings#administrator-bonuses) to users with the **Нараховувати бонуси** switch on.
- **The total** is shown on the [Reports → Administrator payroll](/en/menu/reports#_385-administrator-payroll) page.

---

## 6.5 Background Tasks

> Some actions start a **background task** on the server: they update a large number of records and take from a few seconds to a few minutes. While the task runs, a progress modal is open.

**Actions that start a background task:**

- Adding or removing a date in **[Studio closures](/en/menu/schedule#studio-closures)** — the system goes through all regular workouts, adds or removes an exception for the date and moves dependent bookings to «Відмінено» (Cancelled) or back to «Заплановано».
- **Очистити тренування** (Clear workouts) ([Settings → Settings](/en/login/settings#settings)) — deletes all workouts not yet held and unsubscribes clients.

**Progress modal:**

- The title states the task type (for example, «Оновлення вихідних студії», Updating studio closures).
- The progress bar shows `X / N` processed items.
- The modal cannot be closed until the task finishes.
- After completion the **Закрити** (Close) button appears; the data on the current page is reloaded.

> ⚠️ Closing the browser tab does not stop the task on the server, but the result is not shown in the interface automatically.

---

## 6.6 Class reminders

Reminders are sent in two independent ways.

### The in-app reminder, set by the client

A client with the app and the **Нагадування** (Reminders) notification type on chooses how many hours in advance to be reminded — in [Notifications](/en/mobile/notifications), from 1 to 24 hours. The reminder arrives as an app notification.

### The reminder for clients without the app, set by the studio

Clients without the app are covered by the studio's **Нагадувати про візит** (Remind about the visit) setting on the [Mobile Application](/en/login/settings#mobile-application) tab (from 0 to 24 hours, `0` — off). The setting applies when the studio's mobile app is on. The channel is chosen in the order described in [6.14](#_614-messages-to-clients): Telegram bot, Fitshandler Telegram account, SMS. An SMS reminder is sent only when the **SMS-нагадування про візит** (SMS visit reminder) switch is on; the switch is off by default. After a reminder sent in Telegram, the client receives a second message «Встановіть додаток Fitshandler <link>» (Install the Fitshandler app).

> ⚠️ The studio setting does not apply to clients with the app.

### The night pause

Reminders are not sent **from 23:00 to 06:00** in the studio time zone, on every channel: the app, Telegram and SMS.

- A reminder whose calculated time falls between 22:00 and 23:00 is sent at **22:00**. Example: a "1 hour before" reminder for a 23:30 session falls at 22:30 and arrives at 22:00.
- A reminder whose calculated time falls inside the night pause is sent at **06:00**, once, if the session has not started yet. Example: a "2 hours before" reminder for a 07:30 session falls at 05:30 and arrives at 06:00.
- A reminder for a session that starts during the night pause is sent only when its calculated time comes before 23:00; otherwise no reminder is sent. Example: a "2 hours before" reminder for a 02:00 session falls at 00:00 and is not sent.
- A reminder not sent on its due hourly run is sent on the next run outside the night pause, provided the session has not started. A reminder about the same session is not sent to the same client twice.
- Rating requests are not sent during the night pause — see [Ratings and Reviews](/en/mobile/ratings).
- The app message about an automatic removal from a recurring booking (see [6.9](#_69-removal-from-a-recurring-booking-after-misses)) is not sent during the night pause: it arrives on the first hourly run after the pause, at 06:00.
- The app message «Закінчується дія абонементу(ів)» (membership expiring) is not sent during the night pause: it arrives on the first hourly run after the pause, at 06:00.
- A message held for the night pause is sent once. If sending fails, it is retried on the following hourly runs. After 6 failed attempts, or 24 hours after it was created, the message is not sent.

### The monthly SMS limit

The limit is **shared by all of the studio's SMS**: reminders, app login codes and confirmation codes for guests, messages about cancellations and moves, booking confirmations and rating requests. The limit is counted in SMS parts (a long message takes several SMS) and is defined by the studio's plan. Telegram messages do not count towards the limit.

When the limit is used up, SMS are not sent; login codes and guest booking confirmation codes are sent only through Telegram. If the code cannot be delivered through Telegram, the app shows «Наразі неможливо надіслати код SMS-повідомленням. Спробуйте пізніше.» (The code cannot be sent by SMS right now. Try again later.) Usage is shown under the **Нагадувати про візит** field.

---

## 6.7 Membership expiry

The nightly job ends a membership if its end date has passed (the last day included, in the studio time zone) or all workouts are used. «Оренда» (Rent) memberships end only by date.

Every day at 12:00 (UTC) the client receives the app notification «🔔🔔🔔 Нагадування про абонемент» (Subscription reminder) about an active membership (except «Оренда») when one of the conditions is met:

| Condition | Notification line |
|---|---|
| No more than 1 workout left, and the membership was bought for more than 1 workout | «<name>. Залишилось тренувань: N.» (Workouts left: N.) |
| The last valid day of the membership is today or at most 3 calendar days after today (days are counted in the studio time zone) | «<name>. Термін дії закінчується DD.MM.YYYY.» (Valid until DD.MM.YYYY.) |
| Both conditions are met | Both parts in one line |

- The notification is sent **once** per membership. A visit, an extension or a change of the workout count does not create a repeated notification for the same membership.
- A single-visit membership (bought for 1 workout) gets no workout-count notification; only the end-date condition applies to it.
- The number of workouts a membership was bought for is taken from the membership template; without a template, from the largest workout count recorded when the membership was activated.
- The notification is not sent if the client already has the next purchased membership.
- If the app server does not accept the notification, it is retried the next day.
- Clients without the app do not receive it.

---

## 6.8 Client vacation and the Paused status

When the nightly job creates the next session of a regular schedule and the date falls into the [client's vacation](/en/menu/clients#_3282-client-vacation), the booking is created with the **«Призупинено»** (Paused) status. No workout is deducted from the membership and no place is taken.

---

## 6.9 Removal from a recurring booking after misses

If **Пропусків підряд** (Misses in a row) is set in [Settings → Features](/en/login/settings#features), a client who missed the given number of sessions in a row is removed from the recurring booking automatically. The administrator receives the notification «Клієнт … автоматично знятий з повторного запису: … (N пропусків підряд)» (Client … automatically removed from the recurring booking: … (N misses in a row)), and the client receives an app notification. After that the client is booked manually.

---

## 6.10 Automatic registration on card scan

Applies when the **Автоматична реєстрація при скануванні картки (клієнт з активним абонементом і записом на сьогодні)** switch is on in [Settings → Features](/en/login/settings#features).

When a card is scanned, the **Реєстрація** (Registration) window opens with stages:

1. «Пошук клієнта…» (Searching for the client…)
2. «Реєстрація клієнта…» (Registering the client…)
3. «Клієнта успішно зареєстровано» (Client registered successfully) — with the **Тренування** (Workout), **Час** (Time), **Зал** (Room) lines and the **OK** button.

The window cannot be closed while a stage is running.

**Conditions for automatic registration** (all required):

- the client has no debt;
- a booking for today with the **Заплановано** status for a workout that has not ended yet; rent is not counted;
- an active membership of the matching type (personal — for a personal workout, regular — for the others) with more than 0 workouts left, **or**, with no active one, a single new membership of the matching type with more than 0 workouts left (it will be activated);
- the registration requires no payment (amount due — 0).

**Result:**

| Situation | Behaviour |
| --- | --- |
| One booking meets the conditions | The client is registered and the membership deducted; message «Клієнта <full name> зареєстровано на <workout> о <time>» (Client … registered for … at …). The client receives an app notification. |
| Several bookings meet the conditions | The **Автоматична реєстрація** (Automatic registration) window: «Клієнт <full name> має кілька записів на сьогодні. На яке тренування зареєструвати?» (The client has several bookings today. Which workout to register for?) — a button for each booking («time · name»), **Скасувати** (Cancel), **Відкрити реєстрацію** (Open registration). |
| Conditions not met or saving failed | The regular [Registration](/en/menu/clients#_329-registration) form opens with the booking preselected. |

A repeated scan while a registration is running shows «Зачекайте» (Please wait) — «Ще триває реєстрація попереднього клієнта. Відскануйте картку ще раз за мить.» (The previous client's registration is still running. Scan the card again in a moment.) A scan with the registration window open shows «Вікно реєстрації відкрите» (The registration window is open) — «Закрийте його, щоб зареєструвати іншого клієнта.» (Close it to register another client.)

---

## 6.11 Self check-in by QR code

Applies when **Реєстрація через мобільний застосунок** (Registration through the mobile app) is on in the [Mobile Application](/en/login/settings#mobile-application) tab.

**Reception banner.** The **Показати банер** (Show banner) button opens a page with the studio name, the selected rooms (or «Усі зали», All rooms) and a QR code with the caption «Відскануйте камерою телефону, щоб відмітитись на тренуванні» (Scan with your phone camera to check in for the workout). The code changes at the start of every hour; the previous code stays valid for 10 more minutes. An expired code gives «QR-код застарів. Відскануйте той, що зараз на екрані на рецепції.» (The QR code is out of date. Scan the one currently on the reception screen.) The banner must be opened on a screen at the reception (for example, a tablet); a printed or photographed code is not accepted.

**Registration by the client.** The client scans the code with the phone camera and sees the **Реєстрація на тренування** (Workout registration) window in the app: the workout, the membership («Абонемент: <name>»), the remaining balance after registration. The **Підтвердити** (Confirm) button registers the client: status **Відвідано** (Visited), the workout is deducted from the membership. Message: «Вас успішно зареєстровано на тренування «<name>»» (You have been registered for the workout). The administrator receives the notification «Самореєстрація в застосунку на тренування» (Self check-in in the app for the workout).

**Conditions:**

- the client has no debt; otherwise — «Автоматична реєстрація неможлива, зверніться до адміністратора студії» (Automatic registration is not possible, contact the studio administrator);
- the membership follows the same rules as for [automatic registration](#_610-automatic-registration-on-card-scan); a new membership is activated («Абонемент буде активовано цим тренуванням», The membership will be activated by this workout);
- a workout today, until it ends; rent is not counted;
- the workout room is one of the banner rooms; otherwise — «У вас є тренування сьогодні, але в іншому залі: <rooms>.» (You have a workout today, but in another room);
- with **Реєстрація тільки з записом** on — only workouts the client is booked for; off — today's schedule workouts with free places (except personal and rent);
- a free place is checked at the moment of registration: «На тренуванні вже немає вільних місць» (There are no free places left on the workout).

**Several clients on one phone number.** If several clients of the studio are linked to the number, the app shows the choice «Кого відмітити?» (Whom to check in?). After registration the **Обрати іншого клієнта** (Choose another client) and **Відмітити ще когось** (Check in someone else) buttons are available.

**Other app messages:** «Сьогодні немає тренувань, на які ви записані» (No workouts you are booked for today), «Сьогодні немає доступних тренувань для реєстрації» (No workouts available for registration today), «Ви вже зареєстровані на це тренування» (You are already registered for this workout), «Ви ще не клієнт цієї студії. Зверніться до адміністратора студії» (You are not a client of this studio yet. Contact the studio administrator), «Студію за цим QR-кодом не знайдено» (No studio found for this QR code), «Увійдіть у застосунок, щоб зареєструватися на тренування за QR-кодом студії.» (Sign in to the app to register for a workout by the studio QR code).

---

## 6.12 Card payment without a terminal

The **Картка** (Card) payment method is available at the Cash Register, in the [Registration](/en/menu/clients#_329-registration) window, when paying a debt and in the workout form.

- If the device manager is on and a POS terminal is registered ([Settings → Integrations](/en/login/settings#integrations)), the hint «Термінал доступний — оплата пройде через нього при підтвердженні» (Terminal available — the payment will go through it on confirmation) is shown, and the amount is sent to the terminal.
- Otherwise the card payment is recorded immediately as a sale with the **Картка** method without terminal data.

With an active fiscal integration, a card payment is fiscalized as a regular sale; a receipt without a terminal contains no terminal data.

---

## 6.13 Debts

A debt is created when **Сплатити пізніше** (Pay later) is on in the registration or sale window, and by the [no-show debt at a personal workout](/en/login/settings#features) rule.

- **Сплатити пізніше:** the sold membership or product is recorded as the client's debt for the amount due; a registration without a membership creates the debt «Борг за тренування: <name>» (Debt for the workout). No cash register operation and no fiscal receipt are created when the debt is created.
- **Paying a debt** ([Clients → Client debt](/en/menu/clients#_3212-client-debt)): creates a sale in the current shift and is fiscalized at the moment of payment (with an active fiscal integration). A payment from the personal account is not fiscalized. The debt is closed when the whole amount is paid; an amount larger than the debt is rejected with «Сума перевищує борг» (The amount exceeds the debt).
- While the client has a debt, automatic registration and self check-in by QR code are not performed; the registration window shows «Увага!!! У клієнта є борг: <amount>» (Attention!!! The client has a debt).

---

## 6.14 Messages to clients

Messages to clients are sent through the first available channel in this order:

1. **Mobile app notification** — if the client installed the app and allowed notifications.
2. **The studio Telegram bot** — if the client card is linked to one Telegram bot chat.
3. **The Fitshandler Telegram account** — a message from the Fitshandler account to the phone number on the client card, if the number is registered in Telegram.
4. **SMS** — paid, if the Telegram account did not deliver the message, the matching SMS switch is on, the card has a phone number and the [monthly limit](#the-monthly-sms-limit) is not used up.
5. **The studio Telegram bot in one of the chats** — if the client card is linked to several different Telegram bot chats and neither the Telegram account nor the SMS delivered the message.
6. If no channel is available, the message is not sent.

| Message | Channels | Condition for SMS |
| --- | --- | --- |
| Visit reminder | App — by the client's setting; without the app — Telegram bot → Telegram account → SMS | **Нагадувати про візит** greater than 0 and **SMS-нагадування про візит** |
| Session cancelled | App → Telegram bot → Telegram account → SMS | **SMS про відміну заняття** |
| Booking cancelled by the studio | App → Telegram bot → Telegram account → SMS | **SMS про скасування запису** |
| Session moved | App → Telegram bot → Telegram account → SMS | **SMS про перенесення заняття** |
| Confirmation of a web page booking | App → Telegram bot → Telegram account → SMS | **SMS про підтвердження запису** |
| Confirmation code for a guest | Telegram bot → Telegram account → SMS | — |
| Request to rate the session | App → Telegram bot → Telegram account → SMS; sent to any channel only with both **Пропонувати оцінити заняття** and **Пропонувати оцінити заняття в смс (для клієнтів без застосунку)** on | **Пропонувати оцінити заняття в смс (для клієнтів без застосунку)** |
| Move from the waiting list | App → Telegram bot → Telegram account → SMS | — |
| Membership expiry | App only | — |
| Message from the studio | App only | — |

Login codes and guest booking confirmation codes have no separate switch. The app and Telegram do not depend on the SMS switches, except the session rating switches, and are not counted in the SMS limit.

**Cancellation, booking cancellation and moves.** Changes to one session are collected over a few seconds into one message: each client receives one message per session about the nearest date. If a session was moved and then cancelled, only the cancellation message is sent. A Telegram message additionally contains the workout name («Тренування: <name>») and a link to the app.

**Message length.** SMS texts set by the studio are not truncated; a long message is billed as several SMS (see [Message texts](/en/login/settings#sms-notifications)). Telegram messages are sent as one message without splitting.

**Telegram bot.** The bot is used as a delivery channel for app login codes and messages; signing in through the bot is not available in the app. Details — [Telegram bot](/en/login/telegram-bot).

[Back to home](/en/)

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.3 Workouts

> The **Workouts** page

![](../../_media/workouts-page.png ':size=200x121')

---

## 3.3.1 Create a workout

> The **Create workout** ("Створити тренування") button (SuperAdmin and Admin roles) opens the **Add workout** ("Додати тренування") modal window:

![](../../_media/add-workout-1.png ':size=200x121')

**Fields:**

- **Name** ("Назва") — required.
- The **Personal** ("Персональне") toggle — sets the type to "Personal".
- The **Regular** ("Регулярне") toggle — defines whether the workout repeats.
- **Date** ("Дата", for a non-regular workout) — not earlier than today.
- **Choose a day** ("Вибрати день", for a regular workout) — weekdays; at least one day must be selected ("Необхідно вибрати день").
- **Start** ("Початок") — the workout start time.

> For a non-regular workout, the date and time are required.

![](../../_media/add-workout-2.png ':size=200x121')

> For a regular workout, the day(s) and time are required.

![](../../_media/add-workout-3.png ':size=200x121')

> After the date and time are added or the days are selected, additional fields appear:

![](../../_media/add-workout-4.png ':size=100x100')

- **Workout duration (min)** ("Час тренування (хв)") — required, from 1 to 720.
- **Coach** ("Тренер")
- **Room** ("Зал")
- **Maximum number of people** ("Максимальна кіл-сть людей на тренуванні")
- **Category** ("Категорія") — required, chosen from the list (categories are created in [Settings → Categories](/en/login/settings#categories)).
- The **Show on the web page** ("Показувати на веб сторінці") toggle — whether the workout is shown on the studio's public web page; in the mobile app the workout stays available regardless of the toggle. On by default.

> If the workout conflicts with others, a message appears at the bottom of the form.  
> In that case, coaches and rooms with conflicts are excluded from the lists.

**Example:**  
The studio has 3 rooms (**Room 1**, **Room 2**, **Room 3**) and 3 coaches (**Coach 1**, **Coach 2**, **Coach 3**).  
**Coach 1** has a workout on Tuesday at 12:00 in **Room 2**.  
When creating another workout at the same time, a conflict message will be shown.  
Only **Coach 2**, **Coach 3**, **Room 1** and **Room 3** will remain available.

---

![](../../_media/add-workout-5.png ':size=100x106')

> A regular workout has:

- **Тренування почне відбуватися з:** (the workout starts on) — the start date of the repeats (on creation).
- **Повторювати тренування до:** (repeat the workout until) — the **Вибрати дату** (choose a date) toggle. When on, a limit date is chosen: sessions are created up to it, not on the date itself. The end date must be later than the start date ("Дата завершення має буде більшою за дату початку"). Turning the toggle off clears the field and the workout repeats without a limit.
- **Exceptions** ("Виключення") — the **Додати виключення** (add exception) button adds a **День коли тренування не відбудеться** (day the workout will not take place) field.

---

![](../../_media/add-workout-6.png ':size=100x103')

> A personal workout has additional fields:

- **Choose a client** ("Виберіть клієнта") — the client who will be booked for the workout automatically. The **New client** ("Новий клієнт") button opens the **New client** window with the **Прізвище** (surname) and **Імʼя клієнта** (first name, required) fields.
- **Choose a plan** ("Виберіть абонемент") — the plan that will pay for the workout at check-in.

Window buttons: **Close** ("Закрити"), **Save** ("Зберегти").

---

## 3.3.2 Renting a room

![](../../_media/rent.png ':size=100x60')

> The **Room rent** ("Оренда Зала") button opens the **Оренда Зала** window. The button is available only while a shift is open (tooltip "Відкрийте зміну для створення оренди", open a shift to create a rental).

- The form is similar to workout creation, but has fewer fields.
- A client (**Choose a client**) and a plan for payment (**Choose a plan**) are required.
- After a plan is chosen, the payment block is shown (payment method, discount, **Сплатити пізніше** (pay later), **До сплати** (to pay)); the amount due equals the plan price.

---

## 3.3.3 Filters

> Filters above the table:

- **Filter** ("Фільтр", by time): **Всі** (all), **Майбутні** (future), **Минулі** (past), **Регулярні** (regular).
- **Type** ("Тип"): **Всі** (all), **Групові** (group, default), **Персональні** (personal), **Оренда** (rent), **Не активні** (inactive).
- **Coach** ("Тренер") — a coach picker; the filter can be cleared.

> ℹ️ Going to a workout from other sections (for example, the **Go to workout** button in the [schedule workout window](/en/menu/schedule#workout-window)) shows the table with this workout only: instead of the filters, "Показано 1 тренування" (1 workout shown) and the **Show all** ("Показати всі") button are displayed.

---

## 3.3.4 Search

> Search is by workout name.

---

## 3.3.5 Workouts table

> The table contains:

- **Name** — a past workout has the **Минуле** (past) badge.
- **Coach**
- **Duration**
- **Room**
- **Day**
- **Time**
- **Type** — **Персональне** (personal), **Оренда** (rent) or **Звичайне** (regular group).
- **Category** — the category name or **Без категорії** (no category).
- **Actions** (SuperAdmin and Admin roles):
  - **Delete** — available for an inactive or past workout; for others — the tooltip "Деактивуйте тренування щоби видалити" (deactivate the workout to delete it). Deletion requires confirmation; afterwards "Тренування успішно видалено" (workout deleted) is shown.
  - **Edit**
  - **Change history** ("Історія змін")

If no workouts are found, "Не знайдено жодного тренування" is shown.

### Change history

The **Change history** button (clock icon) opens the window "Історія змін — <workout name>" with the workout's change log. The button is available in the workouts table and in the edit form.

| Column | Content |
|---|---|
| **Дата/час** (date/time) | Time of the change |
| **Хто змінив** (changed by) | User |
| **Тип** (type) | **Шаблон** (a change to the workout itself) or **Заняття** (a change to the session on a specific date) |
| **Поле** (field) | Name of the changed field (for example, **Статус**, **Статус оплати**, **Клієнт**, **Тренер**) |
| **Було** / **Стало** (before / after) | Values before and after the change |

If there are no changes, "Змін не зафіксовано" is shown.

---

**Sorting is available by:**

- Name
- Coach
- Room
- Day
- Category

---

## 3.3.6 Editing

> Editing opens the **Edit workout** ("Редагувати тренування") window (for a rental — **Редагування Оренди Зала**) with the same fields as creation, with restrictions.

![](../../_media/edit-workout-1.png ':size=100x60')

**Fields that cannot be changed:**

- The **Personal** and **Regular** toggles (the workout type does not change).
- The **Choose a client** field (for a personal workout the client is changed by cancelling and booking again).
- The **Date** field (for a non-regular workout the date is changed through [Schedule → Workout settings → Change workout time](/en/menu/schedule#workout-settings)).

**Fields that can be changed:**

- Name, duration, coach, room, maximum number of people, category, **Show on the web page**, schedule (for regular ones — days, time, "Повторювати тренування до:", exceptions).
- The **Active** ("Активне") toggle — deactivates the workout, see [3.3.7](#_337-deletion).

**Additional buttons:** **Create a duplicate** ("Створити дублікат") — opens the new-workout form with the data of the current one (without exceptions, with the start date from today); **Change history**.

![](../../_media/edit-workout-change.png ':size=100x50')

> If the days of a regular workout, the date or the time are changed and clients are already booked for the nearest session, a warning with the number of booked clients is shown on save. After confirmation, the clients are booked for the new date automatically and get a Telegram notification (if they connected the bot).

---

## 3.3.7 Deletion

> A workout can be deleted only after it is deactivated (the **Active** toggle in the edit form) or once it has become past.  
> Deactivation is not possible if the workout takes place today or has attendees ("Деактивація неможлива, якшо тренування відбудеться сьогодні aбо має відвідувачів").

![](../../_media/edit-workout-2.png ':size=100x37')

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

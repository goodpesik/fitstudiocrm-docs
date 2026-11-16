<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.4 Coaches

![](../../_media/coaches-1.png ':size=200x70')

## 3.4.1 Coach card

> A coach card contains:

- **Name**
- **Avatar** (if uploaded; otherwise the default one is used)
- **Rating** — the coach's average score (a star, the value and the number of ratings in brackets). Shown when the coach has been rated at least once; see [Reports → Rating](/en/menu/reports#_386-rating).
- "Телефон: <number>" (phone)
- **Buttons** (SuperAdmin and Admin roles):
  - **Delete** — disabled when the coach has workouts (tooltip "Неможливо видалити. У тренера існують тренування", cannot delete, the coach has workouts). Deletion requires confirmation; afterwards "Тренера успішно видалено" (coach deleted) is shown.
  - **Edit** — opens the **Edit coach** ("Редагувати тренера") window.

> Next to the add button the plan limit is shown: "Тренери: N / L · ще M" (coaches: used / limit · M left) or "Тренери: N · без ліміту" (no limit), see [Plan and access](/en/login/billing).

---

## 3.4.2 Add a coach

> The "+" button above the list of cards (SuperAdmin and Admin roles) opens the **Add coach** ("Додати тренера") modal window:

![](../../_media/coach-2.png ':size=150x90')

**Contains:**

- Avatar upload — an image of up to 5 MB ("Зображення завелике. Дозволено завантажувати зображення до 5 МБ", image too large); an uploaded photo is removed with the **Видалити фото** (delete photo) button.
- **Name** ("Імʼя") — required, at least 3 characters.
- **Phone** ("Телефон") — required, format `0XXXXXXXXX`.
- **Choose the coach's colour in the calendar** ("Виберіть колір тренера в календарі") — a required choice from a palette of light shades (a 7×5 grid). The colour is used for the coach's workout cards in the [schedule](/en/menu/schedule). A colour saved before the palette existed is shown as the nearest palette shade.
- **Birthday** ("День народження") — optional.

Buttons: **Close** ("Закрити"), **Save** ("Зберегти").

> ℹ️ **Coach payroll calculation:**
> All payroll parameters (rate, calculation type `PerPerson` / `PerWorkout`) are defined **on the workout category** ([Settings → Categories](/en/login/settings#categories)), not on the coach card. The coach card has neither a category choice nor a rate.
>
> More details: [Information about visit processing, membership deductions and reminders](/en/pages/processing)

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

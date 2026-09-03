<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.6 Account

> The **Account** tab is the user's profile. The set of sub-tabs depends on the role.

<!-- TODO: screenshot of the Account tab -->

| Sub-tab | Client | Coach | Admin |
|---|:---:|:---:|:---:|
| **Profile** | ✔ | ✔ | ✔ |
| **Memberships** | ✔ | — | — |
| **History** | ✔ | — | — |
| **Balance** | ✔ | — | — |
| **Statistics** | — | ✔ | — |
| **About the App** | ✔ | ✔ | ✔ |

---

## 7.6.1 Profile

- **"My Information"** ("Моя інформація"): name, phone, date of birth.
- **Client:** the **"Edit Details"** ("Редагувати дані") button enables editing → **"Save"** ("Зберегти") (name and date of birth can be changed; phone number cannot).
- **Coach:** photo/avatar upload. If there is no photo — **"No Photo"** ("Немає фото"); if there is — avatar and **"Delete Photo"** ("Видалити фото"). Size limit — up to 10 MB (**"Image too large…"** ("Зображення завелике…")).
- **Admin:** phone number and date of birth are hidden.
- **"Log Out"** ("Вихід") — signs out of the account (confirmation **"Are you sure you want to continue?"** ("Ви впевнені що хочете продовжити?")).

---

## 7.6.2 Memberships (Client)

> Cards for active memberships:

- **"Membership:"** ("Абонемент:") + name.
- **"Classes remaining: {N}"** ("Тренувань лишилося: {N}"), **"Valid through {date}"** ("Діє до {дата} включно").
- New membership — **"Not active. Activates on your visit to the studio"** ("Не активний. Активується під час візиту в студію").
- Warning **"Membership is about to expire"** ("Абонемент скоро закінчує дію") (fewer than 3 days / 3 classes).
- **"Single-visit passes: {N}"** ("Разові абонементи: {N}") — number of single-visit passes.
- Empty → **"No current membership"** ("Немає поточного абонемента").

---

## 7.6.3 History (Client)

> History of deductions/transactions on memberships for the selected period.

- Date range filter, table with pagination (10/20/50 rows).
- Each row: date, membership, **"Classes remaining:"** ("Залишок тренувань:"), status (**Planned / Cancelled / Registration Cancelled / Not Attended / Visited / Added to Waiting List**), **"Created:"** ("Створено:"), class, coach.
- Empty → **"No transactions found"** ("Не знайдено жодної транзакції").

---

## 7.6.4 Personal Balance / "Balance" (Client)

> The client's personal monetary balance (wallet).

- **"Personal Balance"** ("Особовий рахунок") + current balance in UAH.
- History table with pagination. Transactions: **"Top-up"** ("Поповнення") (green), **"Refund"** ("Повернення") (blue), **"Deduction"** ("Списання") (red, with a minus sign).
- Empty → **"No transactions"** ("Немає транзакцій").

> ℹ️ The studio tops up the balance in the [POS](/en/menu/pos). In the app, the client can only view the balance and history.

---

## 7.6.5 Statistics (Coach)

> Summary of the coach's earnings for the selected period.

- Date range filter, **"Total:"** ("Всього:") amount + UAH.
- For each category: **"Amount:"** ("Сума:"), **"Total classes: {N}"** ("Всього тренувань: {N}"), **"Credited to coach: {N}"** ("Зараховано тренеру: {N}"), **"Visited: {N}"** ("Відвідано: {N}"), **"Not attended: {N}"** ("Не відвідано: {N}"), **"Cancelled: {N}"** ("Відмінено: {N}").

---

## 7.6.6 About the App

- **"Version: {version}"** ("Версія: {версія}").
- **"Development"** ("Розробка") → fitshandler.com, **"Contacts:"** ("Контакти:") → fitshandler@gmail.com.
- **"For issues and suggestions about the app, please reach out"** ("З проблемами та пропозиціями щодо роботи додатку, звертайтеся") → Telegram.
- **Admin** additionally sees **"Registered in the app:"** ("Зареєстровано у додатку:") — **"Clients: {N}"** ("Клієнтів: {N}"), **"Coaches: {N}"** ("Тренерів: {N}").

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

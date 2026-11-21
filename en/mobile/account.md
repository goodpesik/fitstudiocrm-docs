<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.6 Account

> The **Account** tab contains the profile card (initials, name, role and studio), the list of sections and the **«Log out»** button. The set of sections depends on the role.

| Section | Customer | Coach | Admin, Guest |
|---|:---:|:---:|:---:|
| **Profile** | ✔ | ✔ | ✔ |
| **Plans** | ✔ | — | — |
| **History** | ✔ | — | — |
| **Balance** | ✔ | — | — |
| **Statistics** | — | ✔ | — |
| **About** | ✔ | ✔ | ✔ |

A section opens as a separate page; the **«Cabinet»** button at the top returns to the list.

**«Log out»** — logs out of the account after the confirmation «Are you sure you want to continue?».

---

## 7.6.1 Profile

- Fields: **First name** and **Last name** (for a client; for other roles — a single **Name** field), **Phone**, **Date of birth** (format dd/mm/yyyy). For an administrator the phone and the date of birth are not shown.
- **Client:** the **«Edit data»** button turns on editing → **«Save»**. The first name, last name and date of birth can be changed; the phone is changed only by the studio.
- **Coach:** the **«Photo»** block. Without a photo — «No photo» and image selection; with a photo — the image and the **«Delete photo»** button. Image size — up to 10 MB; larger — «Image is too large. You can upload images up to 10 MB».

### Deleting Data

The **«Delete my data»** button opens a window with the text «This permanently deletes your account and data from the app. Your records at the studio remain. Continue?».

1. In the field «Enter your phone number to confirm», the account phone number must be entered (format `+380XXXXXXXXX`). If the number does not match — «This is not the account phone number».
2. The **«Delete my data»** button becomes active after the correct number is entered; **«Cancel»** closes the window. The window does not close on a tap outside it.
3. After deletion the user is logged out of the app. Error — «Could not delete the data. Please try again»; if no studio is selected — «Choose the studio whose data should be deleted, then try again».

---

## 7.6.2 Plans (Client)

Cards of active and new plans:

- **«Plan»** and the status **Active** or, for a new plan, **New**;
- the plan name; «A plan of {N} workouts» if the number is not part of the name;
- **«Workouts remaining: {N}»**, **«Valid until {date} inclusive.»**;
- the warning «The plan is expiring soon» — fewer than 3 workouts or fewer than 3 days left.

Tapping a card opens the **History** section. The **«One-time plans»** row shows the number of one-time plans. If there are no plans — «No current plan».

---

## 7.6.3 History (Client)

Operations on plans and bookings for the selected period (date range selection, not later than today; by default, from the same day a week ago to today). The period days follow the studio time zone. Rows are loaded 10 at a time; the **«Show more»** button loads the next ones.

Each row: operation date and time, workout name, status, workout date and time and the coach, **«Plan:»** {name}, **«Left:»** {number of workouts} (for attended and missed workouts on a plan, plan activation and plan cancellation), **«Created by:»** {who created it}.

| Status | Meaning |
|---|---|
| **Planned** | booking for a workout |
| **Attended** | the workout was attended |
| **Missed** | the workout was not attended |
| **Canceled** | the booking was cancelled |
| **Registration canceled** | the registration at the workout was cancelled |
| **Waiting list** | the client was added to the wait list |
| **Left the waiting list** | the client left the wait list |

Empty — «No transactions found».

---

## 7.6.4 Balance (Client)

The client's personal balance.

- **«Balance»** — the current balance in UAH.
- **«Operations»** — rows 10 at a time, the **«Show more»** button. Each row: the operation name (or a description set by the studio), date and time, the amount with a sign.

| Operation | Sign |
|---|---|
| **Top-up** | + |
| **Refund** | + |
| **Balance correction** | + or − depending on the direction |
| **Withdrawal** | − |

Empty — «No transactions».

> ℹ️ The balance is topped up and corrected by the studio in the [Point of sale](/en/menu/pos) and the [client card](/en/menu/clients). In the app the client views the balance and operations.

---

## 7.6.5 Statistics (Coach)

Coach earnings for the selected period (date range selection, not later than today).

- The period total: the date range and the amount in UAH.
- A card for each category: name, amount in UAH, «Total workouts: {N}» and the **Credited to coach**, **Attended**, **Missed**, **Canceled** figures.
- No data — «No data for this period».

---

## 7.6.6 About

- The app icon and name, «Version {version}».
- **Developed by** — a link to fitshandler.com; **Contacts** — the developer's email address; **Support** — a Telegram link.
- «For issues and suggestions about the app, contact».
- **Admin** additionally sees the **«Registered in the app»** block: **Customer** — {N}, **Coach** — {N}.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

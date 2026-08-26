<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 1.3.2.2 Settings

> The **Settings** ("Налаштування") section is the studio's admin panel, split into tabs. Available to the **Super Admin**, **Admin**, and **Manager** roles.

![](../../_media/admin-panel-tabs.png ":size=600x362")

**Tabs:**

- [1. Users](#users) ("Користувачі") — administrator account management.
- [2. Settings](#settings) ("Налаштування") — operating hours, time zone, studio rules.
- [3. Features](#features) ("Функції") — features and business rules (cancellations, bonuses, bot, reminders).
- [4. Integrations](#integrations) ("Інтеграції") — fiscalization (VchasnoKasa, Checkbox) and card acquiring.
- [5. Import](#import) ("Імпорт") — importing clients from Excel.
- [6. Information](#information) ("Інформація") — version and supporting information.
- [7. Mobile Application](#mobile-application) ("Мобільний додаток") — client app configuration.
- [8. Reminders](#reminders) ("Нагадування") — custom reminders for studio staff.
- [9. Categories](#categories) ("Категорії") — categories for calculating coach salaries (moved from Reports).
- [10. Studio Information](#studio-information) ("Інформація про студію") — studio name, logo, description, photos, and contact details. This tab appears when the mobile app for clients is enabled.

---

## Users

> The list of studio administrators: adding new ones, editing roles, deleting.

![](../../_media/admin-panel-users.png ":size=600x362")

The full description of the table, of inviting a new user and of the roles is on the [Users](/en/login/users) page. Only the location of this tab is given here, so that one screen is not described in two places: those descriptions inevitably drift apart.

---

## Settings

> General studio parameters.

![](../../_media/admin-panel-settings.png ":size=600x362")

> ⚠️ **The studio name and logo have been moved** to the [Studio Information](#studio-information) tab. This tab only appears once the mobile app for clients is enabled.

### Studio Name

A text field on the **Studio Information** tab. Used in the Telegram bot and on fiscal receipts.

### Studio Logo

> Uploading or replacing the logo. Supports JPG/PNG. The **Delete Photo** ("Видалити фото") button removes the current logo.

### Studio Operating Hours

> The start and end time of the working day (selected with a time picker). Affects:

- Hints in the workout creation form.
- Administrator salary calculation (cannot exceed the shift duration).
- The mobile app (hides bookings outside these hours).

### Studio Rules

> A text field that supports multi-line text. Shown to clients in the mobile app (**Account → Information → Rules** tab).

### Studio Time Zone

> A dropdown list of IANA time zones (defaults to `Europe/Kyiv`). Affects ALL dates and reports.

> ⚠️ Changing the time zone is a wide-reaching operation. The selector is locked if the studio has at least one workout — otherwise the dates on already-created workouts could "shift". First delete/process all workouts, then change the time zone.

---

## Features

> Business rules and feature toggles. Each group is placed in its own section with a heading.

![](../../_media/admin-panel-functions.png ":size=600x362")

### Minimum Time Before Workout Cancellation

- **Time before workout cancellation (hours)** — a number (default 6).
- If a client has an active plan and cancels a workout **less than the specified number of hours** before it starts — the workout is **deducted** from the plan as **Unvisited** ("Не відвідано").

### Minimum Number of Clients

- **Min. count** — a number.
- If the setting is > 0 and fewer clients attended the workout — the coach is credited the minimum (protection against small, unprofitable groups).
- Available only for the **"Number of people at the workout"** ("Кількість людей на тренуванні") rate type (`PerPerson`).

### Remove Recurring Booking After Missed Workouts

- **Number of misses** — a number.
- If a client has a duplicate (recurring) booking for a workout and misses N consecutive sessions (status **Unvisited**) — the system automatically removes them from the recurring booking.
- `0` or an empty field → disables the feature.

### Administrator Bonuses

> Bonus settings that are calculated in the [Admin Salaries](/en/menu/reports#_3-8-5-administrator-payroll) report.

Each bonus is a row with three fields:

- **Condition** — what it is awarded for (for example, "Every card sold", "Every closed shift").
- **Accrual** — the method (fixed amount / percentage).
- **Client type** — a filter (new client / all).

The **➕ Add Bonus** and **🗑 Delete** (trash icon) buttons are available for each row.

### Creating Personal Workouts via the Bot

- The **"Allow coaches to create personal workouts via the bot"** toggle — enables the feature.
- When enabled, a list of **categories** appears for which the bot allows creating workouts. A coach can only create a personal workout within these categories.
- The **+ Add Category** button adds a row with a dropdown list of the studio's categories.

### Remind About Coach Birthdays

- **Days** — how many days before the birthday the notification arrives.
- `0` → the feature is disabled.

### Features (Additional Toggles)

- **Notify clients about a coach substitution (App)** — if a substitute is assigned for a workout, all booked clients receive a push notification in the mobile app.
- **Apply the maximum number of people when calculating salaries** — caps the number of clients credited to a coach at the `workoutCapacity` value.
- **Close the shift automatically** (closes at 23:57) — under the law, a cash register shift cannot last more than 24 hours. Automatic closing avoids human error and keeps this requirement.
- **Charge a debt for a no-show on a personal (no-plan) workout and credit the coach** — when enabled: if a personal workout is marked **"Unvisited"**, and the client has **no active personal plan**, the system automatically creates a **debt** for the client equal to the cost of the workout (the price of the plan linked to the category) and **credits the coach** with that workout toward their salary. This triggers on any "Unvisited" status being set (the nightly automatic process, a late cancellation, or a manual status change by an administrator). If the workout's category has no plan with a price linked to it — no debt is created.

---

### Danger Zone

The **Clear Workouts** ("Очистити тренування") button irreversibly cancels all of the studio's not-yet-held workouts and stops all recurring ones. To confirm, you must type the word **DELETE** in the confirmation field.

### Automatic Logout on Inactivity

The number of hours of inactivity after which a user is automatically logged out of the system. A value of `0` disables automatic logout.

---

## Integrations

> Integration with a fiscal payment recorder. **VchasnoKasa** and **Checkbox** are supported. Each integration is added as a separate card.

![](../../_media/admin-panel-prro.png ":size=600x362")

### Connection

Each fiscal integration is added as a separate card — using the **+ Add VchasnoKasa** or **+ Add Checkbox** button.

- **Label** — an arbitrary name for the card, to distinguish between several connections.
- **Token** — for VchasnoKasa: the token from your personal account.
- **PIN Code**, **Client Name**, **Client Version**, **License Key** — for Checkbox; all four fields are required.
- The **Active** ("Активна") toggle enables the card. It only takes effect once the required fields are filled in, and only one card of each type can be active at a time.

> ⚠️ The "Receipt Header" and "Receipt Footer" fields no longer exist — they were removed together with the move to integration cards.

### What Changes When Fiscalization Is Enabled

- All sales (cash/card) are **fiscalized** through VchasnoKasa; a fiscal receipt is created for every transaction.
- A Z-report is printed automatically when the shift closes.
- Top-ups to a client's personal account are also fiscalized (as a regular transaction). Deductions from the personal account are **NOT** fiscalized (because the funds were already fiscalized at the time of the top-up).

> ℹ️ The **X Report** and **End-of-Day Report** buttons on the [POS](/en/menu/pos) page are available **whenever a shift is open**, regardless of the fiscal integration. Without it, these reports show a summary of cash flow for the shift and for the day; with it, they additionally include fiscal data.

---

## Import

> Importing clients from an Excel file.

[More about importing](/en/pages/setup#_4-7-2-importing-clients-from-an-excel-file)

---

## Information

> Technical information.

- **Version** — the current version of the application.
- Date and source of the last update.
- Support contacts.

---

## Mobile Application

> Tools for working with the studio's mobile PWA client app.

> ℹ️ A description of the app **from the user's point of view** (installation, sign-in, booking a workout, the card, notifications) is in section [7. Mobile Application](/en/mobile/mobile).

![](../../_media/admin-panel-mobile.png ":size=600x362")

### Main Toggles

- **Use the mobile app for clients** — the main toggle. To turn it off, you must type the confirmation **SWITCHOFF**: along with the app, clients lose the ability to book online.
- **Confirm a guest booking by SMS** — allows a person without an account to confirm a booking with an SMS code, not only through Telegram.
- **Offer to rate the session** — after an attended session, the client is offered the chance to leave a rating.

### Visit Reminders

- **Remind about the visit** — how many hours before the session to send a reminder. A value of `0` disables the reminder.
- Next to it, the number of SMS already used from the studio's monthly limit is shown.
- **SMS reminder text** — the studio's own text. The date and time are inserted automatically, so only the words before and after them can be edited. A counter shows how many of the 57 characters remain: an SMS cannot hold more than that, and each additional one is billed separately.

### Public Studio Link

A link to the studio's public page together with a QR code. Anyone can use it to view the schedule and book a session without an account.

### Link + QR Code

- **App link** — the PWA install URL (defaults to `https://app.fitshandler.com`). Clickable, opens in a new tab.
- **Download QR Code** — the button downloads a PNG with a QR code that leads to this link. It can be printed and shown to the client at the studio.
- **Download Banner** — a print-ready promotional banner with the QR code and the app's logo.

### User Counters

An information block showing how many are registered in the app:

- **Registered clients: N** — how many of the studio's clients have connected the mobile app.
- **Registered coaches: N** — how many of the studio's coaches have an active account in the app.

### Send a Message from the Studio

> Sends a push notification to all app users in the chosen audience.

- **Choose message type** — a dropdown list:
  - **Clients** — all clients receive the push.
  - **Coaches** — all coaches receive the push.
  - **All** — both audiences.
- **Text editor** — supports formatting (bold/italic/links). Has a length limit; exceeding it shows the error "Message is empty or too long."
- **Send** — the button becomes active once an audience is chosen and text is entered. Clicking it immediately queues the message for delivery to all devices.

---

## Reminders

> Custom reminders for studio staff: one-off or recurring entries with a date, time, and text. Not to be confused with visit reminders sent to clients — those are configured on the [Mobile Application](#mobile-application) tab.

---

## Studio Information

> This tab appears when the mobile app for clients is enabled. Everything filled in here is shown to the client in the app, in the studio's header and in the **"About Us"** window.

- **Studio Name** — used in the app, the Telegram bot, and on fiscal receipts.
- **Studio Logo** — the image the client sees next to the name.
- **About Us** — a description of the studio.
- **Photos** — up to ten gallery photos.
- **City** — besides appearing on the studio card, it is used for the city filter in the list of studios.
- **Phone** and **Address** — contact details the client sees in the studio's header and in the "About Us" window.

Changes are saved with the **Save** button.

> ℹ️ While these fields are empty, only the name and logo are shown in the app: the **"About Us"** button is always present, but inside it there will be a message that no information is available yet.

---

## Categories

> The **Categories** tab (previously in [Reports](/en/menu/reports)). Categories are used for calculating coach salaries and, optionally, for linking to a plan.

**Table columns:**

| Column | Description |
| --- | --- |
| **Name** | The category name (for example, "Group", "Personal", "Kids"). |
| **Category base rate** | The amount in UAH used in the salary formula. |
| **Rate type** | **Per Person** (`PerPerson`) — the number of clients is counted and multiplied by the rate. **Per Workout** (`PerWorkout`) — the number of workouts held is counted. |
| **Plan** | An optional link to a specific plan (for categories under personal plans). |
| **Actions** | Edit / Delete. |

**Search** — a field above the table, searches by name.

### Add / Edit Category

> The **+ Add Category** button opens a modal. The same modal opens when you click **Edit** on a row.

**Fields:**

- **Name** — required.
- **Base rate** — required, a number in UAH.
- **Rate type** — **Per Person** / **Per Workout**.
- **Plan** — links the category to a specific plan. This field is **optional for the "Per Person" type**, but **required for the "Per Workout" type** (marked with an asterisk on the form). Reasoning: with Per Workout, the salary for the category depends on the client's specific plan; without a plan it cannot be calculated unambiguously.

> ℹ️ If **Per Workout** is chosen without a plan — the **Save** button will be inactive. First create or choose the corresponding plan.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

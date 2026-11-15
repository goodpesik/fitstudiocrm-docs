[Back to home](/en/)

# 2. Opening and Closing a Shift

## 2.1 Opening a Shift

> The **Відкрити зміну** (Open shift) button is on the right side of the header while the shift is closed.

![](../../_media/shift-closed.png ":no-zoom")

Clicking it opens the [«Ви впевнені що хочете продовжити?» (Are you sure you want to continue?) modal](../_modals/are-you-sure-modal.md ":include"). **Продовжити** (Continue) opens the shift, and the message «Зміну відкрито» (Shift opened) appears.

If another user has already opened the shift, the window «Зміну вже відкрито користувачем <name>» (The shift is already opened by user <name>) appears with the **Зрозуміло** (Got it) button; no new shift is opened.

**Restrictions while the shift is closed:**

- The **Продаж** (Sale) button is not shown in the header. The button is available to the **Супер Адмін** (Super Admin) and **Адмін** (Admin) roles only while a shift is open.
- Scanning cards and certificate QR codes is blocked: the system shows the «Необхідно відкрити зміну!» (You need to open a shift!) window with the **Зрозуміло** button.
- When a user with the **Адмін** role goes to the **Клієнти** (Clients) page, the window «Ви не відривали поточну зміну. Деякі дії будуть не доступні» (You have not opened the current shift. Some actions will not be available) appears with the **Зрозуміло** button. Work on the page can continue; some actions are unavailable. The warning is not shown to the **Супер Адмін** and **Менеджер** (Manager) roles.

### Shift opened by another user

If, when a user with the **Адмін** role signs in, the shift is open under another user, the window «Зміна була відкрита <name>. Бажаєте відкрити зміну під своїм користувачем?» (The shift was opened by <name>. Do you want to open the shift under your own user?) appears:

- **Так** (Yes) — the current shift is closed and a new shift is opened under the signed-in user.
- **Ні** (No) — the shift stays with the previous user.

> Shifts are used to track working time and [administrator salaries](/en/menu/reports#_3-8-5-administrator-payroll).

---

## 2.2 Closing a Shift

> The **Закрити зміну** (Close shift) button is on the right side of the header while the shift is open.

![](../../_media/shift-opened.png ":no-zoom")

Clicking it opens the [«Ви впевнені що хочете продовжити?» modal](../_modals/are-you-sure-modal.md ":include"). If the shift was opened by another user, the text is «Зміна була відкрита користувачем <name>. Ви впевненні що хочете закрити зміну?» (The shift was opened by user <name>. Are you sure you want to close the shift?).

After confirmation the **Зміну закрито** (Shift closed) modal appears.

![](../../_media/close-shift-modal.png ":no-zoom")

- The **Робочі години** (Working hours) field holds the calculated shift length. Format — a decimal number: 1 hour — `1`, 1 hour 30 minutes — `1.5`.
- The **Зберегти** (Save) button is active only when the value has changed; it saves the entered hours.
- The **Закрити** (Close) button closes the window without changes.
- If a fiscal integration is active, the window also shows the shift Z-report.

> ⚠️ When the **Зміну закрито** window is closed (with **Закрити**, **Зберегти** or the cross), the system signs the user out.

The hours of a closed shift can be changed later on the [Reports → Shifts](/en/menu/reports#_3-8-2-shifts) page.

---

## 2.3 Opening and Closing a Shift with a Fiscal Integration

If at least one fiscal integration (Vchasno Kasa or Checkbox) is active in [Settings → Integrations](/en/login/settings#integrations), the **Відкрити зміну** and **Закрити зміну** buttons open the **Відкрити зміну** / **Закрити зміну** window instead of the confirmation window.

The window contains the **Активні фіскальні інтеграції** (Active fiscal integrations) table:

| Column | Value |
| --- | --- |
| **Назва** (Name) | Integration card name |
| **Оператор** (Operator) | Integration type |
| **Статус** (Status) | **Онлайн** (Online) / **Офлайн** (Offline) / **Перевірка…** (Checking…) — connection with the operator |
| **Зміна на інтеграції** (Shift on the integration) | **Відкрита** (Open) / **Закрита** (Closed) / **Перевірка…** — shift state on the operator side |

If the shift state in the system and at the operator differ, the row shows the **Синхронізувати** (Synchronize) button; after synchronization the message «Інтеграцію синхронізовано» (Integration synchronized) appears.

Window buttons:

- **Скасувати** (Cancel) — closes the window with no action.
- **Відкрити** (Open) / **Закрити** (Close) — brings the shift of every active integration into the required state, then opens or closes the shift in the system. If the action fails for one of the integrations, the message «<name>: синхронізація не вдалась» (<name>: synchronization failed) appears; the shift in the system is opened or closed anyway.

On closing, the Z-reports received from the integrations are saved with the shift and shown in the **Зміну закрито** window.

---

## 2.4 Automatic Shift Closing

If the **Закривати зміну автоматично(закриється 23:57)** (Close the shift automatically (closes at 23:57)) switch is on in [Settings → Functions](/en/login/settings#features), an open shift is closed every day at 23:58 Kyiv time. The record «Зміну закрито автоматично» (Shift closed automatically) appears in the notifications.

---

## 2.5 Notifications

![](../../_media/notifications-1.png ":no-zoom")

The **Сповіщення** (Notifications) button in the header shows the number of unread notifications. The number is refreshed every 10 minutes; if there are unread notifications, the window «Доступні нові сповіщення» (New notifications available) appears with the **Зрозуміло** button.

Notifications are created by events in the studio, including:

- bookings and booking cancellations by clients through the mobile app;
- a booking that needs administrator confirmation;
- automatic removal of a client from a repeat booking (see [Settings → Functions](/en/login/settings#features));
- automatic shift closing;
- service messages from the Fitshandler platform.

![](../../_media/notifications-2.png ":no-zoom")

Clicking the button opens the **Сповіщення** window with a table: **Дата** (Date), **Повідемлення** (Message), **Дії** (Actions). Available actions:

- **Прочитати** (Read) / **Позначити як непрочитане** (Mark as unread);
- **Видалити** (Delete);
- **Перейти до тренування** (Go to workout) — for notifications related to a workout;
- **Підтвердити** (Confirm) / **Відхилити** (Reject) — for bookings that need confirmation.

[Back to home](/en/)

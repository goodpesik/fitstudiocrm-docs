<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.7 Notifications

> The **Notifications** tab is the push notification history and notification settings. The tab icon shows an unread counter.

<!-- TODO: screenshot of the Notifications tab -->

The tab has two sub-tabs: **"Notifications"** ("Сповіщення") (history) and **"Settings"** ("Налаштування").

---

## 7.7.1 Notification History

- A paginated list of messages (10/20/50). Unread ones are highlighted.
- The **"Mark All as Read"** ("Прочитати всі") button marks all as read.
- Each unread row has a **"Mark as Read"** ("Прочитати") button.
- Empty → **"No messages found"** ("Не знайдено жодного повідомленя").

---

## 7.7.2 Notification Settings

> Title **"Notification Settings"** ("Налаштування сповіщень").

- **"Enable Push Notifications"** ("Увімкнути Push сповіщення") — the main toggle. When enabled, the browser will ask for notification permission.
- **Notification types** (the set depends on the role):
  - **"Reminders"** ("Нагадування") — client only.
  - **"Messages from the Studio"** ("Повідомлення від студії") — client, coach.
  - **"Classes"** ("Тренування") — client, coach.
  - **"System Messages"** ("Системні повідомлення") — admin only.
- **Client:** **"Remind me about an upcoming class"** ("Нагадувати про майбутнє тренування за") + number of hours (1–24).
- **"Save"** ("Зберегти") — saves the selected types and reminder time.

> ℹ️ The administrator sends **"Messages from the Studio"** mass messages from [Settings → Mobile App](/en/login/settings#send-a-message-from-the-studio).

> ⚠️ If push is disabled at the system level (in the phone/browser settings), notifications will not arrive even if the toggle is enabled in the app. Check the permissions in your device settings.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

---

## When notifications stop arriving

Permission for notifications sometimes goes stale — the browser or the system revokes the subscription without saying so. The app notices this itself: if notifications are switched on in the settings but there is in fact no subscription, it either quietly restores it or shows a window explaining how to unblock notifications in the browser settings. That window appears at most once per session.

---

[Back to home](/en/)

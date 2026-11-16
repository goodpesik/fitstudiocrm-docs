<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.7 Notifications

> The **Notifications** tab is the notification feed of the selected studio and the notification settings. The tab icon shows a counter of unread notifications.

---

## 7.7.1 Notification Feed

- A notification card: type icon, studio name, date and time, text. Unread cards are highlighted and marked with a dot.
- Tapping an unread card marks it as read.
- The **«Unread: {N}»** line and the **«Mark all as read»** button — shown if there are unread notifications.
- Notifications are loaded 10 at a time; the **«Show more»** button loads the next ones.
- Empty — «No messages found».

**Booking requests (admin).** The card of a notification about a booking request waiting for a decision shows the **«Reject»** and **«Approve»** buttons. After the decision the buttons disappear and the card is marked as read. The reason for a refusal (the request has already been reviewed, the class has passed) is shown in an error window. The same requests are available on [Home](/en/mobile/home#_735-administrator-panel).

---

## 7.7.2 Notification Settings

The gear button next to the heading opens the **«Notification settings»** window:

- **«Enable push notifications»** — the main switch. When it is turned on, the phone or browser asks for notification permission.
- Notification types (the set depends on the role):

| Type | Customer | Coach | Admin |
|---|:---:|:---:|:---:|
| **Reminders** | ✔ | — | — |
| **Studio messages** | ✔ | ✔ | — |
| **Workouts** | ✔ | ✔ | — |
| **System messages** | — | — | ✔ |

- Session reminders are received by clients only. A coach does not receive session reminders; the coach settings have no **Reminders** type.

- **Client:** **«Remind me»** — the number of hours from 1 to 24, with − and + buttons. The field is inactive if the **Reminders** type is off.
- **«Save»** — saves the notification types and the reminder time.

> ℹ️ The reminder from this setting arrives as a notification in the app. To clients without the app the studio sends reminders via Telegram or SMS according to its own setting. The channel order and the night pause are in [Class reminders](/en/pages/processing#_66-class-reminders).

> ℹ️ **Studio messages** are sent by the administrator in [Settings → Mobile Application](/en/login/settings#send-a-message-from-the-studio).

If notifications could not be turned on for a technical reason — «Couldn't turn notifications on. Check your connection and try again.»

---

## 7.7.3 Blocked Notifications

If notifications are on in the app but their permission is blocked in the system, notifications do not arrive. At launch the app checks the notification subscription: where possible it restores it without the user's involvement, otherwise it shows the **«Notifications blocked»** window:

- in the store app — «Notifications for the app are turned off in your phone settings, so we can't send them. Allow notifications for Fitshandler in your device settings.»;
- in a browser — «Notifications for this site are blocked in your browser, so you are not receiving them. To get reminders again, allow notifications in your browser's site settings for this site.»

The window is shown no more often than once per session.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

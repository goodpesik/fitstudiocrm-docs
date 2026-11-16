[Back to home](/en/)

# 7. Mobile App (Client App)

> **The Fitshandler mobile app** is the studio's client app. Clients use it to book workouts, check in to workouts with the studio's QR code, show their client card at the front desk, view their plans and history, and receive notifications. Coaches and administrators work in the app in their own roles.

The app is installed from the **App Store** or **Google Play**. The studio's public page also opens in a browser without installing the app. The studio-side settings of the app (turning it on, online booking, SMS, self check-in, link and QR code, studio messages) are described in [Settings → Mobile Application](/en/login/settings#mobile-application). This section describes the app from the user's side.

The app interface is available in Ukrainian and English; UI labels below are quoted as the English interface shows them.

---

## 7.0 Roles in the App

One account (one phone number) can have several roles and belong to several studios. After logging in, the user selects a studio and a profile. Roles:

| Role | Who | What is available |
|---|---|---|
| **Customer** | a client of the studio | workout booking, client card, plans, history, personal balance, rating classes |
| **Coach** | a coach of the studio | own workouts and the studio schedule, creating personal workouts, statistics, ratings |
| **Admin** | a studio administrator | studio schedule, booking clients, creating workouts, booking requests, system messages, coach ratings |
| **Guest** | a user without a client card in the selected studio | studio schedule and a booking request (see [7.2](/en/mobile/registration)) |

> ℹ️ No account is needed to view a studio: the public studio page and the studio list open without logging in (see [7.8](/en/mobile/guest)).

---

## 7.1 Sections

- [7.1 Installation and Login](/en/mobile/install) — installing from the App Store or Google Play, logging in with a code via Telegram or SMS.
- [7.2 Registration and Studio Selection](/en/mobile/registration) — a booking request for a user without a client card, selecting a studio and a profile.
- [7.3 Home](/en/mobile/home) — studio header, upcoming workouts, current plan, booking requests for the administrator.
- [7.4 Client Card](/en/mobile/card) — the client card QR code for the front desk.
- [7.5 Workouts](/en/mobile/workouts) — schedule, booking, cancellation, wait list, creating workouts.
- [7.6 Account](/en/mobile/account) — profile, plans, history, personal balance, statistics, data deletion.
- [7.7 Notifications](/en/mobile/notifications) — notification feed and notification settings.
- [7.8 Public Studio Page and Booking Without an Account](/en/mobile/guest) — studio list, studio page, booking with phone number confirmation.
- [7.9 Ratings and Reviews](/en/mobile/ratings) — class ratings, studio and coach ratings.

---

## 7.2 Bottom Navigation

After a studio and a profile are selected, a navigation bar is shown at the bottom of the screen. The set of tabs depends on the role:

| Tab | Customer | Coach | Admin | Guest |
|---|:---:|:---:|:---:|:---:|
| **Home** | ✔ | ✔ | ✔ | ✔ |
| **Client card** | ✔ | — | — | — |
| **Workouts** | ✔ | ✔ | ✔ | ✔ |
| **Ratings** | — | ✔ | ✔ | — |
| **Account** | ✔ | ✔ | ✔ | ✔ |
| **Notifications** | ✔ | ✔ | ✔ | ✔ |

> The **Notifications** tab shows a counter of unread notifications.

The navigation bar is not shown on public pages (studio list, studio page, check-in by QR code, rating a class by link).

---

## 7.3 App Header

The header of every screen except the login screen contains:

- the Fitshandler logo — opens fitshandler.com;
- the data refresh button — shown on screens whose data can be refreshed;
- the language switcher (flag) — Ukrainian or English. For a logged-in user the choice is saved in the account and applies in all studios and roles; this language is used in the messages the studio sends to the client through notifications, Telegram or SMS;
- on the studio page in a browser — the **«Install»** button, which opens the App Store and Google Play links.

---

## 7.4 Service Screens and Windows

| Situation | What is shown |
|---|---|
| System update | The **«Attention!!! A system update is in progress»** screen with the text «Please wait — the page will refresh automatically.» The screen cannot be closed; the server state is checked every 10 seconds, and the screen disappears when the update ends. |
| Server unavailable | The **«Technical issues»** screen with the text «The server is temporarily unavailable. Please refresh the page.» and the **«Update»** button. |
| New version available | The window «A new version of the app is available. Update now?». A new version is checked for every 10 minutes. |
| Offer to rate the app | In the App Store or Google Play app — the **«Rate the app»** window with the **«Rate»** and **«Close»** buttons and the **«Don't show again»** switch. The window is shown no more often than once every 30 days, the first time 30 days after the first launch. |
| Client profile without a last name | The **«Please enter your last name»** window with the **First name** and **Last name** fields and the **«Save»** button. The window cannot be closed without saving. |

> ⚠️ From 1 November 2026 the web version of the app added to the phone home screen (PWA) does not work on iPhone and Android: instead of the app, the window «The old version of the app stops working on 1 November 2026. Install the new one.» is shown with a button to the App Store or Google Play. The window cannot be closed.

---

[Back to home](/en/)
<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

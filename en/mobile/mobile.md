[Back to home](/en/)

# 7. Mobile App (Client App)

> **The Fitshandler mobile app** is the studio's client-facing PWA. Clients use it to book classes, show their QR client card at reception, track their membership, and receive push notifications. Coaches and administrators also have their own mode in the app.

This is a separate app from the studio's admin panel. The studio-side setup of the app (link, QR code, banner, mass messaging, counters) is described in [Settings → Mobile App](/en/login/settings#mobile-application). This section describes the app **from the user's point of view**.

---

## 7.0 Roles in the App

One login (one Telegram account) can hold several roles and belong to several studios. After logging in, the user selects a studio and a role (client). Roles:

| Role | Who it is | What they see |
|---|---|---|
| **Client** | a studio visitor | class booking, QR client card, memberships, history, personal account |
| **Coach** | a studio coach | own schedule, salary statistics, class creation |
| **Admin** | a studio administrator | overall schedule, client booking, system notifications |
| **Guest** | logged in but not yet part of any studio | request to join a studio |

> ℹ️ The same email/phone number can have several "clients" (a role + studio pair). After logging in, the user switches between studios and roles from the [Home screen](/en/mobile/home).

> ℹ️ No account is needed just to browse. Anyone can open a studio page — via a link or from the list of studios — view the schedule, and book a class right away by confirming their phone number with a code. The person automatically becomes a client of the studio after their first booking.

---

## Application language

Next to the name in the header there is a language switch — Ukrainian or English. The choice is stored against the user and applies across every studio and role. It also decides the language of the reminders that arrive as notifications, in Telegram or by SMS.

---

## 7.1 Sections

- [7.1. Installation and Login](/en/mobile/install) — installing the app, viewing the list of studios without logging in, and confirming login via Telegram or SMS.
- [7.2. Registration and Studio Selection](/en/mobile/registration) — a new client's first request, choosing a studio/role.
- [7.3. Home](/en/mobile/home) — the welcome screen, upcoming classes, current membership.
- [7.4. Client Card](/en/mobile/card) — the QR client card for reception (client role only).
- [7.5. Classes](/en/mobile/workouts) — booking, cancelling, waiting list; coach/admin schedule.
- [7.6. Account](/en/mobile/account) — profile, memberships, history, personal account, statistics.
- [7.7. Notifications](/en/mobile/notifications) — push notification history and notification settings.
- [7.8. Public Studio Page and Booking Without an Account](/en/mobile/guest) — viewing the schedule and booking without registering.
- [7.9. Ratings and Reviews](/en/mobile/ratings) — client ratings, studio and coach ratings.

---

## 7.2 Bottom Navigation

After selecting a studio and role, a navigation bar appears at the bottom of the screen. The set of tabs depends on the role:

| Tab | Icon | Client | Coach | Admin |
|---|:---:|:---:|:---:|:---:|
| **Home** ("Головна") | 🏠 | ✔ | ✔ | ✔ |
| **Client Card** ("Карта клієнта") | ▦ (QR) | ✔ | — | — |
| **Classes** ("Тренування") | 📅 | ✔ | ✔ | ✔ |
| **Ratings** ("Рейтинги") | ⭐ | — | ✔ | ✔ |
| **Account** ("Кабінет") | 👤 | ✔ | ✔ | ✔ |
| **Notifications** ("Сповіщення") | 🔔 | ✔ | ✔ | ✔ |

> The **Notifications** tab shows a red counter of unread messages.

> **Ratings.** A coach sees their own average rating and clients' reviews about them; an administrator sees the ratings of all coaches at the studio, with a link through to each coach's reviews. This tab is not shown to clients: a client opens the studio's rating and reviews by tapping the star in the studio header on the Home screen.

---

[Back to home](/en/)

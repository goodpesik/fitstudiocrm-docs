<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.2 Registration and Studio Selection

> A user who is logged in but has no client card in the selected studio works in the **Guest** role: views the studio schedule and submits a **booking request**. The request is approved or rejected by a studio administrator.

---

## 7.2.1 Booking Request

The guest schedule opens on the **Workouts** tab:

1. At the top is a strip of the days of the current week (from today, 7 days); a dot under a day marks a day with workouts. The day is changed by tapping a day or by swiping the screen left or right.
2. The workout card has the **«Book»** button. The **«Workout booking»** window shows the workout, coach, room, date and time; buttons **«Cancel»** and **«Continue»**.
3. If the studio does not yet know the user's first and last name, the **«Enter your first and last name»** window opens with the class details and the **First name** and **Last name** fields (both required); buttons **«Confirm selection»** and **«Close»**.
4. The request is sent to the studio administrators. A client card is created in the studio; the seat in the workout is not taken until the request is approved.

If there are no workouts on the selected day — «There are no workouts available for booking».

If the user is not logged in, **«Book»** opens the login screen; after login the booking continues for the selected class. If after login the user turns out to be a client of the studio already, the app opens the **Workouts** tab on the day of that class for a regular booking.

### Restrictions

| Situation | Message («Cannot book») |
|---|---|
| A request is waiting for a decision | «Wait for the studio to review your previous request. You can cancel it on the home page.» |
| Requests have been submitted for three different workouts | «You have already tried three different classes. Request one of them again from the home page.» |
| The class is no longer available | «This class is no longer available. Pick another one.» |

<!-- TODO: screenshot of the request on Home -->

---

## 7.2.2 Request Status

The request is shown on [Home](/en/mobile/home) in the **«Upcoming workouts»** block as a class card with a status:

| Status | Action in the card menu |
|---|---|
| **Waiting for approval** | **«Cancel request»** |
| **Request cancelled** | **«Request again»** — available if there is no other request waiting for a decision |

For a cancelled request for a class that is no longer in the schedule, «This class has already passed» is shown. A class card with a request in the schedule does not show the **«Book»** button.

The administrator reviews the request in the admin panel or in the app (see [7.3.5](/en/mobile/home#_735-administrator-panel)). After approval the client is booked for the workout and receives a message; the client profile becomes available in the app.

---

## 7.2.3 Studio and Profile Selection

If the user has profiles in several studios or several profiles in one studio, after login the app asks to select:

- **«Select a studio»** → studio → **«Confirm selection»**;
- **«Select a client»** → profile in the format **«Name - Role»** → **«Confirm selection»**.

If the studio has one profile, it is selected automatically.

The studio is changed with the **«Select studio»** button above the studio header on [Home](/en/mobile/home); the profile — with the **«Select client»** button in the studio header (shown if there is more than one profile).

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

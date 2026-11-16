<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.3 Home

> The **Home** tab shows the header of the selected studio, a greeting, upcoming workouts, the client's current plan, and for the administrator — the shift state and booking requests.

---

## 7.3.1 Studio

- The **«Select studio»** button above the studio header opens the **«Select a studio»** window. It lists all studios that work in the app. For a studio where the user has no profile, Home of that studio opens in the **Guest** role (see [7.2](/en/mobile/registration)).
- **Studio header**: logo, name, address (opens the route in maps), phone (call), the **«About us»** button with the studio description, photos, a map, the **«Route»** and **«Call»** buttons and reviews, and a star with the average rating and the number of reviews (see [7.9](/en/mobile/ratings)).
- Buttons in the studio header (when applicable):
  - **«Studio rules»** — opens the studio rules if the studio has filled them in [Settings](/en/login/settings#studio-rules);
  - **«Select client»** — opens the **«Select a client»** window; shown if the user has more than one profile.

---

## 7.3.2 Greeting

- **«Hello, {name}»**. Next to the name — the **Coach** or **Admin** role badge; no badge is shown for a client.
- For a guest — **«Welcome to the studio»**. If the guest is not logged in, the **«Log in»** button is shown under the greeting; if logged in — the **«Upcoming workouts»** block with the booking request state (see [7.2.2](/en/mobile/registration#_722-request-status)) or «You have no workouts in the near future».

---

## 7.3.3 Upcoming Workouts

For a **client** and a **coach** — the **«Upcoming workouts»** block with workout cards:

- A **client** sees their own bookings for the next **6 days** (144 hours).
- A **coach** sees their own workouts for the next **4 hours**; next to the heading — their own average rating and number of ratings.
- The client's booking requests, if any, are shown above the bookings (see [7.2.2](/en/mobile/registration#_722-request-status)).
- If there are no workouts and no requests — «You have no workouts in the near future».

A client who has attended a class sees the **«Rate your last class»** offer above the block (see [7.9](/en/mobile/ratings)).

The workout card and its actions are described in [Workouts](/en/mobile/workouts).

---

## 7.3.4 Current Plan (Client)

The **«Current plan»** block shows one plan: the active one; if there is none — the new one; if there is none either — an ended plan whose validity period has not yet passed. The plan card:

- **«Plan · {studio name}»** and the status: **Active**, **New**, **Ended** or **Suspended**;
- the plan size («{N} workouts») and **«Used {X} of {N}»**; a ring with the number of workouts left (**«left»**). For a plan without a number of workouts, the plan name and **«Workouts remaining: {N}»** are shown instead of the size;
- for a new plan — «Not active. It will be activated during your visit to the studio»;
- the warning «Attention! Your plan is expiring soon.» — when fewer than 3 days or fewer than 3 workouts are left;
- **«Valid until (inclusive)»** and the end date;
- the **«Client card»** button — opens the [Client Card](/en/mobile/card).

Tapping the card opens [Account → History](/en/mobile/account#_763-history-client). If there is no plan — «No current plan.»

---

## 7.3.5 Administrator Panel

For the **Admin** role:

- the badge **«Shift open · {name}»** or **«Shift closed»**;
- **«Total clients today:»** — the number of clients with the **Attended** status in today's workouts;
- the **«Booking requests»** card with the caption «Waiting for a decision: {N}» — shown if there are requests waiting for a decision. The card opens the request list: client, workout, date and time, the **«Approve»** and **«Reject»** buttons. An empty list — «No requests are waiting for a decision»; a loading error — «Could not read the requests. Try again.»

A request is also decided with the **«Approve»** / **«Reject»** buttons on the notification card in the [Notifications](/en/mobile/notifications) tab and in the admin panel. For a request already reviewed or a class that has passed, the reason for the refusal is shown.

---

## 7.3.6 Offer to Enable Notifications

After login, if notifications are off on the device, the **«Enable notifications?»** window is shown with the text «To receive reminders and stay up to date with all updates, we recommend enabling notifications. You can do this later in the Notifications => Settings section».

- **«Enable»** — subscribes the device to notifications.
- **«Cancel»** — closes the window; notifications are turned on later in [Notifications](/en/mobile/notifications).

The window is shown once. If notification permission is blocked in the phone or browser settings, the **«Notifications blocked»** window is shown with an explanation of how to allow notifications.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

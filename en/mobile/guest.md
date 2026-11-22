<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.8 Public Studio Page and Booking Without an Account

> Viewing a studio schedule and booking a class do not require an account. A person opens the studio page by a link or from the studio list, chooses a class and confirms the phone number with a code. After the first booking a client card with this number is created in the studio.

The pages work in the app and in a browser. The app navigation bar is not shown on them.

---

## Studio List

The **«Choose a studio»** screen («Browse the schedule and book — no account needed.») opens:

- when the app is launched without login;
- by the **«Browse studios»** link on the login screen.

On the screen:

- the **«Search by studio or city»** field;
- the city filter (**«All cities»** and the studios' cities) — shown if the studios are in several cities. The city is taken from the **Місто** (City) field on the [Studio Information](/en/login/settings#studio-information) tab;
- studio cards with the **«View»** button;
- the line «Already have an account?» with the **«Sign in»** button.

The list shows studios that have turned on the mobile app for clients. No studios — «No studios available right now.»; a search without results — «Nothing found».

---

## Studio Page

Each studio has a public link of the form `<app link>/s/<studio identifier>` and a QR code for it — on the [Settings → Mobile Application](/en/login/settings#online-booking-and-sign-in) tab.

On the page:

- **Studio header**: logo, name, address, phone, the **«About us»** button (description, photos, **«Map»**, **«Route»**, **«Call»**, **«Reviews»**) and a star with the rating, if the rating is shown (see [7.9](/en/mobile/ratings));
- **«Class schedule»** — classes for the next 15 days, by day, with day switching by arrows or swiping. The class card: time, name, room, coach, «Seats left: {N}» or «No seats left», the **«Book»** button. Personal classes, rentals, cancelled and already started classes, and classes the studio has taken off online booking are not shown. An empty schedule — «No upcoming classes yet.»; an empty day — «No classes on this day»;
- in the installed app — the **«Log in»** button; in a browser — the **«Install»** button in the header.

| Situation | What is shown |
|---|---|
| A mistyped link or the studio is not found | **«Studio not found»** — «This link looks outdated or mistyped.» and the **«Browse studios»** button |
| The studio has turned off the mobile app | **«Studio temporarily unavailable»** — «This studio is not taking app bookings right now.» and the **«Browse studios»** button |
| **«Онлайн запис із веб сторінки»** (Online booking from the web page) is off | The schedule is shown with the caption «Online booking is temporarily unavailable»; there is no **«Book»** button |

---

## Booking a Class

The **«Book»** button opens the **«Book a class»** window:

1. **Phone number** — «Confirm your phone number to book.», the **Phone number** field → **«Send code»**. The person does not choose the code delivery channel: the system sends a six-digit code **via Telegram** if the person can be found there, otherwise **by SMS**. The messages about a failed send and the 5-second pause before another attempt are the same as when [logging in to the app](/en/mobile/install#phone-number).
2. **Code** — 6 digits → **«Confirm»**. The hint above the code field matches the channel: «Код надіслано вам у Telegram. Введіть його тут.» (The code was sent to you in Telegram. Enter it here.) or «Введіть код з SMS.» (Enter the code from the SMS.) **«Request another code»** is available 60 seconds after the previous send; **«Change number»** returns to the number entry. The code is valid for 10 minutes; a wrong or expired code — «Invalid or expired code.»
3. **First and last name** — the **First name** and **Last name** fields → **«Next»**. If the number already belongs to a client of the studio, the step is skipped, and the next step shows «You are already a client of this studio. Booking as {name}.»
4. **«Check your booking»** — client, class, coach, room, date, time; buttons **«Cancel»** and **«Book»**.

Result:

| Result | Message |
|---|---|
| The booking needs the studio's confirmation | «Your request has to be approved by an administrator. We will let you know as soon as it is.» |
| Booked | «You're booked!» |
| The booking got the **Waiting list** status | «Вас додано до листа очікування. Вільні місця на цьому занятті першочергово надаються клієнтам з листа очікування.» (You have been added to the waiting list. Free places in this class are offered first to clients on the waiting list.) |
| The person is already booked for this class | **«You're already booked for this class»** — «See you there. Manage your booking in the app.», the **«Got it»** button |
| No seats | «This class has no seats left» |
| Other error | «Couldn't book. Please try again.» |

After booking in a browser, the **«Easier with the app»** block with the App Store and Google Play badges is shown.

> ℹ️ If the number already belongs to a client of the studio, no new card is created — the booking is added to the existing card.

---

## What the Studio Sees

- The client card is created right after the number is confirmed with a code, before the request is decided.
- If the **«Підтверджувати записи з веб сторінки»** (Confirm bookings from the web page) switch is on (on by default), the booking is submitted as a request and reaches the administrators as a notification with the **Approve** / **Reject** buttons — in the admin panel and in the app (see [7.3.5](/en/mobile/home#_735-administrator-panel)). Until the decision the person is not booked on the class and no seat in the class is taken.
  - One administrator decides on a request; a repeated decision on the same request is not executed.
  - Approval books the client on the class (status **Planned**, or **Waiting list** if the class waiting list is not empty) and sends them a message through the cascade: studio Telegram bot → Fitshandler Telegram account → SMS (see [Messages to clients](/en/pages/processing#_614-messages-to-clients)). For a booking with the **Waiting list** status the message is «<studio name> - Вашу заявку прийнято. Вас додано до листа очікування на тренування <date>. Після звільнення місця Вас буде записано автоматично та повідомлено.» (Your request has been accepted. You have been added to the waiting list…; see [Schedule — Waiting list](/en/menu/schedule#waiting-list)).
  - Rejection books nobody and sends no message.
  - A request for a class that has already passed can only be rejected.
- If the switch is off, the booking is created right after the code is confirmed and appears in the [schedule](/en/menu/schedule) and in the [client card](/en/menu/clients); the administrators receive the notification «Запис на тренування з веб сторінки: {workout}» (Booking from the web page: {workout}).
- While the waiting list of the class is not empty, a guest booking gets the **Waiting list** status. A client with the **Waiting list** status does not take up a seat.

The language of the page the booking was made from is saved in the client card and sets the language of SMS about a class cancellation or move.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

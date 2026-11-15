[Back to home](/en/)

# 7.8 Public Studio Page and Booking Without an Account

> No account is needed to view the studio's schedule and book a class. A person opens the studio page via a link or from the list of studios, chooses a class, and confirms their phone number with a code. They automatically become a client of the studio after their first booking.

---

## Where People Reach the Page From

- **Direct link.** Each studio has its own public link and QR code — they are on the [Settings → Mobile App](/en/login/settings#mobile-application) tab. The link can be printed, posted on social media, or sent to a client.
- **From the list of studios.** The app's start screen has a **"Browse Studios"** ("Переглянути студії") button. It opens the list of studios operating in the app, with a filter by city. The city is taken from the **City** field on the [Studio Information](/en/login/settings#studio-information) tab — if it is not filled in, the studio will not appear in the city filter.

---

## What's Visible on the Studio Page

- **Studio header**: logo, name, address, city and phone number, an **"About Us"** ("Про нас") button with the description and photos, and a star with the rating if there are enough ratings.
- **Schedule of upcoming group classes**: day, time, class name, coach. Personal classes and other people's personal data are not shown here.
- A button to book a specific class.

> ℹ️ The page only works when the studio has enabled the mobile app for clients on the [Settings → Mobile App](/en/login/settings#mobile-application) tab. If the app is disabled, the link opens a message stating the studio does not accept online bookings.

---

## How Booking Works

1. The person selects a class and taps to book.
2. They enter their name and phone number.
3. They confirm the number with a code. The code arrives **via Telegram**, and if the studio has connected SMS messaging and enabled the **"Confirm Guest Booking by SMS"** ("Підтвердження запису гостя по SMS") toggle — **SMS** can be chosen instead.
4. Once confirmed, a new client with this phone number appears at the studio, and the booking is submitted as a request.

> ℹ️ A request from the public page must be approved by a studio administrator. Until approval the person is not booked on the class and no seat is held for them. After approval the person is booked and receives a notice: studio Telegram bot → Fitshandler Telegram account → SMS.

> ℹ️ While the waiting list of the class is not empty, the booking (from an approved request or without approval) gets the **Waiting list** status, and the page shows "You have been added to the waiting list. Once a place becomes available, you will be booked automatically and notified." instead of "You're booked!". A client on the waiting list does not occupy a seat. An approved request that lands on the waiting list is notified with "Your request has been accepted. You have been added to the waiting list for the workout on <date>…" (see [Schedule — Waiting list](/en/menu/schedule#waiting-list)).

> ℹ️ If the number already belongs to a studio client, a new client is not created — the booking is attached to the existing card. This is exactly why the number is confirmed with a code: without it, someone could book under another person's name.

---

## Login for Existing Clients

The **"Already a client? Log in"** ("Вже клієнт? Увійти") button is shown **only in the installed app**. It is intentionally absent from the plain web page: the public page is meant for booking, not logging in, and its link is often opened by people who do not yet have the app.

---

## What the Studio Sees

- The client card is created right after the number is confirmed with a code, before the request is decided.
- The request appears among the studio notifications with approve and reject buttons. One administrator decides: a repeated decision on the same request is not executed.
- Approval books the client on the class (status **Planned**, or **Waiting list** if the class waiting list is not empty) and sends them a notice. Rejection books nobody and sends no notice.
- A request for a class that has already passed can only be rejected.
- If administrator approval of requests is disabled, the booking is created immediately after the code is confirmed and appears in the [schedule](/en/menu/schedule) and on the [client card](/en/menu/clients).

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

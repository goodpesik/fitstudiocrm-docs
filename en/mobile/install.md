<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.1 Installation and Login

> The **Fitshandler** app is installed from the **App Store** (iPhone) or **Google Play** (Android). Login uses a confirmation code delivered via Telegram or by SMS.

<!-- TODO: screenshot of the installation screen -->

---

## 7.1.1 Installation

The studio provides the app link as a QR code or the address `https://app.fitshandler.com`. Materials for handing out — the QR code, the link and the banner — are in [Settings → Mobile Application](/en/login/settings#mobile-application).

If the link is opened in a browser, the installation screen is shown:

- **«Hi!»**, «I'm your **Fitshandler**», «To get started, you need to install me»;
- the **«Install the app»** block with the **App Store** and **Google Play** badges, which open the app page in the store.

On the studio's public page in a browser, the same badges are opened by the **«Install»** button in the header; the **«Back»** button returns to the studio page.

> ⚠️ From 1 November 2026 the web version of the app added to the phone home screen (PWA) does not work on iPhone and Android: a window with a button to the App Store or Google Play is shown instead. The user's data (studios, profiles, bookings, plans) is stored on the server and is available in the store app after logging in with the same phone number.

---

## 7.1.2 First Launch

If the user is not logged in, the app opens the **«Choose a studio»** studio list (see [7.8](/en/mobile/guest#studio-list)). Browsing studios and schedules does not require logging in. Login is offered by the **«Sign in»** / **«Log in»** buttons — in the studio list («Already have an account? Sign in»), on Home and on the studio page.

---

## 7.1.3 Login

The login screen contains:

- **«Hi!»** and the name of the selected studio (if a studio is selected);
- the hint «Choose how to confirm your phone number.»;
- the **«Log in with Telegram»** button with the caption «The bot will send a confirmation code in Telegram»;
- the **«Via SMS»** button — shown if a studio is selected and the studio has turned on SMS confirmation (the **«Підтвердження запису гостя по SMS»** (Guest booking confirmation by SMS) switch). If no studio is selected, «To log in by SMS, pick a studio first.» is shown instead of the button;
- the **«Browse studios»** link;
- the **«Back»** button.

### Login with Telegram

1. **«Log in with Telegram»** opens the Telegram bot. In the bot the user shares their phone number — the bot sends a 6-digit code.
2. The app shows the **«Enter the code»** screen with the hint «Open the bot, share your contact, and enter the code you receive.»
3. The user enters the 6 digits and taps **«Log in»**. The button is active only after all 6 digits are entered.
4. The line «No code? **Request another code**» opens the bot again.

### Login by SMS

1. **«Via SMS»** opens the **«Your number»** screen («We will send the code to this number by SMS») with a field in the format `+38 (0__) ___-__-__`.
2. **«Send code»** sends the code. The code is delivered through the first available channel: the studio's Telegram bot (if the user has already talked to the bot), the Fitshandler Telegram account (if the number is registered in Telegram), SMS.
3. On the **«Enter the code»** screen the hint matches the channel: «We sent the code to you on Telegram from the Fitshandler account. Enter it here.» or «Enter the code from the SMS.»
4. The user enters the 6 digits and taps **«Log in»**.

If SMS is unavailable for the studio, the **«Via Telegram»** button is shown on the number screen instead of **«Send code»**.

> ℹ️ The code is valid for 10 minutes. The client app has no password and no Google login. The session is stored on the device: logging in again on every launch is not required.

---

## 7.1.4 After Login

- A user with profiles in studios selects a studio and a profile (see [7.2.3](/en/mobile/registration#_723-studio-and-profile-selection)).
- A user without a client card in the selected studio sees Home in the **Guest** role and can submit a booking request (see [7.2](/en/mobile/registration)).
- If notifications are off, the app offers to turn them on (see [7.3.6](/en/mobile/home#_736-offer-to-enable-notifications)).

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

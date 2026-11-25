<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.1 Installation and Login

> The **Fitshandler** app is installed from the **App Store** (iPhone) or **Google Play** (Android). Login uses the phone number and a confirmation code delivered via Telegram or by SMS.

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

Login uses only the phone number and a confirmation code. The user does not choose the code delivery channel: the system defines it. The client app has no password, no Google login and no Telegram bot login.

Login is possible only in the context of a studio: the confirmation code is issued by the selected studio. If no studio is selected, the login screen shows **«To log in, pick a studio first.»** («Щоб увійти, спершу оберіть студію.») and the **«Browse studios»** button.

### Phone Number

1. The login screen shows **«Hi!»**, the name of the selected studio, the hint «Enter your phone number. The confirmation code will arrive in Telegram or by SMS.», a field in the format `+38 (0__) ___-__-__` and the **«Browse studios»** link.
2. Once the full number is entered, the **«Send code»** button becomes active.
3. **«Send code»** sends a 6-digit confirmation code:
   - via **Telegram** — if the user already talks to the bot or the number can be found in Telegram;
   - by **SMS** — in other cases.
4. If the code is not sent, one of the following messages is shown:

| Message | Condition |
|---|---|
| «Не вдалося надіслати код на цей номер. Зверніться до адміністратора студії.» (The code could not be sent to this number. Contact the studio administrator.) | The studio has no SMS messaging connected, and the code cannot be delivered via Telegram |
| «Наразі неможливо надіслати код SMS-повідомленням. Спробуйте пізніше.» (The code cannot be sent by SMS right now. Try again later.) | The studio's monthly SMS limit is used up, or the request rate limit applies |
| «Не вдалося надіслати код. Спробуйте ще раз.» (Could not send the code. Try again.) | Any other sending error |

After a failed send, the **«Send code»** button is inactive for 5 seconds and shows «You can try again in N s» («Повторити спробу можна через N с») instead of its label.

### Entering the Code

1. The **«Enter the code»** screen shows the channel the code was sent through: «Код надіслано вам у Telegram. Введіть його тут.» (The code was sent to you in Telegram. Enter it here.) or «Введіть код з SMS.» (Enter the code from the SMS.) If a repeated code request fails, the hint keeps the channel of the last code sent. After returning to the app (for example, from Telegram or Messages) and after the screen is restored, the hint is the same.
2. The user enters the 6 digits and taps **«Log in»**. The button is active only after all 6 digits are entered. The code can be pasted from the message as a whole.
3. The line «No code? **Request another code**» is available 60 seconds after the previous send; until then «You can request another code in N s» is shown. If a repeated request fails, the button is inactive for 5 seconds and shows «You can try again in N s».
4. The **«Back»** button returns to the number entry.

> ℹ️ The code is valid for 10 minutes and is checked together with the number it was sent to.

> ℹ️ If the app is closed or restarted while the code is awaited, within 20 minutes after the code was sent the login screen opens directly on the code entry with the same number.

> ℹ️ The session is stored on the device: logging in again on every launch is not required.

---

## 7.1.4 After Login

- A user with profiles in studios selects a studio and a profile (see [7.2.3](/en/mobile/registration#_723-studio-and-profile-selection)).
- A user without a client card in the selected studio sees Home in the **Guest** role and can submit a booking request (see [7.2](/en/mobile/registration)).
- If notifications are off, the app offers to turn them on (see [7.3.6](/en/mobile/home#_736-offer-to-enable-notifications)).

### Session Duration

- The login is kept while the user uses the app.
- If the app is not used for 90 days, the login ends; on the next launch the app shows the login screen.
- **«Log out»** in the Account tab (see [Account](/en/mobile/account)) ends the login on all of the user's devices. On the other devices the app shows the login screen at the next request to the server.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

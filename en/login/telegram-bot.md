<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# Telegram bot

> There is no separate **Телеграм-бот** (Telegram bot) tab in the settings. The QR code and banner for installing the app, the counters of registered clients and coaches and the message broadcast are on the [Settings → Mobile Application](/en/login/settings#mobile-application) tab.

## Bot functions

The Telegram bot has two functions:

1. **Signing in to the mobile app with a code.** When signing in through Telegram, the bot asks to share the phone number («Вітаю! Будь ласка натисніть на кнопку Поділитися номером телефону.», Hello! Please press the Share phone number button) and sends a code: «Введіть цей код для входу у додаток.(код дійсний впродовж 10 хв)» (Enter this code to sign in to the app (the code is valid for 10 min)). The code is valid for 10 minutes. If the client is already signed in, the bot replies «Ви вже увійшли у додаток» (You are already signed in to the app).
2. **Delivering messages** to clients who signed in through the bot: visit reminders, messages about cancelled, cancelled-booking and moved sessions, booking confirmations, requests to rate the session. Channel order — [Messages to clients](/en/pages/processing#_614-messages-to-clients).

To any other message the bot replies «Чат бот припинив свою роботу» (The chat bot has stopped working) with an offer to install the Fitshandler app (button **Встановити Додаток**, Install the app).

## The Fitshandler Telegram account

Clients who did not sign in through the bot receive Telegram messages from the Fitshandler account at the client's phone number, if the number is registered in Telegram. If a Telegram message cannot be sent, an SMS is sent — under the conditions described in [Messages to clients](/en/pages/processing#_614-messages-to-clients).

After a visit reminder or a rating request sent in Telegram, a client without the app receives a second message «Встановіть додаток Fitshandler <link>» (Install the Fitshandler app).

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

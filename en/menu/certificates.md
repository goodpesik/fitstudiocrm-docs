<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.10 Gift certificates

> **Certificates** ("Сертифікати") — gift certificates that the studio sells. A certificate holds prepaid memberships and has a unique number and a QR code. A certificate is redeemed by an administrator: from the certificates table, with the scanner, or by number.

![](../../_media/certificates-overview.png ':size=400x241')

---

## 3.10.1 Certificates table

**Columns:**

| Column | Description |
|---|---|
| **Certificate number** ("Номер сертифікату") | A unique code of the form `CRT…`. Next to it: copy the number (notification "Скопійовано", copied) and show the QR code. |
| **Price** ("Ціна") | The certificate price in UAH. |
| **Memberships** ("Абонементи") | The memberships the client receives on redemption (`--` when there are none). |
| **Status** ("Статус") | **Активний** (active) / **Погашено** (redeemed) / **Прострочено** (expired). |
| **Date used** ("Дата використання") | Redemption date (`--` if not redeemed). |
| **Client who used it** ("Клієнт що використав") | The client the certificate was redeemed for. |
| **Date of sale** ("Дата продажу") | The date the certificate was sold. |
| **Expiration date** ("Дата закінчення дії") | The date after which the certificate becomes expired. Edited in the table (the **Редагувати** (edit) column, SuperAdmin and Admin roles). |
| **Comment** ("Коментар") | Text from the sale form or `--`. |
| **Actions** ("Дії") | **Погасити** (redeem, only for an active certificate) and **Видалити** (delete, requires confirmation); SuperAdmin and Admin roles. |

**Search** — the **Пошук** field above the table. The table is paginated (10, 20 or 50 rows). If there are no certificates, "Не знайдено жодного сертифікату" is shown.

---

## 3.10.2 Creating a certificate

> The **+** button is available only while a **shift is open**, to the **SuperAdmin** and **Admin** roles.

![](../../_media/cert-add-modal.png ':size=400x241')

**Fields of the "Створення Сертифікату" (create certificate) window:**

- **Memberships** — rows with the **Виберіть абонемент** (choose a membership) field and a quantity (1 to 20); the **Додати абонемент** (add membership) button adds a row. The certificate price is the sum of the selected memberships' prices times their quantities.
- **Certificate validity (months)** ("Термін дії сертифікату (міс.)") — the number of months from the date of sale; 3 by default, at least 1 ("Значення не може бути меньшим за 1").
- **Comment** ("Коментар") — optional (for example, "Подарунок на 8 березня" — "Gift for March 8").
- **Payment method** — Card / Cash / Bank transfer. The **Split payment** ("Розділити оплату") button adds another payment method.
- **Discount (discount amount)** ("Знижка (сума знижки)") and the **Відсотки %** (percent) toggle — a fixed or percentage discount.
- **Amount due** ("До сплати") — the final amount after the discount.

Buttons: **Close** ("Закрити"), **Save** ("Зберегти").

After saving:

- a register sale transaction is created (in the [Point of sale](/en/menu/pos) the client is shown as **Сертифікат**); with an active fiscal integration it is fiscalized with a receipt line "Подарунковий сертифікат" (gift certificate);
- the certificate gets a unique number (format `CRT…`) and appears in the table with the **Active** status.

---

## 3.10.3 QR code

> The QR-code button in a certificate's row opens the **QR Code** window with the certificate's QR code.

![](../../_media/cert-qr-modal.png ':size=260x157')

- **Copy** ("Скопіювати") — copies the QR code as an image to the clipboard, for sending to the client.
- The QR code holds the certificate number; on redemption it is read with the scanner.

---

## 3.10.4 Redemption

> The **Погасити** (redeem) button in a certificate's row, scanning the QR code, or the **Сертифікат** (certificate) button in the [Registration](/en/menu/clients#_329-registration) window opens the **Погашення Сертифікату** (certificate redemption) window.

**Process:**

1. Scan or enter the certificate number (the **Відскануйте або введіть номер сертифікату** field) and click **Шукати сертифікат** (find certificate), unless the window was opened from a table row.
2. Choose a client (**Виберіть клієнта**) or create a new one with the **Новий клієнт** (new client) button.
3. Click **Погасити** (redeem).

Result:

- Each membership of the certificate (with its quantity) is added to the client with the **Неактивний** (inactive) status.
- The certificate gets the **Redeemed** status; the redemption date and the client are recorded automatically.
- No register transaction is created on redemption: the payment was made when the certificate was sold.
- The memberships are added and the certificate is marked redeemed in one operation: on a refusal no membership is added and the certificate status does not change.
- A certificate is redeemed only once. A repeated redemption, including a simultaneous one from another device, is refused.
- A certificate is valid through the last day of its validity period in the studio's time zone inclusive. A certificate without an expiration date does not expire.

**Search errors:**

| Message | Condition |
|---|---|
| Сертифікат за номером <number> не знайдено !!! | The number does not exist |
| Сертифікат прострочено!!! | The certificate has the **Expired** status |
| Сертифікат вже погашено!!! | The certificate has the **Redeemed** status |

**Redemption refusals** (checked when **Погасити** (redeem) is clicked; the message is shown in the error window):

| Message | Condition |
|---|---|
| Сертифікат уже погашено. Повторне погашення неможливе. | The certificate was redeemed earlier, including from another device after the window was opened |
| Термін дії сертифіката минув. Погашення неможливе. | The last day of the validity period has passed in the studio's time zone, or the certificate has the **Expired** status |
| Абонемент, зазначений у сертифікаті, відсутній у довіднику. Погашення неможливе. | A membership of the certificate was deleted from the memberships catalogue |
| Клієнта не знайдено. | The chosen client was deleted |

---

## 3.10.5 Statuses

| Status | Colour | Condition |
|---|---|---|
| **Active** ("Активний") | green | The certificate is neither redeemed nor expired. |
| **Redeemed** ("Погашено") | orange | The certificate has been redeemed for a client. |
| **Expired** ("Прострочено") | red | The current date is later than the expiration date. |

> ℹ️ The **Expired** status is set by a nightly job every day at 02:00 server time — the same for all studios, regardless of their time zones.
> ℹ️ **Delete** removes the certificate from the system permanently; there is no separate "Cancelled" status.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

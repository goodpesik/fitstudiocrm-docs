<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.10 Gift certificates

> **Gift certificates** are vouchers the studio can issue or sell. A certificate holds prepaid sessions / memberships and has a unique number and a QR code. A client redeems a certificate through an administrator, who opens the redemption window either directly from the certificates list or by scanning the QR code.

![](../../_media/certificates-overview.png ':size=400x241')

---

## 3.10.1 Certificates table

**Columns:**

| Column | Description |
|---|---|
| **Certificate number** | A unique code in the form `CRT…`. Next to it, buttons to copy (`pi-copy`) and show the QR code (`pi-qrcode`). |
| **Price** | Cost of the certificate in UAH. |
| **Memberships** | List of memberships the client will receive upon activation (`--` until activated). |
| **Status** | Active / Redeemed / Expired. |
| **Date used** | Date the client activated it (`--` if not used). |
| **Client who used it** | Name of the client who activated the certificate. |
| **Date sold** | When the certificate was sold. |
| **Expiration date** | Date after which the certificate becomes Expired. Editable directly in the table via the **Edit** (pencil icon) column in the certificate's row. |
| **Comment** | Optional text, added on the sale form. |
| **Actions** | **Redeem** (activate), **Delete** (delete), **Row Edit** (edit the expiration date). |

**Search** — by number, client, or comment — a field at the top of the table.

---

## 3.10.2 Creating a certificate

> The **+** button is only available when the **shift is open** and the user has the **SuperAdmin** or **Admin** role.

![](../../_media/cert-add-modal.png ':size=400x241')

**Fields in the "Create certificate" modal:**

- **Certificate validity (months)** ("Термін дії сертифікату (міс.)") — how many months the certificate is valid for from the date of sale. After this period, its status automatically becomes **Expired**.
- **Comment** — optional (for example, "Подарунок на 8 березня" — "Gift for March 8").
- **Payment method** — Cash / Card / Bank transfer. The **Split payment** ("Розділити оплату") button lets you add an additional payment method (split pay).
- **Discount (discount amount)** ("Знижка (сума знижки)") + the **Percent %** ("Відсотки %") toggle — a fixed or percentage discount off the price.
- **Amount due** ("До сплати") — the final amount after the discount.

After saving:
- a sale transaction is created (fiscalized if PRRO is active),
- the certificate receives a unique number (format `CRT…`),
- it appears in the table with **Active** status,
- the memberships (`plans`) remain empty — the admin assigns them when the client [redeems](#_3104-Activation-Redeem) the certificate.

> ℹ️ The expiration date can be changed later via **Edit** (`pi-pencil` icon) in the certificate's row.

---

## 3.10.3 QR code

> Clicking the **🔳 QR** button (QR code icon) in a certificate's row opens a modal window with the certificate's QR code.

![](../../_media/cert-qr-modal.png ':size=260x157')

- **Copy** ("Скопіювати") — copies the QR code as an image to the clipboard, for sending to the client.
- The QR code contains the certificate number — the client shows it upon activation, and the admin scans it with the card scanner.

---

## 3.10.4 Activation (Redeem)

> The **🎟 Redeem** ("Погасити", ticket icon) button in a certificate's row, or scanning the QR code, opens a separate redemption window pre-loaded with the memberships from the certificate.

**Process:**

1. Select or create a client.
2. Click **Redeem** ("Погасити").
3. The certificate receives **Redeemed** status; the activation date and `clientId` are recorded automatically.
4. A fiscal transaction with no payment is created (method **Certificate**), and the membership(s) are added to the client.

---

## 3.10.5 Statuses

| Status | Color (badge) | Condition |
|---|---|---|
| **Active** | green (success) | The certificate has not been used and has not expired. |
| **Redeemed** | orange (warn) | The client has activated the certificate. |
| **Expired** | red (danger) | The current date has passed the expiration date. |

> ℹ️ Expiration is calculated automatically by a nightly job that runs daily at 02:00 — the same time for all studios, regardless of their time zone.
> ℹ️ Deleting (`Delete`) permanently removes the certificate from the system — there is no separate "Canceled" status.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

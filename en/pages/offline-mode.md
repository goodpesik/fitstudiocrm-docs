# Offline mode

Offline mode lets a till computer with Device Handler installed work without internet and while the Fitshandler server is unavailable. Operations made without a connection are sent to the server once the connection is back.

## Devices and access

### Enabling on a computer

- Offline mode is enabled separately for each till computer.
- A user with the **Super Admin** or **Admin** role, signed in on that computer, can enable offline mode. A user with the **Manager** role gets `403`.
- On enabling, the computer receives a device access — a separate key bound to the studio, the user and the computer.
- The key is passed to the computer once. The server stores only its hash; the key cannot be restored from the server data.
- One user on one computer has one valid device access. Enabling again issues a new access; the previous one stops working.
- A device access opens only the data exchange of the offline till with the server: sending offline operations and receiving the till data. Other sections of the system are not available with a device access.

### Access validity

- A device access is valid for 7 days from the computer's last contact with the server, not from the day it was enabled.
- Every request of the computer to the server extends the validity by 7 days from that request. A computer that contacts the server daily does not lose access.
- A computer that has not contacted the server for more than 7 days loses access. Offline mode on it must be enabled again while it is online.
- The access stops working if the user it was issued to no longer has a role with access to the system.

| Parameter | Value |
|---|---|
| Access validity | 7 days from the last contact |
| Validity update | at most once every 5 minutes |
| Valid accesses per user and computer | 1 |

### Device list and revoking

- A user with the **Super Admin** or **Admin** role sees the list of valid device accesses: device name, user, date enabled, date of last contact, expiry date.
- The **Revoke** button stops the device access at once. The next request of the computer with this access is refused; offline mode on it must be enabled again.
- A revoked access and an expired access are not shown in the list.

| Request with a device access | Server response |
|---|---|
| Access revoked, expired, or the user has no role with access | `401` |
| A section the device access does not open | `403` |
| Data of another computer than the one the access was issued to | `403`, code `DEVICE_MISMATCH` |

## Data available without internet

The offline till works with the data received from the server at the last connection. The offline banner shows when the data was received: "Data as of …".

### Contents

| Data | What is sent |
|---|---|
| Plans | every plan of the studio with its price, number of sessions and duration |
| Categories | every workout category |
| Products | name, price, stock |
| Coaches | name, colour, categories; phone and birthday are not sent |
| Rooms | name, capacity |
| Workouts | recurring workout templates in effect within the schedule window, and one-time workouts of the schedule window |
| Clients | first name, last name, type, card number, vacations (freezes), personal account balance and time of the last personal account operation; phone, email and birthday are not sent |
| Client plans | active, not yet activated and frozen plans, including plans shared across a studio network, with sessions left, sessions at the start of the plan (`initialWorkouts`) and validity; ended plans are not sent |
| Debts | unpaid debts with total amount (`totalAmount`), amount left to pay (`remainingAmount`), contents and clients; the amount left to pay equals the one on the client's debt screen |
| Certificates | active certificates within their validity only: number, description, price, plans of the certificate, validity, client, status |
| Sales | sales and personal account top-ups from the start of the day 3 days back in the studio time zone, except sales of the current online shift: lines, amount, payment method, paid from the personal account flag, top-up flag, invoice payment confirmation flag, paid through a terminal flag, refunds made, fiscalization state, fiscal card id |
| Shifts | closed shifts from the start of the day 3 days back in the studio time zone; the current online shift is not sent |
| Schedule | workouts from 3 days before today to 7 days after it, with booked clients and the number of taken seats; recurring workouts on dates with no workout created yet, from today on, with their regular clients |
| Self check-in codes | ready QR links for every hour of the next 48 hours: for all rooms, for each room alone and for the room sets the till asks for; only when self check-in is on; the state of the codes is in the `checkInCodesStatus` field |
| Settings | studio name and time zone, shift and booking parameters, self check-in parameters, printers; fiscal and acquiring cards — id, name, type and active flag only |

- Keys, tokens, cashier PIN codes, licence keys and the self check-in signing secret are not sent to the till computer.
- A self check-in code from the till's data is the code the server accepts in that hour. The server accepts the previous hour's code for 10 more minutes after the hour changes.

### Full package and updates

- The full package contains all the data in the table.
- An update (a request with the `since` parameter) contains all the data except plans, categories, products (name and price), coaches, rooms, workouts and settings. Product stock is sent in an update as a separate list.
- Every list of an update is complete: the till replaces its list with the one received. A record missing from an update list (a redeemed or expired certificate, a paid or deleted debt, an ended plan) is removed by the till.
- A product sale, a personal account payment, a certificate redemption and a refund made online or in the app appear in the offline till after the next update.

### Technical parameters

| Parameter | Value |
|---|---|
| Request | `GET /offline/snapshot`, with device access only |
| Update | `since` parameter — the `generatedAt` of the previous package |
| Room sets for check-in codes | `checkInRooms` parameter: sets separated by `;`, room ids in a set separated by `,`; up to 20 sets |
| Response fields | `version`, `generatedAt`, `full`, `window` (schedule bounds), `salesFrom` (start of the sales period), `catalog` (full package only), `clients`, `clientPlans`, `clientDebts`, `certificates`, `stock`, `transactions`, `shifts`, `occurrences`, `checkInCodes`, `checkInCodesStatus` |
| Workout with no record created | `projected: true`, `id: null` |

| `checkInCodesStatus` | Meaning |
|---|---|
| `ready` | self check-in codes are sent in `checkInCodes` |
| `off` | self check-in is off; `checkInCodes` is `null` |
| `failed` | self check-in is on, the codes could not be built; `checkInCodes` is `null`; the rest of the data is sent |

| Response | Meaning |
|---|---|
| `403`, code `DEVICE_TOKEN_REQUIRED` | request without device access |
| `400`, code `INVALID_SINCE` | `since` is not a date or is later than the server time |
| `400`, code `TOO_MANY_ROOM_SETS` | more than 20 sets in `checkInRooms` |

## One-time application of operations

- Every till action receives an operation id at the moment of the click. The id does not change when the action is sent again.
- An action the till received no server response to (connection drop, server unavailable) is sent again with the same id — online or during the sync of the offline queue. The server applies an operation at most once: sending it again returns the stored result; no second sale, payment or booking is created.
- The stored result is returned in the form the first server response had it (JSON): dates as ISO 8601 strings, money amounts in the same format as in the first response.
- The same id with another operation content is refused.
- A sale, refund, debt payment or booking stopped after a step that cannot be undone (a cash ledger row, a fiscal receipt, a write to the class roster) is not run again. Such an operation gets the `conflict` result with the `OPERATION_INTERRUPTED` code and needs an admin's review. This also applies to an operation whose delivery did not finish within 2 minutes.
- An operation stopped before the first such step leaves no changes; sending it again with the same id runs it.
- An operation of a version above the one the server supports is not applied and changes no data. The operation stays in the computer's queue and is applied after the server is updated.
- An action without an operation id runs as an ordinary online action.

These till actions accept an operation id:

| Action | Operation kind |
|---|---|
| Sale, including payment from the personal account | `sale` |
| Sale refund | `refund` |
| Debt payment, including from the personal account | `debt_payment` |
| Booking a client for a class | `booking` |
| Creating a client | `client_create` |
| Certificate sale | `certificate_sale` |
| Certificate redemption | `certificate_redeem` |

### Technical parameters

| Parameter | Value |
|---|---|
| Online action header | `X-Operation-Id`, UUID |
| Offline queue sync | `POST /offline/sync`, up to 200 operations per request |
| Operation fields | `id` (UUID), `kind`, `version`, `occurredAt` (ISO 8601), `payload` |
| Operation time | not earlier than 30 days and not later than 5 minutes from the server time |

| Code | Meaning |
|---|---|
| `IDEMPOTENCY_KEY_REUSED` | the id was already used for another operation; an online action gets `409` |
| `OPERATION_IN_PROGRESS` | another delivery is applying the operation with this id; an online action gets `409` with this code, retry later with the same id |
| `OPERATION_INTERRUPTED` | the operation stopped after a step that cannot be undone; it is not run again; an online action gets `409`; an admin's review is needed |
| `INVALID_VERSION` | the operation version is not a whole number from 1; the operation is refused |
| `RETRY` | the server could not apply the operation; send it later |
| `INVALID_OPERATION_ID` | the `X-Operation-Id` header is not a UUID; response `400` |
| `OP_VERSION_UNSUPPORTED` | the operation version is above the one the server supports; the operation stays in the queue |
| `OP_KIND_UNSUPPORTED` | the server does not apply this operation kind yet; the operation stays in the queue |

During sync every operation gets its own result:

| Result | Meaning |
|---|---|
| `applied` | the operation is applied (or was applied earlier; the stored result is returned) |
| `rejected` | the operation is refused; sending it again returns the same |
| `conflict` | the operation contradicts changes made meanwhile, or it stopped after a step that cannot be undone; an admin decision is needed |
| `retry` | the operation is not applied now; send it later, the next operations of the queue wait |
| `in_progress` | another delivery is applying the operation |
| `pending` | the operation was not looked at: an earlier operation of the queue is not applied yet |

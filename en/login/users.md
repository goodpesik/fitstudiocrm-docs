<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 1.3.2.1 Users

![](../../_media/admin-panel-users.png ':no-zoom')

> The **Users** tab shows a table of users who have been **invited** to this studio. Each studio keeps its own separate list of users.

> **`Important:`** a user is now **no longer added automatically** after signing in. They must first be invited by email (see below). If a person signs in through Google but was not invited to the studio — they **will not get access** and **will not appear** in this list.

---

### The table contains:

- **Login** (pulled from Google after the first sign-in)
- **Name** (can be changed)
- **Email** (used for the invitation and for linking the Google account)
- **Phone** ("Телефон")
- **Role** (can be changed)
- **Actions** (**Delete** ("Видалити") and **Edit** ("Редагувати") buttons) — available only to the **Super Admin** ("Супер Адмін") and **Admin** ("Адмін") roles. A **Manager** ("Менеджер") sees the table but cannot change records.

The edit form contains: **Name** ("Імʼя"), **Phone** ("Телефон"), **Hourly rate**
("Ставка за годину") — used to calculate the administrator's payroll — **Role** ("Роль"),
and the **Earn bonuses** ("Нараховувати бонуси") toggle.

---

## Add a User (invitation by email)

> Above the table there is an add row: an **Email of the new user** ("Email нового користувача") field, a **role** selector, and an **Add** ("Додати") button.

1. Enter the **email** of the person you want to add to the studio.
2. Choose a **role** — **Manager** or **Admin** are available.  
   **`The "Super Admin" role cannot be requested`** — it is granted separately at the system level.
3. Click **Add**. The message *"User added"* ("Користувача додано") appears, and the record shows up in the table immediately.

> The **Add** button is inactive until a valid email is entered, or if a user with that email is **already** on the list.

**What happens next:**

- An invitation is created for that email with the assigned role (for now, the account "awaits sign-in").
- When the invited person **signs in through Google for the first time** using the same email, their Google account is linked to the invitation, and they immediately get access to the studio with the assigned role.
- A single user can have access to several studios under their email — after signing in, they choose the studio they need.

---

## The **Delete** Button

1. You cannot delete your own user.
2. If you click the **Delete** button and deletion is possible, the ["Are you sure you want to continue?" modal window](../_modals/are-you-sure-modal.md ':include') appears.  
   If confirmed — the selected user is removed from the studio.  
   **`Warning! This action is irreversible.`**

---

## The **Edit** Button

> Clicking the edit button (pencil icon) opens the user's page.

![](../../_media/admin-panel-edit-user.png ':no-zoom')

Possible actions:

- Change the name.
- Change the phone number.
- Change or set the hourly rate (used for salary calculation).
- Change the role.  
  **`Warning! This action can only be performed by a user with the "Super Admin" role.`**
- Turn **Earn bonuses** ("Нараховувати бонуси") on or off.

---

## The **Earn bonuses** toggle

> Not every administrator works on bonuses, so it is switched on per person.

Switched off, that person earns nothing: neither the bonus for a sale they rang up
themselves, nor a share of the bonus split among administrators. And the split counts
**only** the administrators who are on bonuses — the rest share the same sum between
them rather than losing it along with the excluded colleague.

> ℹ️ The default is **on**, so nothing changes for anyone already in the system.
> Bonuses are calculated by the payroll report, which is what reads this value.

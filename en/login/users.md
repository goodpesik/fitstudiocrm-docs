<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 1.3.2.1 Users

![](../../_media/admin-panel-users.png ':no-zoom')

> The **Користувачі** (Users) tab shows a table of users invited to the studio. Each studio has a separate list of users.

> Access to the studio is granted only by an email invitation (see below). A person who signed in through Google without an invitation gets no access and does not appear in the list.

Above the table the plan limit indicator «Користувачі: <used> / <limit> · ще N» (Users: … · N more) is shown (see [Plan and access to the system](/en/login/billing#plan-limits)).

---

### The table contains:

- **Логін** (Login) (from the Google account after the first sign-in)
- **Імʼя** (Name)
- **Емайл** (Email) (used for the invitation and for linking the Google account)
- **Телефон** (Phone)
- **Роль** (Role)
- The **Видалити** (Delete) and **Редагувати** (Edit) buttons — available to the **Супер Адмін** (Super Admin) and **Адмін** (Admin) roles. The **Менеджер** (Manager) role sees the table without the buttons.

---

## Add a user (invitation by email)

> Above the table there is an add row: the **Email нового користувача** (New user's email) field, the role selection and the **Додати** (Add) button.

1. Enter the person's email.
2. Select the role — **Менеджер** or **Адмін**. The **Супер Адмін** role cannot be invited: it is granted at system level.
3. Click **Додати**. The message «Користувача додано» (User added) appears and the record is shown in the table.

> The **Додати** button is inactive until an email with the `@` character is entered, or if a user with this email is already in the list.

**After the invitation:**

- When the invited person first signs in through Google with the same email, their account is linked to the invitation and they get access to the studio with the assigned role.
- One email can have access to several studios; switching — with the **Змінити студію** (Switch studio) item of the user menu.

---

## The **Видалити** button

1. You cannot delete your own user: the button is inactive with the hint «Неможливо видалити свого користувача» (You cannot delete your own user).
2. For other users the button opens the [«Ви впевнені що хочете продовжити?» modal](../_modals/are-you-sure-modal.md ':include').
   After confirmation the user is removed from the studio and the message «Користувача успішно видалено» (User deleted successfully) appears.
   **`Attention! This action is irreversible.`**

---

## The **Редагувати** button

> The edit button (pencil icon) opens the user form under the table.

![](../../_media/admin-panel-edit-user.png ':no-zoom')

Form fields:

- **Імʼя** (Name);
- **Телефон** (Phone);
- **Ставка за годину** (Hourly rate) — used to calculate the [administrator salary](/en/pages/processing#_64-calculating-administrator-salaries);
- **Роль** (Role) — **Не задано** (Not set), **Супер Адмін**, **Адмін**, **Менеджер**. Only a user with the **Супер Адмін** role can change roles; you cannot change your own role;
- the **Нараховувати бонуси** (Accrue bonuses) switch — shown when the **Адмін** role is selected.

Buttons **Назад** (Back) and **Зберегти** (Save). After saving, the message «Користувача успішно оновлено» (User updated successfully) appears.

---

## The **Нараховувати бонуси** switch

The switch defines whether the user receives bonuses from [Settings → Features → Administrator Bonuses](/en/login/settings#administrator-bonuses).

- Off — the user receives neither the bonus for their own sale nor a share of a bonus split between administrators. A split bonus is distributed only among administrators with the switch on.
- The switch is on by default.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

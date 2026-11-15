[Back to home](/en/)

# 1. Login and Users

---

## 1.2 Login Window

The **Логін в систему** (Sign in to the system) window contains the **Увійти** (Sign in) button; sign-in is done with a Google account.

Access is granted **by invitation**: a studio administrator adds the email address on the [Users](/en/login/users) tab with a role. The person then signs in through Google with the same email and gets access to the studio.

![](../../_media/login-screenshot.png ':size=100x53')

---

If there is no access after signing in (the email was not invited or the role is **Не задано**, Not set), the message **Доступ заборонено** (Access denied) — «Зверніться до адміністратора для отримання доступу» (Contact the administrator to get access) — and the **Вийти** (Sign out) button are shown.

![](../../_media/access-denied-screenshot.png ':size=100x63')

A studio employee should give their email to an administrator who has access, so that the administrator adds it on the [Users](/en/login/users) tab. One email can have access to several studios.

If the studio's access is suspended by the plan, the message **Акаунт деактивовано** (Account deactivated) is shown — see [Plan and access to the system](/en/login/billing).

> System-level access (including the **Супер Адмін**, Super Admin, role) is granted by the [system administrator](mailto:fitshandler@gmail.com).

---

## 1.3 User Menu and Roles

After signing in, the main interface of the system is shown.

> The user avatar (from the Google account) is shown in the top-right corner. Clicking it opens the menu:

- User name
- **Профіль** (Profile)
- **Змінити студію** (Switch studio) — if the user has access to several studios
- **Вийти з системи** (Sign out of the system) — after confirmation in the [«Ви впевнені що хочете продовжити?» window](../_modals/are-you-sure-modal.md ':include')
- **Тариф: <name>** (Plan) and **Оплатити** (Pay) — see [Plan and access to the system](/en/login/billing)

The **Налаштування** (Settings) item is in the main menu at the top.

![](../../_media/header-screenshot.png ':size=100x19')

---

### 1.3.1 User Name

> A text element: the user's name in the system.

---

### 1.3.2 Profile

> The **Профіль** item opens a window with the user's photo and name and a form:

- **Імʼя** (Name) — required («Обов’язкове поле», Required field);
- **Телефон** (Phone) — format `0XXXXXXXXX` («Номер має бути у форматі 0XXXXXXXXX», The number must be in the format 0XXXXXXXXX).

The **Зберегти** (Save) button is active when the field values are valid. The window is closed with the cross in the top-right corner.

![](../../_media/profile-screenshot.png ':size=100x27')

> If **Зберегти** is clicked with no changes, the [«Дані не змінилися» modal](../_modals/nothing-changed-modal.md ':include') appears.

> If the data was changed, clicking **Зберегти** opens the [«Ви впевнені що хочете продовжити?» modal](../_modals/are-you-sure-modal.md ':include').

---

### 1.3.3 Settings

> The **Налаштування** item in the main menu opens a page with tabs:

- [Users](/en/login/users)
- [Settings](/en/login/settings#settings)
- [Features](/en/login/settings#features)
- [Integrations](/en/login/settings#integrations) — only for the **Супер Адмін** role
- [Information](/en/login/info)
- [Mobile Application](/en/login/settings#mobile-application)
- [Reminders](/en/login/settings#reminders)
- [Categories](/en/login/settings#categories)
- [Studio Information](/en/login/settings#studio-information)

---

[Back to home](/en/)

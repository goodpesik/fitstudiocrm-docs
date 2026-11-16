# Personal cabinet (subscription management)

The **personal cabinet** is at **clients.fitshandler.com**. It is the owner's cabinet for managing **studios**, **subscription and payment**, **plans**, **groups (studio networks)** and contacting **support**.

One cabinet account can have **several studios**. Each studio is a separate working database with its own admin panel.

---

## 1. Signing in to the cabinet

The **Вхід до кабінету** (Sign in to the cabinet) window, button **Увійти через Google** (Sign in with Google). The cabinet is tied to the Google email: all of the owner's studios are available under this sign-in.

If the account is disabled, the message «Обліковий запис вимкнено, тому доступ до кабінету закрито. Увімкнути його знову може адміністратор.» (The account is disabled, so access to the cabinet is closed. An administrator can enable it again.) is shown.

---

## 2. My tenants

The main tab of the cabinet is **Мої тенанти** (My tenants): the list of studios with their plan, validity date and status.

If there are no studios, «Для початку роботи натисніть «Новий тенант»» (To get started, click «Новий тенант») and the **Запланувати консультацію** (Schedule a consultation) button are shown.

**Table columns:**

- **Назва** (Name) — studio name; clicking it opens the studio card (see 3).
- **Продукт** (Product) — product (fitstudiocrm).
- **План** (Plan) — current plan and its price.
- **Діє до** (Valid until) — the date until which the subscription is paid.
- **Статус** (Status) — studio state, for example «Активний» (Active), «Очікує першої оплати» (Awaiting first payment), «Пробний · залишилось N дн.» (Trial · N days left), «буде видалено після закінчення плану» (will be deleted after the plan ends).
- **Дії** (Actions) — operations available for the studio.

**Studio actions:**

- **Оплатити** (Pay) — shown when the studio needs payment (mark «Не оплачено», Not paid); opens the payment window (see 4).
- **Деталі підписки** (Subscription details) — opens the subscription window (see 3).
- **Докупити SMS** (Buy more SMS) — opens the **Керування SMS** (SMS management) window (see 4.1).
- **Запросити зміну** (Request a change) — a plan change request; sent to the administrator for approval.
- **Реактивувати** (Reactivate) — for a frozen or deactivated studio; requires choosing a plan.
- **Передати** (Transfer) — a request to transfer the studio to another owner by email (**Email нового власника**, New owner's email); the administrator confirms the transfer.
- **Видалити** (Delete) — for a studio with a paid plan, deletion is scheduled: the studio works until the end of the paid period, money is not refunded, cancellation — with the **Відмінити видалення** (Cancel deletion) button. A studio without an active plan is deleted permanently after confirmation; the database is sent to the owner by email.

**Buttons at the top:**

- **Створити групу** (Create group) — combine several studios into a network (see 7).
- **Запланувати консультацію** — book a consultation with a manager.
- **Новий тенант** (New tenant) — create a studio with the wizard (see 5).
- **Видалити акаунт** (Delete account) — delete the account with all studios. Available only if no studio has an active plan; the account is deactivated for 3 months.

While a studio is awaiting administrator approval, a new studio cannot be created and the plan of existing studios cannot be changed.

---

## 3. Subscription details

The **Деталі підписки** window has tabs:

- **Деталі** (Details) — **План**, **Оплачено до** (Paid until), **Статус**, switch **Автопродовження (регулярний платіж)** (Auto-renewal (recurring payment)). If no card is saved (payment by IBAN transfer), there is no automatic charge; the card is saved at the next card payment while the switch is on.
- **Транзакції** (Transactions) — the studio's payments with the statuses **Очікує** (Pending), **Успішно** (Success), **Помилка** (Error).

The **Скасувати підписку** (Cancel subscription) button, after confirmation («Підтверджую скасування», I confirm the cancellation), turns off auto-renewal and deletes the saved card; the studio works until the end of the paid period, after which the subscription stops. Data is not deleted; the subscription is restored with the **Відновити підписку** (Resume subscription) button or by payment.

The studio card (by name in the table) contains: **Назва**, **Продукт**, **Статус**, **Домен / SSL** (Domain / SSL), **Google-вхід** (Google sign-in), **План**, **Діє до**, **Налаштування** (Setup), **Створено** (Created).

---

## 4. Paying for the plan

The **Оплата плану** (Plan payment) window opens with the **Оплатити** button. It shows the plan and the price per month (for an annual tariff — per year, with the saving compared with monthly payment; an annual tariff lasts 12 months) and the number of SMS included in the plan.

Payment methods:

- **Plata by mono** — card payment at once, the receipt is sent by email;
- **Переказ на IBAN** (IBAN transfer) — the **Отримати рахунок** (Get invoice) button creates an invoice; the receipt is issued after the money arrives.

The **Регулярний платіж (автопродовження)** (Recurring payment (auto-renewal)) switch turns on automatic charging every period. The **Оплатити — <amount> ₴** button goes to payment.

### 4.1 SMS management

The **Керування SMS** window shows **Норма SMS / місяць** (SMS allowance / month), **Доступно цей період** (Available this period) and **На рахунку** (On account). The **Докупити SMS** button buys extra SMS: they go to the venue's account, do not expire at the end of the period, are kept when the plan changes and are used after the monthly allowance. Buying is available after online payment (acquiring) is connected; otherwise extra SMS are added by the manager.

---

## 5. Creating a new studio

The **Новий тенант** button opens the **Новий тенант** wizard; «Крок N з M» (Step N of M) is shown above the steps. Steps: plan, project name, questionnaire (only if there are unanswered questions for the venue's line of business), setup, confirmation.

### 5.1 Plan

Choosing the plan. Each plan shows the price and limits. For a trial plan the limits are those of the permanent plan chosen after the trial period.

### 5.2 Project name

The project (studio) name; availability is checked at once («✓ Доступно», Available / «Недоступно: <reason>», Unavailable).

> Name: **4–24 characters**, Latin letters, digits and hyphens only. **The name cannot be changed later.**

If the account contact details are not filled in yet, this step asks for **Імʼя** (Name), **Телефон** (Phone), **Назва закладу** (Venue name), **Місто** (City) and **Країна** (Country); you cannot proceed without them. The name becomes the administrator's name in the app. Contact details are changed later in the **Акаунт** (Account) → **Контактні дані** (Contact details) window.

### 5.3 Questionnaire

The step is shown if there are unanswered questionnaire questions for the venue's line of business. The questionnaire is filled in once per line of business.

### 5.4 Setup

How the studio will be set up:

- **Налаштую самостійно** (I will set it up myself) — setup by the documentation (see [Initial Setup](/en/pages/setup)).
- **Потрібна допомога** (Help needed) — a manager contacts the owner.

### 5.5 Confirmation

Summary (**План**, **Назва**, **Налаштування**), **Період оплати** (Billing period, if the plan has an annual tariff), **SMS-нагадувань на місяць** (SMS reminders per month) and **До сплати при першій оплаті** (Due at the first payment). For a trial plan — the optional **План після пробного періоду** (Plan after the trial period); if it is not chosen, the administrator assigns the plan when approving the request.

Optional data transfer options:

- **Скопіювати з іншого тенанта** (Copy from another tenant) — transfers reference lists and settings from an existing studio. Users, staff and working data **are not transferred**.
- **Відновлення з резервної копії** (Restore from a backup) — upload a saved encrypted dump (`.enc`); the database is restored when the studio is created.

The **Умови використання** (Terms of use) must be accepted («Я приймаю Умови використання», I accept the Terms of use). The **Надіслати заявку** (Submit request) button submits the request; the result is «Заявку прийнято» (Request accepted). If the studio needs approval, it appears after the administrator approves it.

---

## 6. Plans

The **Плани** (Plans) tab (title «Плани, що ростуть разом з вами», Plans that grow with you) shows the available tariffs. The current plan is marked **Поточний** (Current).

### 6.1 Regular plans

Plans for a single studio. Each shows the price in UAH (with an approximate USD equivalent) and the limits. The **Вибрати** (Select) button offers **Створити новий тенант** (Create a new tenant) with this plan or **Замінити план існуючому тенанту** (Replace the plan of an existing tenant) (the change requires administrator approval).

### 6.2 Enterprise

**Enterprise** plans are for a **network** (group) of studios: the price is calculated for the actual number of studios («Ціна за фактичну кількість тенантів», Price for the actual number of studios). The minimum number of studios is set in the plan («Мінімум тенантів: N», Minimum studios: N). The plans are assigned to a group (see 7).

---

## 7. Groups (studio network)

Several studios are combined into a **group (network)** with shared limits and shared data.

### 7.1 Creating a group

The **Створити групу** button opens the **Нова група** (New group) window with the **Назва групи** (Group name) and **Корпоративний план** (Corporate plan) fields. The button is shown when there are at least **2** studios outside groups and at least one Enterprise plan is available.

After creation the group is **inactive** («Неактивна — додайте щонайменше 2 тенанти.», Inactive — add at least 2 tenants). While the number of tenants is below the plan minimum, «Додайте ще N тенант(ів), щоб перейти до оплати.» (Add N more tenant(s) to proceed to payment) is shown. Once the minimum is reached, the group starts working after payment with the **Оплатити план групи** (Pay the group plan) button; until then each venue works on its own plan.

### 7.2 Adding studios and an Enterprise plan

The **Додати в групу** (Add to group) button adds a studio to the group. If the studio has a paid plan, it stays in effect until the end of the period, after which the studio moves to the group plan. The Enterprise plan turns on shared limits for the whole group; group settings are available right after the plan is assigned. The **Вилучити з групи** (Remove from group) button returns the studio to its own plan.

### 7.3 Active group and shared data

When the group is active, group features are available:

- **Спільна база клієнтів** (Shared client base) — one client card and one shared bonus balance for the whole network.
- **Абонементи спільні на мережу** (Memberships shared across the network) — one session counter: purchased sessions can be used in any venue of the network.
- Synchronization (copying from the main venue) of reference lists: **Категорії занять** (Session categories), **Абонементи** (Memberships), **Тренери (без розкладу)** (Coaches, without schedule), **Зали** (Rooms), **Клієнти з номерами карток** (Clients with card numbers).

One venue is marked **Головний** (Main) — data is copied from it to the other venues. Switch changes are applied with the **Застосувати зміни** (Apply changes) button; the synchronization result is shown in the **Синхронізація групи** (Group synchronization) window.

> Coaches are transferred **without schedule**: each studio's schedule is made separately.

The **Видалити групу** (Delete group) button closes the group: the venues move to a regular plan and work on it until the end of the group's paid period.

---

## 8. Support

The **Підтримка** (Support) tab — requests to the support service. The **Новий тікет** (New ticket) button creates a request (**Заклад** (Venue), **Тема** (Subject), **Повідомлення** (Message), priority **Звичайний** (Normal) / **SOS**). The list shows **Тема**, **Статус** (**Відкрито** (Open), **Очікує вас** (Awaiting you), **Вирішено** (Resolved), **Закрито** (Closed)), **SOS** and **Оновлено** (Updated). The monthly request balance is shown («Залишок: N з M на місяць», Remaining: N of M per month, or «Тікети: без ліміту», Requests: no limit). Details — [Support system](/en/pages/support-system).

---

## 9. Top bar

The cabinet top bar always contains:

- **Сайт** (Site) — the product website.
- **Документація** (Documentation) — this documentation.
- **Умови використання** (Terms of use) — the public agreement.
- Language switch (UA / EN).
- **Сповіщення** (Notifications) — a bell with the unread counter; **Прочитати всі** (Read all).
- **Акаунт** (Account) — the role and the **Контактні дані** (Contact details) tab (phone with the country code, for example `+380XXXXXXXXX`).
- **Вийти** (Sign out) — signing out of the cabinet.

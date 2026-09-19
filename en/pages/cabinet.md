# Owner Cabinet (subscription management)

Besides the working admin panel, you have an **owner cabinet** at **clients.fitshandler.com**. It is a separate owner area where you manage your **tenants** (studios), **subscription and payments**, **plans**, **groups (studio networks)** and contact **support**.

One cabinet account can hold **several tenants** — for example, a few studios or separate projects. Each tenant is its own working database with its own admin panel.

---

## 1. Signing in

Sign in with a **Google account**. Press "Sign in with Google" and pick your account.

> The cabinet is tied to your Google email: all your tenants live under that login.

---

## 2. My tenants

The main tab is **"My tenants"**. It lists all your tenants with their plan, due date and status.

If you have no tenants yet, the cabinet shows where to start instead of an empty list: press **"New tenant"**, and if you have questions — **"Schedule a consultation"**.

**Table columns:**

- **Name** — the tenant name (click it to open the card — see 3).
- **Product** — the product (fitstudiocrm).
- **Plan** — the current plan and its price.
- **Due date** — the date the subscription is paid up to.
- **Status** — "Active" while the tenant is running.
- **Actions** — operations available for the tenant.

**Tenant actions:**

- **Pay** — appears when there is an unpaid balance (the "Not paid" badge); opens the payment dialog (see 4).
- **Subscription details** — opens the tenant card (see 3).
- **SMS** — view or top up the tenant's SMS quota.
- **Transfer** — hand the tenant over to another owner.
- **Delete** — delete the tenant.

**Buttons at the top:**

- **Create group** — join several studios into a network (see 7).
- **Schedule a consultation** — book a call with our manager.
- **New tenant** — create a tenant with the wizard (see 5).
- **Delete account** — delete the whole cabinet account.

---

## 3. Tenant card

The card shows everything about the tenant: product, status, the admin panel address (**URL**), technical identifiers (**App ID**, **DB name**), the current plan, the due date, the setup choice and the creation date.

---

## 4. Paying for a plan

The payment dialog opens with the **"Pay"** button. It shows the plan, its monthly price in UAH, and the **number of SMS reminders** per month (a base amount is included in the plan; you can raise it — the extra is charged at the plan's rate).

The **"Recurring payment (auto-renew)"** switch turns on monthly automatic charging so the subscription never lapses.

---

## 5. Creating a tenant

**"New tenant"** opens a **four-step** wizard.

### 5.1 Step 1 — pick a plan

Pick the plan for the new tenant. Each plan lists its limits: users, staff, memberships, services, trainers, gyms, support tickets, SMS reminders.

### 5.2 Step 2 — project name

Enter the project (tenant) name. Availability is checked as you type.

> Name: **4–24 characters**, Latin letters, digits and hyphens only. **It cannot be changed later** — it is a technical identifier.

### 5.3 Step 3 — setup

Choose how you will set the tenant up:

- **I will do it myself** — you follow the documentation (see [First setup](/en/pages/setup)).
- **I need help** — a manager will contact you.

### 5.4 Step 4 — confirmation

The last step shows the summary (plan, name, setup choice), lets you set the **number of SMS reminders** and shows the **amount of the first payment**.

Two optional data-transfer options live here as well:

- **Copy from another tenant** — bring reference data and settings over from a studio you already have. Users, staff and working data are **not** copied.
- **Restore from a backup** — if you were our client before, upload the encrypted dump (`.enc`) and we restore your database while creating the tenant.

Press **"Send request"** to create the tenant.

---

## 6. Plans

The **"Plans"** tab lists the available plans. Your current plan carries the **"Current"** badge.

### 6.1 Regular plans

Plans for a single studio. Each shows the price in UAH (with an approximate USD equivalent) and the limits: users, staff, memberships, services, trainers, gyms, support tickets, SMS reminders.

### 6.2 Enterprise

**Enterprise** plans are for a **network** (group) of studios: the price is counted **per actual tenant**. The minimum number of studios is set on the plan itself (usually 2) and is shown on the plan card. They are activated for a group (see 7).

---

## 7. Groups (studio network)

Several studios can be joined into a **group (network)** with shared limits and shared data.

### 7.1 Creating a group

**"Create group"** opens a dialog where you name the network. It appears once you have at least **2** studios outside any group and at least one Enterprise plan is available.

A new group starts **inactive** — it needs as many studios as the chosen Enterprise plan requires (usually 2). With fewer, it stays inactive and the cabinet says how many are missing.

### 7.2 Adding tenants and an Enterprise plan

Add studios to the group and assign it an **Enterprise plan**. The Enterprise plan turns on shared limits for the whole group; group settings become available as soon as the plan is assigned.

### 7.3 An active group and shared data

An active group offers:

- **Shared client base** — one client record and one bonus balance across the network.
- **Shared memberships** — a purchased membership works in every studio of the network.
- **Sync from the main studio** — copy reference data between studios: class categories, memberships, trainers (without schedules), gyms, clients with card numbers.

One studio is marked as the **Main** one — the sync runs from it. After changing the switches press **"Apply changes"**.

> Trainers are copied **without their schedules**: the schedule is specific to each studio and has to be built there.

---

## 8. Support

The **"Support"** tab is where you reach our support service. **"New ticket"** creates a request; the list shows the subject, status, the **SOS** mark (urgent) and the update date. More in [Support System](/en/pages/support-system).

---

## 9. Top bar

The cabinet's top bar always offers:

- **Product site** — the Fitshandler mark links to fitshandler.com.
- **Documentation** — this guide.
- **Terms of Use** — the public offer.
- **Language switch** (UA / EN).
- **Notifications** — a bell with the unread counter.
- **Sign out**.

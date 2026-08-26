[Back to home](/en/)

# 4. Initial Setup

> Tips for the initial setup of the system

---

## 4.1 Add and Configure Administrators

> To add all administrators, each of them must complete their first login to the system.  
> After that, the **Super Admin** configures roles, base rate, phone number, and so on for each administrator.

---

## 4.2 Add Categories

> Add and configure categories.  
> Categories can also be added or edited later.  
> It is recommended to first create the base categories that will be used when creating workouts.

---

## 4.3 Add Plans

> Add the base plans.  
> Plans can also be created later, and existing ones can be edited.

---

## 4.4 Add Rooms

> Create and configure rooms.  
> The room color is used in the calendar if a workout has no coach (rental), or if the coach has no color selected.

---

## 4.5 Add Coaches

> Add and configure coaches.  
> They can also be added and edited later.

---

## 4.6 Add Workouts

> Add and configure workouts.

---

## 4.7 Add Clients

> Add clients.

### 4.7.1 Configuring Client Plans

> When switching to the new system, many clients may have active plans with a different number of remaining workouts.  
> For each client, a separate plan needs to be created based on the remaining balance.  
> Such plans are sold to clients at a price of **0**, since they have already been paid for previously.  
> After the sale, these plans can be deleted from the system.  
> Book the clients into the workouts they were previously registered for.

---

### 4.7.2 Importing Clients from an Excel File

> The import option is available in the **Admin Panel** menu, on a separate **Import** tab, next to the [Settings](/en/login/settings) tab.

![](../../_media/admin-panel-settings-prro.png ':size=150x86')

**Required fields for import:**

- Name
- Phone number
- Email
- Card
- Date of birth

> The file must contain at least one of these fields, otherwise the system will show an error message.

![](../../_media/import-error.png ':size=150x73')

Other fields can be mapped manually.  
An example test Excel file has been prepared:

![](../../_media/import-simple-xls.png ':size=200x58')

**The file contains:**

- Name
- Last name
- Phone number
- Email
- Card
- Date

> All fields match the required ones except the **Date** field. There is also an extra field, **Last name**.

After the file is uploaded, a mapping step appears:

![](../../_media/import-mapping-step.png ':size=150x89')

- The system ignores extra and unrecognized fields if no mapping is performed.  
- To do this, click **Add Field Mapping**:

![](../../_media/import-mapping-step-1.png ':size=200x45')

- **Field** — list of unmatched fields
- **Mapping** — list of fields available in the system
- **Prefix** — arbitrary text (for example, a space to join the first and last name)

**Example:**  
The **Last name** field needs to be combined with the **Name** field, adding a space as the prefix.  
The **Date** field is mapped as **Date of birth** (without a prefix).

![](../../_media/import-mapping-step-2.png ':size=200x56')

![](../../_media/import-mapping-step-3.png ':size=200x46')

After that, an import preview will be shown:

![](../../_media/import-preview-step.png ':size=200x68')

If you click **Continue** — the import will finish with a message:

![](../../_media/import-success.png ':size=200x47')

> After the import, all clients will appear in the table on the **Clients** page.

---

## 4.8 Getting Ready to Operate

> Go to the admin panel and open the [Mobile Application](/en/login/settings#mobile-application) tab.
> Download the QR code or the ready-made banner and print it.
> Place the QR code in the studio, at the reception desk, in the changing rooms. By scanning the code, clients
> will install the PWA app and will be able to book workouts themselves, view
> their plans, receive push notifications about coach substitutions, and more.

---

[Back to home](/en/)

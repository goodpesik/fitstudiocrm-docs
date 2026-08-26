<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 3.3 Workouts

> The **Workouts** page

![](../../_media/workouts-page.png ':size=200x121')

---

## 3.3.1 Create a workout

> Clicking the **Create workout** button opens a modal window with a form:

![](../../_media/add-workout-1.png ':size=200x121')

**Fields:**

- **Name**
- **Personal** ("Персональне") toggle — sets the type to "Personal"
- **Recurring** ("Регулярне") toggle — determines whether the workout repeats
- **Date** (for a one-time workout)
- **Start** — the workout's start time

> To create a workout, you must fill in the name and choose a type.  
> For a one-time workout, the date and time are required.

![](../../_media/add-workout-2.png ':size=200x121')

> For a recurring workout, the day(s) and time are required.

![](../../_media/add-workout-3.png ':size=200x121')

> After the date and time are added, or the days are chosen, additional fields appear:

![](../../_media/add-workout-4.png ':size=100x100')

- **Workout duration (min)**
- **Coach**
- **Room**
- **Maximum number of people**
- **Category** — chosen from a list (created under [Settings → Categories](/en/login/settings#categories))

> If the workout conflicts with another one, a message appears at the bottom of the form.  
> In that case, the coaches and rooms with conflicts are excluded from the lists.

**Example:**  
The studio has 3 rooms (**Room 1**, **Room 2**, **Room 3**) and 3 coaches (**Coach 1**, **Coach 2**, **Coach 3**).  
**Coach 1** has a workout on Tuesday at 12:00 in **Room 2**.  
When creating another workout for the same time, a conflict message is shown.  
Only **Coach 2**, **Coach 3**, **Room 1**, and **Room 3** remain available.

---

![](../../_media/add-workout-5.png ':size=100x106')

> For a recurring workout, the **Add exception** field is available — it lets you set dates on which the workout will not take place.

> Next to it is the **Repeat workout until:** → **Choose date** toggle. When it is turned on, a date picker opens — the chosen date becomes the **last day** of the recurrence. After that date, no further occurrence of the workout is created in the calendar. Useful for term-based courses or temporary series. Turning the toggle off clears the field and returns the workout to an indefinite repeat.

---

![](../../_media/add-workout-6.png ':size=100x103')

> For a personal workout, additional fields are available:

- **Client** — the client who will automatically be booked for the workout
- **Plan** — the plan that will be used to pay for the workout at registration

---

## 3.3.2 Renting a room

![](../../_media/rent.png ':size=100x60')

> The form is similar to creating a workout, but has fewer fields.  
> A client and a plan for payment must be chosen.

---

## 3.3.3 Filters

> The page has the following filters:

- All
- Upcoming
- Past
- Group
- Personal
- Rental
- By coach

---

## 3.3.4 Search

> Search is available by workout name.

---

## 3.3.5 Workouts table

> The table contains:

- **Name**
- **Coach**
- **Duration**
- **Room**
- **Day**
- **Time**
- **Type**
- **Category**
- **Actions**:
  - *Delete* (available for deactivated workouts)
  - *Edit*

**Sorting is available by:**

- Name
- Coach
- Room
- Day
- Category

---

## 3.3.6 Editing

> Editing offers the same fields as creating, with some restrictions.

![](../../_media/edit-workout-1.png ':size=100x60')

**Fields locked from editing on the edit form:**

- The **Personal** and **Recurring** toggles (the workout type is fixed).
- The **Client** field (for personal workouts — changed via cancel → rebook, not by editing the template).
- The **Date** field (for one-time workouts — use the separate flow on [Schedule → gear icon → Change workout time](/en/menu/schedule#settings-button)).

**Fields that can be changed:**

- Name, duration, coach, room, max count, category, schedule (for recurring workouts — days / time / "Repeat until" / exceptions).

![](../../_media/edit-workout-change.png ':size=100x50')

> If the day or time is changed, a warning appears on save.

---

## 3.3.7 Deletion

> A workout can only be deleted after it has been deactivated.  
> Deactivation is not possible if the workout takes place today or has attendees.

![](../../_media/edit-workout-2.png ':size=100x37')

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

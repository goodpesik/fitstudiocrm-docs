<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

# 7.9 Ratings and Reviews

> Clients rate attended classes in the app or by a link from a message. The ratings make up the studio rating and the rating of each coach.

---

## Rating a Class

**In the app.** A client whose class is marked as **Attended** sees the **«Rate your last class»** offer with the class name and date on [Home](/en/mobile/home). The offer is shown if **«Пропонувати оцінити заняття»** (Offer to rate the session) is on in the [Settings → Mobile Application](/en/login/settings#ratings-and-reviews) tab.

The **«Rate the class»** window: the class date, the coach, a rating from 1 to 5 stars (required), the field «Your feedback (optional)», the **«Submit»** and **«Not now»** buttons.

- After submitting — «Thanks for your feedback!»; error — «Could not save your review».
- **«Not now»** closes the offer; the client is not asked about this class again.
- If there is no class to rate — «No class to rate».

**By a link from a message.** If **«Пропонувати оцінити заняття в смс (для клієнтів без застосунку)»** (Offer to rate the session by SMS (for clients without the app)) is on, a client without the app receives a message with a rating link after the class (channels — [Messages to clients](/en/pages/processing#_614-messages-to-clients)). The link opens the **«Rate the class»** page without login. The message is sent for classes attended within the last 2 days; the link is valid for 14 days.

| Link state | What is shown |
|---|---|
| The class has already been rated | «Thank you, you have already rated this class» — «A second rating is not needed.» |
| The link has expired | «The link no longer works» — «A rating request lives for a limited time. You can rate the class in the app — the prompt appears there by itself.» |

---

## Rating Visibility

| Rating | Shown |
|---|---|
| Studio rating | after **5 ratings** |
| Coach rating | from the **first rating** |

- The average is calculated from all ratings.
- The public review list contains up to 10 newest reviews rated 4 or higher.
- Until a rating is shown, there are no stars or numbers under the coach avatar or in the studio header.
- If **«Показувати рейтинг клієнтам»** (Show the rating to clients) is off in the [Settings → Mobile Application](/en/login/settings#ratings-and-reviews) tab, clients and visitors of the public page do not see the rating and reviews; ratings are collected and shown in the studio reports.

---

## Who Sees What

| Role | What is available |
|---|---|
| **Client**, public page visitor | Studio rating and reviews — the **«About us»** button and the star in the studio header; coach rating — under the coach avatar on the workout card |
| **Coach** | The **Ratings** tab: own average rating, the number of ratings («reviews: {N}») and reviews about themselves; the average rating is also shown next to the «Upcoming workouts» heading on Home |
| **Administrator** | The **Ratings** tab: all studio coaches with the average rating and the number of ratings; tapping a coach opens the reviews about them |

- A coach sees only reviews about themselves.
- A coach without ratings is shown in the administrator's list with a dash «—» instead of a number.
- Empty states: «No reviews yet», «This studio has no coaches yet»; error — «Could not load the ratings. Please try again later».

---

## Ratings in the Admin Panel

The studio rating, the rating of each coach and the review list are in [Reports → Rating](/en/menu/reports#_386-rating). The **Супер Адмін** (Super Admin) and **Адмін** (Admin) roles can delete a review.

---

<a href="javascript:void(0)" onclick="history.back()">⬅️ Back</a>

[Back to home](/en/)

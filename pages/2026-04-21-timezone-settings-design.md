# Timezone Settings — Design

**Date:** 2026-04-21

## Overview

Admin staff opening the schedule from a different timezone (e.g., Poland) sees incorrect workout times because the frontend parses UTC dates through the browser's local timezone. Workouts and WorkoutOccurrences already store `localTimeHours` and `localTimeMinutes` — studio wall-clock time set at creation. The fix is to use these fields for all time display instead of parsing UTC through `Date.getHours()`, and to store the studio's IANA timezone in Settings so it can be used wherever a real "now vs. event" comparison is needed.

No changes to how `localTimeHours`/`localTimeMinutes` are stored — that logic is already correct.

---

## Affected Repositories

| Repo | Change |
|---|---|
| `fitstudiocrm-server` | Add `timezone` field to `Settings` entity + DTO + migration |
| `fitstudiocrm-app` | Timezone selector in UI; load timezone into store; fix display helpers; fix `isPassMinEventCancelTime` |
| `fitstudiocrm-mobile-server` | Add `GET /settings/timezone` endpoint (TCP proxy to main server) |
| `fitstudiocrm-mobile` | Load timezone from API into store; pass to `dates.helper.ts`; fix `workouts.helper.ts` display |

---

## Backend — fitstudiocrm-server

### Settings Entity

Add one column to `Settings`:

```typescript
@Column({ nullable: true, default: 'Europe/Kyiv' })
timezone: string;
```

- Type: `string` (IANA timezone identifier, e.g. `"Europe/Kyiv"`, `"Europe/Warsaw"`)
- Nullable with default `"Europe/Kyiv"` — existing studios get Kyiv automatically
- Included in `SettingsDTO` for both PATCH (input) and GET (response)

### Migration

Standard TypeORM `ALTER TABLE settings ADD COLUMN timezone varchar DEFAULT 'Europe/Kyiv'`.

### No other backend changes

The server already writes `localTimeHours`/`localTimeMinutes` from the frontend payload when creating Workout and WorkoutOccurrence records. This remains unchanged.

---

## Admin App — fitstudiocrm-app

### ISettingsModel

Add `timezone?: string` to the existing `ISettingsModel` interface.

### Timezone selector (admin-panel.vue — Налаштування tab)

PrimeVue `Select` with a fixed curated list of IANA timezone strings. The list includes European and other relevant timezones. **Russian and Belarusian timezones are explicitly excluded.**

Allowed timezone identifiers (representative list):
```
Europe/Kyiv, Europe/Warsaw, Europe/Berlin, Europe/Prague, Europe/Vienna,
Europe/Budapest, Europe/Bratislava, Europe/Bucharest, Europe/Sofia,
Europe/Helsinki, Europe/Tallinn, Europe/Riga, Europe/Vilnius,
Europe/Stockholm, Europe/Oslo, Europe/Copenhagen, Europe/Amsterdam,
Europe/Brussels, Europe/Paris, Europe/Madrid, Europe/Rome,
Europe/Zurich, Europe/Lisbon, Europe/London, Europe/Athens,
Europe/Istanbul, UTC
```

Each option displays a human-readable label alongside the identifier (e.g., "Київ (UTC+2/+3)"). Saved via the existing `onSaveGeneralSettings` handler. Added to the general settings payload.

### Settings Pinia store

A lightweight `settings` store (or extend the existing `user` store) loads `GET settings` once at app startup and exposes `timezone: string` (default `"Europe/Kyiv"` if API returns null/undefined). All helpers that need timezone read from this store.

### getDateTimeForEvent (workouts.helper.ts)

`getDateTimeForEvent` currently calls `new Date(workout.time).getHours()` and `.getMinutes()` — browser-timezone-dependent.

**Fix:** If `workout.localTimeHours` and `workout.localTimeMinutes` are present, use them directly. Fallback to `getHours()`/`getMinutes()` for records that predate the migration.

```typescript
const eventTimeH = workout.localTimeHours ?? new Date(time).getHours();
const eventTimeM = workout.localTimeMinutes ?? new Date(time).getMinutes();
```

**Conflict checking is not affected** — the conflict logic operates on millisecond timestamps normalized through `normalizeToReference`. Both sides of every comparison go through the same normalization, so relative ordering remains correct. No changes to `getConflictingWorkouts` or `normalizeToReference`.

### isPassMinEventCancelTime (date.helpers.ts)

Currently compares `eventH` (from `new Date(eventTime).getHours()`) to `now.getHours()` — both browser-local, consistently wrong in the same direction.

**Fix:** Add optional `studioTimezone?: string` parameter. When provided, use Luxon to get the current hour in the studio timezone:

```typescript
const nowH = studioTimezone
  ? DateTime.now().setZone(studioTimezone).hour
  : now.getHours();
const nowM = studioTimezone
  ? DateTime.now().setZone(studioTimezone).minute
  : now.getMinutes();
```

`eventH` / `eventM` come from `localTimeHours`/`localTimeMinutes` (studio wall-clock) when available. This makes the comparison correct across DST transitions: both sides are in the same studio-local timezone.

**DST edge case:** `localTimeHours` is always studio wall-clock time (e.g., 10 = "10:00" regardless of season). Luxon's `.hour` on the studio timezone also returns the wall-clock hour accounting for DST. So the comparison is always apples-to-apples.

### Luxon dependency

Luxon is already used in `fitstudiocrm-mobile`. Check if it is present in `fitstudiocrm-app`; add it if not.

---

## Mobile Server — fitstudiocrm-mobile-server

### GET /settings/timezone

New endpoint returning `{ timezone: string }`. Retrieves settings from the main server via the existing TCP microservice connection and returns only the `timezone` field.

This is the minimal surface — the mobile app does not need the full settings object.

---

## Mobile App — fitstudiocrm-mobile

### Timezone store

Load `GET /settings/timezone` once at app startup. Store result in Pinia. Expose `timezone: string` (default `"Europe/Kyiv"`).

### dates.helper.ts

`formatDate`, `getLocalDate`, `getLocalTime` each hardcode `"Europe/Kyiv"`. Add optional `timezone?: string` parameter with default `"Europe/Kyiv"`:

```typescript
export function formatDate(
  dateStr: Date | string,
  options: "date" | "time" | "dateLong" | "dateTime" = "date",
  timezone: string = "Europe/Kyiv",
): string {
  const dt = /* ... */.setZone(timezone);
  // ...
}
```

Call sites pass `settingsStore.timezone` where the displayed time must match studio timezone.

### workouts.helper.ts

Lines 56–57 use `new Date(workout.time).getHours()` / `.getMinutes()`. Replace with:

```typescript
const eventH = workout.localTimeHours ?? new Date(workout.time).getHours();
const eventM = workout.localTimeMinutes ?? new Date(workout.time).getMinutes();
```

Fallback keeps backwards compatibility with any records missing the local time fields.

---

## Save Behavior

Timezone is saved in the Налаштування tab via the existing `onSaveGeneralSettings` PATCH call — no new endpoint or handler needed.

---

## Testing — Edge Cases

All edge cases must be covered by unit tests.

### fitstudiocrm-app: date.helpers.ts

| Case | Expected |
|---|---|
| `isPassMinEventCancelTime` — event in 2h, studio timezone provided, browser in Poland | Returns true (not past cancel time) |
| `isPassMinEventCancelTime` — event 1h ago, studio timezone provided | Returns false |
| `isPassMinEventCancelTime` — no timezone provided (fallback) | Behaves as before (existing tests pass) |
| `isPassMinEventCancelTime` — event at 01:30 on DST spring-forward night | Handled correctly (Luxon normalizes ambiguous times) |
| `isPassMinEventCancelTime` — `maxEventCancelTimeHour = 0` | Returns true unconditionally |

### fitstudiocrm-app: workouts.helper.ts

| Case | Expected |
|---|---|
| `getDateTimeForEvent` — workout has `localTimeHours`/`localTimeMinutes` | Uses local fields, ignores `workout.time` hours |
| `getDateTimeForEvent` — workout missing `localTimeHours` (old record) | Falls back to `new Date(workout.time).getHours()` |
| Conflict check — two workouts at same local time same day | Conflict detected |
| Conflict check — two workouts at different local times same day | No conflict |
| Conflict check — workout with `localTimeHours` vs workout without | Still detects overlap correctly |

### fitstudiocrm-app: admin-panel.vue

| Case | Expected |
|---|---|
| Timezone selector renders with allowed list | No Russian/Belarusian timezones in options |
| `onSaveGeneralSettings` includes `timezone` in PATCH payload | Correct |
| `onSaveGeneralSettings` with `timezone = null` | Sends null (cleared by admin) |

### fitstudiocrm-mobile: dates.helper.ts

| Case | Expected |
|---|---|
| `formatDate(utcDate, "time", "Europe/Kyiv")` | Returns Kyiv wall-clock time |
| `formatDate(utcDate, "time", "Europe/Warsaw")` | Returns Warsaw wall-clock time (1h behind Kyiv in winter) |
| `formatDate(utcDate, "time")` (no timezone arg) | Defaults to "Europe/Kyiv" |
| `formatDate(utcDate, "date", "Europe/Warsaw")` | Date does not shift for midday UTC events |
| Date near midnight UTC — `formatDate` with Kyiv timezone | Returns correct Kyiv date (not UTC date) |

### fitstudiocrm-mobile: workouts.helper.ts

| Case | Expected |
|---|---|
| Workout with `localTimeHours=10`, `localTimeMinutes=30` | `eventH=10`, `eventM=30` regardless of browser timezone |
| Workout missing `localTimeHours` (old record) | Falls back to `new Date(workout.time).getHours()` |

---

## Backend

No changes to `Settings` API shape beyond the new `timezone` field. No migrations to WorkoutOccurrence or Workout tables. No changes to occurrence creation logic.

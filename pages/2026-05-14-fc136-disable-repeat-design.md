# FC-136: Disable Repeating Workouts Automatically

## Goal

When a client misses a repeated workout a total of X times (across all time), automatically remove the repeat flag from their booking so they stop being auto-added to future occurrences. X is configurable per studio via a new setting in the "Functions" section.

## Actions

1. After each daily batch run, if a client is marked `Unvisited` and the setting is enabled, count their total `Unvisited` occurrences for that specific workout (`workoutId`)
2. If the count reaches the threshold X, set `isRepeat: false` on the client's entry in the next unprocessed future occurrence of that workout
3. Create a studio-wide admin notification about the automatic disabling

## Architecture

### Settings Entity — new field

New nullable integer column in the `Settings` entity:

```
autoDisableRepeatAfterMisses: number | null
```

- `null` — feature disabled (default)
- any positive integer — threshold X

Requires a TypeORM migration.

### Backend — daily scheduler logic

**File:** `fitstudiocrm-server/src/tasks/tasks.service.ts`

After marking a client as `ClientWorkoutStatus.Unvisited` during `workoutsAndVisitsJob`, if `settings.autoDisableRepeatAfterMisses` is not null:

1. Call `workoutOccurrenceService.disableRepeatIfExceededMisses(clientId, workoutId, threshold, dataSource)`
2. The method counts occurrences where `processed: true`, client status = `Unvisited`, for the given `(clientId, workoutId)` pair
3. If count >= threshold:
   - Find the earliest future occurrence (`processed: false`) of this `workoutId` where the client entry has `isRepeat: true`
   - Set `isRepeat: false` on that client entry and save
   - Create a `Notifications` record: `"Клієнт [name] автоматично знятий з повторного запису: [workout name] (пропущено N разів)"`

**Helper method signature:**

```typescript
async disableRepeatIfExceededMisses(
  clientId: string,
  workoutId: string,
  threshold: number,
  dataSource: DataSource,
): Promise<void>
```

Located in `workout-occurrence.service.ts` — the method only affects one client entry in one occurrence, keeps the change atomic.

### Notification format

```
Клієнт [ім'я клієнта] автоматично знятий з повторного запису: [назва тренування] (пропущено [N] разів)
```

Created in the `Notifications` table following the same pattern as other automated scheduler notifications (studio-wide, same mechanism as birthday/plan expiry reminders).

### Frontend — Settings UI

**File:** `fitstudiocrm-app/src/pages/settings.vue` (Functions section)

New number input field in the "Функції" tab:

- Label: `"Автоматично знімати повторний запис після ___ пропусків"`
- Type: `number`, min: 1
- Empty or 0 → stored as `null` (feature disabled)
- Saved via `PATCH /settings` along with other settings fields

## File Map

| Action | File | Responsibility |
|---|---|---|
| Modify | `fitstudiocrm-server/src/settings/settings.entity.ts` | Add `autoDisableRepeatAfterMisses` column |
| Create | `fitstudiocrm-server/src/database/migrations/<timestamp>-AddAutoDisableRepeat.ts` | DB migration |
| Modify | `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.service.ts` | Add `disableRepeatIfExceededMisses()` helper |
| Modify | `fitstudiocrm-server/src/tasks/tasks.service.ts` | Call helper after Unvisited is set |
| Modify | `fitstudiocrm-app/src/pages/settings.vue` | Number input in Functions section |

## Out of Scope

- No per-workout or per-client override of the threshold
- No "re-enable" automation — admin re-enables manually if needed
- No notification to the client (only studio admin notification)
- No consecutive miss counting — only total Unvisited for that workout

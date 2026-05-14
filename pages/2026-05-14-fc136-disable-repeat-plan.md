# FC-136: Disable Repeating Workouts Automatically — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** When a client's total missed (Unvisited) count for a specific workout reaches the studio-configured threshold X, automatically set `isRepeat: false` on their entry in the next unprocessed future occurrence of that workout, stopping auto-enrollment going forward.

**Architecture:** A new `disableRepeatIfExceededMisses()` method on `WorkoutOccurrenceService` queries past processed occurrences via JSONB for the miss count, then patches the next future occurrence's clients array via raw SQL if the threshold is reached. `TasksService.workoutsAndVisitsJob` (which already fetches `settings`) calls this helper right after marking each client as `Unvisited`, then fires a studio-wide `Notifications` record if action was taken. A new nullable integer column `autoDisableRepeatAfterMisses` is added to the `Settings` entity. The admin frontend exposes a number input in the "Функції" tab of `admin-panel.vue`.

**Tech Stack:** NestJS, TypeORM (QueryBuilder + raw `manager.query`), PostgreSQL JSONB, TypeORM migration, Vue 3 + PrimeVue `InputNumber`.

---

## File Map

| Action | File | Responsibility |
|---|---|---|
| Modify | `fitstudiocrm-server/src/settings/settings.entity.ts` | Add `autoDisableRepeatAfterMisses` column |
| Create | `fitstudiocrm-server/src/database/migrations/AddAutoDisableRepeat1747180800000.ts` | DB migration |
| Modify | `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.service.ts` | Add `disableRepeatIfExceededMisses()` |
| Create | `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.disable-repeat.spec.ts` | Unit tests for the helper |
| Modify | `fitstudiocrm-server/src/tasks/tasks.service.ts` | Call helper + create notification after Unvisited |
| Modify | `fitstudiocrm-app/src/models/` (file containing `ISettingsModel`) | Add field to interface |
| Modify | `fitstudiocrm-app/src/components/admin-panel.vue` | InputNumber in Functions tab + save payload |

---

## Task 1: Settings entity + migration

**Files:**
- Modify: `fitstudiocrm-server/src/settings/settings.entity.ts`
- Create: `fitstudiocrm-server/src/database/migrations/AddAutoDisableRepeat1747180800000.ts`

- [ ] **Step 1: Add column to Settings entity**

In `fitstudiocrm-server/src/settings/settings.entity.ts`, add after the `remindAboutCoachBirthdays` field:

```typescript
@Column({ type: 'integer', nullable: true })
autoDisableRepeatAfterMisses: number | null;
```

- [ ] **Step 2: Create migration**

Create `fitstudiocrm-server/src/database/migrations/AddAutoDisableRepeat1747180800000.ts`:

```typescript
import { MigrationInterface, QueryRunner } from 'typeorm';

export class AddAutoDisableRepeat1747180800000 implements MigrationInterface {
  public async up(queryRunner: QueryRunner): Promise<void> {
    await queryRunner.query(
      `ALTER TABLE settings ADD COLUMN IF NOT EXISTS "autoDisableRepeatAfterMisses" INTEGER`,
    );
  }

  public async down(queryRunner: QueryRunner): Promise<void> {
    await queryRunner.query(
      `ALTER TABLE settings DROP COLUMN IF EXISTS "autoDisableRepeatAfterMisses"`,
    );
  }
}
```

- [ ] **Step 3: Run migration**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-server
npm run typeorm:run 2>&1 | tail -5
```

Expected: `Migration AddAutoDisableRepeat1747180800000 has been executed successfully.`

- [ ] **Step 4: Build to verify TypeScript**

```bash
npm run build 2>&1 | tail -5
```

Expected: no TypeScript errors.

- [ ] **Step 5: Commit**

```bash
git add src/settings/settings.entity.ts src/database/migrations/AddAutoDisableRepeat1747180800000.ts
git commit -m "FC-136 Add autoDisableRepeatAfterMisses column to Settings"
```

---

## Task 2: `disableRepeatIfExceededMisses` in WorkoutOccurrenceService

**Files:**
- Modify: `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.service.ts`
- Create: `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.disable-repeat.spec.ts`

**Background:** `WorkoutOccurrenceService` has `ConnectionService` injected as `this.connectionService`. The `clients` column on `workout_occurrence` is JSONB — each element is a `WorkoutOccurrenceClient` object with fields `id`, `status` (int), `isRepeat` (bool), etc. `ClientWorkoutStatus.Unvisited = 3`.

- [ ] **Step 1: Write the failing test**

Create `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.disable-repeat.spec.ts`:

```typescript
/* eslint-disable */
import { WorkoutOccurrenceService } from './workout-occurrence.service';

const mockGetCount = jest.fn();
const mockGetOne = jest.fn();
const mockManagerQuery = jest.fn();

const mockQueryBuilder = {
  where: jest.fn().mockReturnThis(),
  andWhere: jest.fn().mockReturnThis(),
  orderBy: jest.fn().mockReturnThis(),
  getCount: mockGetCount,
  getOne: mockGetOne,
};

const mockManager = {
  getRepository: jest.fn().mockReturnValue({
    createQueryBuilder: jest.fn().mockReturnValue(mockQueryBuilder),
  }),
  query: mockManagerQuery,
};

const mockConnectionService = {
  get: jest.fn().mockResolvedValue({ manager: mockManager }),
};

describe('WorkoutOccurrenceService.disableRepeatIfExceededMisses', () => {
  let service: any;

  beforeEach(() => {
    jest.clearAllMocks();
    service = Object.create(WorkoutOccurrenceService.prototype);
    service.connectionService = mockConnectionService;
  });

  it('returns 0 when total misses are below threshold', async () => {
    mockGetCount.mockResolvedValueOnce(2);

    const result = await service.disableRepeatIfExceededMisses(
      'customer-1',
      'workout-1',
      3,
      'studio-1',
    );

    expect(result).toBe(0);
    expect(mockManagerQuery).not.toHaveBeenCalled();
  });

  it('returns 0 when threshold reached but no future repeat occurrence exists', async () => {
    mockGetCount.mockResolvedValueOnce(3);
    mockGetOne.mockResolvedValueOnce(null);

    const result = await service.disableRepeatIfExceededMisses(
      'customer-1',
      'workout-1',
      3,
      'studio-1',
    );

    expect(result).toBe(0);
    expect(mockManagerQuery).not.toHaveBeenCalled();
  });

  it('updates isRepeat to false and returns count when threshold reached', async () => {
    mockGetCount.mockResolvedValueOnce(3);
    mockGetOne.mockResolvedValueOnce({ id: 'occurrence-1' });

    const result = await service.disableRepeatIfExceededMisses(
      'customer-1',
      'workout-1',
      3,
      'studio-1',
    );

    expect(result).toBe(3);
    expect(mockManagerQuery).toHaveBeenCalledWith(
      expect.stringContaining('UPDATE workout_occurrence'),
      ['customer-1', 'occurrence-1'],
    );
  });
});
```

- [ ] **Step 2: Run test to verify it fails**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-server
npx jest src/workout-occurrence/workout-occurrence.disable-repeat.spec.ts --no-coverage 2>&1 | tail -15
```

Expected: FAIL — `disableRepeatIfExceededMisses is not a function`.

- [ ] **Step 3: Implement the method**

In `fitstudiocrm-server/src/workout-occurrence/workout-occurrence.service.ts`, add the following public method near the end of the class (before the closing `}`). `ClientWorkoutStatus` and `WorkoutOccurrence` are already imported in this file.

```typescript
async disableRepeatIfExceededMisses(
  customerId: string,
  workoutId: string,
  threshold: number,
  clientId: string,
): Promise<number> {
  const dataSource = await this.connectionService.get(clientId);
  const manager = dataSource.manager;

  const count = await manager
    .getRepository(WorkoutOccurrence)
    .createQueryBuilder('wo')
    .where('wo."workoutId" = :workoutId', { workoutId })
    .andWhere('wo.processed = true')
    .andWhere(
      `EXISTS (
        SELECT 1 FROM jsonb_array_elements(wo.clients::jsonb) AS elem
        WHERE elem->>'id' = :customerId
        AND (elem->>'status')::int = :unvisited
      )`,
      { customerId, unvisited: ClientWorkoutStatus.Unvisited },
    )
    .getCount();

  if (count < threshold) return 0;

  const occurrence = await manager
    .getRepository(WorkoutOccurrence)
    .createQueryBuilder('wo')
    .where('wo."workoutId" = :workoutId', { workoutId })
    .andWhere('wo.processed = false')
    .andWhere(
      `EXISTS (
        SELECT 1 FROM jsonb_array_elements(wo.clients::jsonb) AS elem
        WHERE elem->>'id' = :customerId
        AND (elem->>'isRepeat')::boolean = true
      )`,
      { customerId },
    )
    .orderBy('wo.date', 'ASC')
    .getOne();

  if (!occurrence) return 0;

  await manager.query(
    `UPDATE workout_occurrence
     SET clients = (
       SELECT jsonb_agg(
         CASE
           WHEN elem->>'id' = $1
             THEN elem || '{"isRepeat": false}'::jsonb
           ELSE elem
         END
       )
       FROM jsonb_array_elements(clients::jsonb) AS elem
     )
     WHERE id = $2`,
    [customerId, occurrence.id],
  );

  return count;
}
```

- [ ] **Step 4: Run test to verify it passes**

```bash
npx jest src/workout-occurrence/workout-occurrence.disable-repeat.spec.ts --no-coverage 2>&1 | tail -10
```

Expected: 3/3 PASS.

- [ ] **Step 5: Commit**

```bash
git add src/workout-occurrence/workout-occurrence.service.ts src/workout-occurrence/workout-occurrence.disable-repeat.spec.ts
git commit -m "FC-136 Add disableRepeatIfExceededMisses to WorkoutOccurrenceService"
```

---

## Task 3: Wire helper into workoutsAndVisitsJob + notification

**Files:**
- Modify: `fitstudiocrm-server/src/tasks/tasks.service.ts`

**Background:** `workoutsAndVisitsJob(clientId: string)` already fetches `settings` near the top:
```typescript
const settings = await this.settingsService.find(clientId, RolesEnum.SuperAdmin);
```
The Unvisited update happens inside `for (const event of workoutOccurrences) { for (const eventClient of event.clients) { ... } }` around line 557. At that point, available variables are: `client` (Client entity — has `.id` and `.name`), `event.workoutId`, `parentWorkout` (Workout entity — has `.name`), `clientId` (studio UUID), `settings`. `TasksService` already has `workoutOccurrenceService` and `notificationsService` injected.

- [ ] **Step 1: Add call after Unvisited updateClient**

In `fitstudiocrm-server/src/tasks/tasks.service.ts`, find the switch case handling `ClientWorkoutStatus.Planned` / `ClientWorkoutStatus.Unvisited`. After the `updateClient` call with `status: ClientWorkoutStatus.Unvisited` and **before** the `break`, add:

```typescript
if (settings?.autoDisableRepeatAfterMisses) {
  const missCount =
    await this.workoutOccurrenceService.disableRepeatIfExceededMisses(
      client.id,
      event.workoutId,
      settings.autoDisableRepeatAfterMisses,
      clientId,
    );
  if (missCount > 0) {
    await this.notificationsService.create(
      clientId,
      `Клієнт ${client.name} автоматично знятий з повторного запису: ${parentWorkout.name} (пропущено ${missCount} разів)`,
    );
  }
}
```

- [ ] **Step 2: Build to verify**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-server
npm run build 2>&1 | tail -10
```

Expected: no TypeScript errors.

- [ ] **Step 3: Run all tests**

```bash
npm test 2>&1 | tail -10
```

Expected: all tests pass (including the 3 new helper tests).

- [ ] **Step 4: Commit**

```bash
git add src/tasks/tasks.service.ts
git commit -m "FC-136 Wire auto-disable repeat into daily scheduler with notification"
```

---

## Task 4: Frontend — Settings model + Functions tab UI

**Files:**
- Modify: `fitstudiocrm-app/src/models/` (file containing `ISettingsModel` interface)
- Modify: `fitstudiocrm-app/src/components/admin-panel.vue`

**Background:** The Functions tab is `<TabPanel value="2">` inside `admin-panel.vue`. Settings are stored in `currentSettings = ref<ISettingsModel>({...})`. The save function `onSaveFunctions()` sends `Partial<ISettingsModel>` via `api.patch('settings/{id}', data)`. `InputNumber` from PrimeVue is already used in this tab for `maxEventCancelTimeHour` and `minWorkoutAttendance`.

- [ ] **Step 1: Find ISettingsModel and add field**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-app
grep -r "maxEventCancelTimeHour" src/models/ --include="*.ts" -l
```

Open the file found above and add inside `ISettingsModel`:

```typescript
autoDisableRepeatAfterMisses?: number | null;
```

- [ ] **Step 2: Add InputNumber to Functions tab**

In `fitstudiocrm-app/src/components/admin-panel.vue`, inside `<TabPanel value="2">` after the `minWorkoutAttendance` `<FloatLabel>` block, add:

```vue
<FloatLabel>
  <InputNumber
    id="autoDisableRepeatAfterMisses"
    v-model="currentSettings.autoDisableRepeatAfterMisses"
    :min="1"
    :allow-empty="true"
  />
  <label for="autoDisableRepeatAfterMisses">
    Знімати повторний запис після (пропусків)
  </label>
</FloatLabel>
```

- [ ] **Step 3: Add field to onSaveFunctions payload**

In `admin-panel.vue`, inside `onSaveFunctions()`, add to the `data` object:

```typescript
autoDisableRepeatAfterMisses: currentSettings.value.autoDisableRepeatAfterMisses ?? null,
```

- [ ] **Step 4: Build to verify**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-app
npm run build 2>&1 | tail -10
```

Expected: no TypeScript errors.

- [ ] **Step 5: Run tests**

```bash
npm run test:ci 2>&1 | tail -10
```

Expected: all tests pass.

- [ ] **Step 6: Commit**

```bash
git add src/models/ src/components/admin-panel.vue
git commit -m "FC-136 Add autoDisableRepeatAfterMisses input to Functions settings tab"
```

---

## Self-Review

**Spec coverage:**
- ✅ Count total (not consecutive) Unvisited per `(customerId, workoutId)` — Task 2
- ✅ Set `isRepeat: false` on earliest future unprocessed occurrence — Task 2
- ✅ Studio-wide admin notification after auto-disable — Task 3
- ✅ Nullable int setting in "Функції" tab — Tasks 1 + 4
- ✅ null/0/empty = feature disabled — Tasks 1 + 4

**Placeholder scan:** None found.

**Type consistency:**
- `disableRepeatIfExceededMisses(customerId, workoutId, threshold, clientId): Promise<number>` — identical signature in Task 2 spec/test and Task 3 call site
- `autoDisableRepeatAfterMisses: number | null` — consistent across entity (Task 1), interface (Task 4), and payload (Task 4)
- Return value `0` = not triggered, positive number = miss count — consistent in Task 2 impl and Task 3 check `missCount > 0`

# FC-110: Add Clients Without Phone to Report Page — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a "Потребують уточнення" option to the report filter select that shows a paginated, searchable list of clients whose `phone IS NULL`, displaying only the name column.

**Architecture:** `GET client/report` gains an optional `withoutPhone=true` query param; the service appends `WHERE c.phone IS NULL` (or `AND c.phone IS NULL`) to its existing raw-SQL WHERE clause without touching pagination or sorting logic. The frontend adds a `NeedsClarification` enum value, a dedicated fetch function, and a single-column DataTable that reuses the existing paginator.

**Tech Stack:** NestJS (`@Query` decorator), raw SQL (PostgreSQL), Vue 3 + PrimeVue `DataTable` / `Paginator`, Vitest.

---

## File Map

| Action | File | Responsibility |
|---|---|---|
| Modify | `fitstudiocrm-server/src/client/client.controller.ts` | Accept `withoutPhone` query param, pass to service |
| Modify | `fitstudiocrm-server/src/client/client.service.ts` | Append `phone IS NULL` condition when flag is true |
| Modify | `fitstudiocrm-app/src/models/enums.ts` | Add `NeedsClarification` to `ReportFilters` |
| Modify | `fitstudiocrm-app/src/pages/reports.vue` | Filter handler, fetch function, single-column table |
| Create | `fitstudiocrm-app/src/pages/__tests__/reports-without-phone.spec.ts` | Vitest test for the new filter option |

> `reportFilterOptions` in `constants.ts` is `Object.values(ReportFilters)` — it picks up new enum values automatically. No change needed.

---

## Task 1: Backend — `withoutPhone` filter on `client/report`

**Files:**
- Modify: `fitstudiocrm-server/src/client/client.controller.ts`
- Modify: `fitstudiocrm-server/src/client/client.service.ts`

**Background:** `clientsReport()` builds a raw-SQL query. It constructs a `sqlSearch` string that starts as `''` and becomes `WHERE (c.name ILIKE $3 OR c.email ILIKE $3 OR c.phone ILIKE $3)` when `search` is non-empty. The phone filter must be appended to this string without breaking the `$3` parameter index.

- [ ] **Step 1: Add `withoutPhone` param to the service method**

In `fitstudiocrm-server/src/client/client.service.ts`, update the `clientsReport` method signature — add `withoutPhone: boolean = false` as the last parameter before `clientId`:

```typescript
async clientsReport(
  search: string,
  currentPage: number,
  pageSize: number,
  sortDir: 'asc' | 'desc',
  sortBy: ExportClientReportFilters,
  from: string,
  to: string,
  withoutPhone: boolean,
  clientId: string,
  role: RolesEnum,
)
```

Then, directly after the existing `sqlSearch` construction block (the `if (search && search !== '') { ... }` block), add:

```typescript
if (withoutPhone) {
  if (sqlSearch === '') {
    sqlSearch = 'WHERE c.phone IS NULL';
  } else {
    sqlSearch += ' AND c.phone IS NULL';
  }
}
```

- [ ] **Step 2: Add `withoutPhone` query param to the controller**

In `fitstudiocrm-server/src/client/client.controller.ts`, add `@Query('withoutPhone') withoutPhone?: string` to the `clientsReport` handler and pass it to the service:

```typescript
@Get('report')
clientsReport(
  @Query('currentPage') currentPage: string,
  @Query('pageSize') pageSize: string,
  @Query('sort') sort: 'asc' | 'desc',
  @Query('sortField') sortField: ExportClientReportFilters,
  @Query('search') search: string,
  @Query('from') from: string,
  @Query('to') to: string,
  @Query('withoutPhone') withoutPhone?: string,
  @Headers() headers: IControllerHeaderModel,
  @Req() req: Request,
) {
  return this.clientService.clientsReport(
    search,
    Number(currentPage),
    Number(pageSize),
    sort,
    sortField,
    from,
    to,
    withoutPhone === 'true',
    headers.appid,
    req['role'],
  );
}
```

(Keep all existing arguments — only add `withoutPhone === 'true'` in the correct position matching the updated service signature.)

- [ ] **Step 3: Build to verify TypeScript**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-server
npm run build 2>&1 | tail -10
```

Expected: no TypeScript errors.

- [ ] **Step 4: Run all server tests**

```bash
npm test 2>&1 | tail -10
```

Expected: all existing tests pass.

- [ ] **Step 5: Commit**

```bash
git add src/client/client.controller.ts src/client/client.service.ts
git commit -m "FC-110 Add withoutPhone filter to client/report endpoint"
```

---

## Task 2: Frontend — enum + filter UI + single-column table

**Files:**
- Modify: `fitstudiocrm-app/src/models/enums.ts`
- Modify: `fitstudiocrm-app/src/pages/reports.vue`
- Create: `fitstudiocrm-app/src/pages/__tests__/reports-without-phone.spec.ts`

**Background:** `reportFilterOptions` is `Object.values(ReportFilters)` — adding a new enum value is enough to make it appear in the select. The filter switch in `onFilter()` controls which table is shown via reactive booleans (e.g. `showClientsTable`). `getClients()` is the existing fetch for the Clients report.

- [ ] **Step 1: Write the failing test**

Create `fitstudiocrm-app/src/pages/__tests__/reports-without-phone.spec.ts`:

```typescript
/* eslint-disable */
import { describe, it, expect } from 'vitest';
import { ReportFilters } from '../../models/enums';
import { reportFilterOptions } from '../../models/constants';

describe('FC-110 — NeedsClarification filter', () => {
  it('ReportFilters enum contains NeedsClarification', () => {
    expect(ReportFilters.NeedsClarification).toBe('Потребують уточнення');
  });

  it('reportFilterOptions includes the new option', () => {
    expect(reportFilterOptions).toContain('Потребують уточнення');
  });
});
```

- [ ] **Step 2: Run test to verify it fails**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-app
npx vitest run src/pages/__tests__/reports-without-phone.spec.ts 2>&1 | tail -15
```

Expected: FAIL — `ReportFilters.NeedsClarification` is undefined.

- [ ] **Step 3: Add `NeedsClarification` to `ReportFilters` enum**

In `fitstudiocrm-app/src/models/enums.ts`, add to the `ReportFilters` enum after `Advanced`:

```typescript
export enum ReportFilters {
  Workouts = "Тренування",
  Plans = "Абонементи",
  Products = "Продукти",
  Clients = "Клієнти",
  Advanced = "Розширений звіт",
  NeedsClarification = "Потребують уточнення",
}
```

- [ ] **Step 4: Run test to verify it passes**

```bash
npx vitest run src/pages/__tests__/reports-without-phone.spec.ts 2>&1 | tail -10
```

Expected: 2/2 PASS.

- [ ] **Step 5: Add state variable and fetch function to `reports.vue`**

In `fitstudiocrm-app/src/pages/reports.vue`:

**A. Add reactive state** (near the other `showXxxTable` refs, around line 59):

```typescript
const showClarificationTable = ref(false);
const clarificationList = ref<{ id: string; name: string }[]>([]);
const clarificationTotalRecords = ref(0);
const clarificationPage = ref(0);
```

**B. Add fetch function** (near `getClients`, around line 310):

```typescript
const getClarificationClients = async (event?: any) => {
  loading.value = true;
  const currentPage = event ? event.first / event.rows + 1 : 1;
  clarificationPage.value = event ? event.first : 0;
  const pageSize = event ? event.rows : 10;
  const response = await api.get<ApiResponse<{ id: string; name: string }[]>>(
    `client/report?withoutPhone=true&currentPage=${currentPage}&pageSize=${pageSize}&search=${searchText.value}`,
  );
  clarificationList.value = response.data;
  clarificationTotalRecords.value = response.totalCount;
  loading.value = false;
};
```

**C. Add case to `onFilter` switch** (in the switch that handles `reportFilter.value`, after the `ReportFilters.Clients` case):

```typescript
case ReportFilters.NeedsClarification: {
  showChart.value = false;
  showClientsTable.value = false;
  showClarificationTable.value = true;
  await getClarificationClients();
  break;
}
```

Also reset `showClarificationTable.value = false;` in all other cases that set `showClientsTable` etc. (wherever other cases reset each other's show flags — follow the existing pattern).

**D. Add the table template** (after the existing clients DataTable block, still inside `<div v-if="showClarificationTable">`):

```vue
<div v-if="showClarificationTable">
  <DataTable
    :value="clarificationList"
    :loading="loading"
    lazy
    paginator
    :rows="10"
    :rows-per-page-options="[10, 20, 50]"
    :total-records="clarificationTotalRecords"
    :first="clarificationPage"
    @page="getClarificationClients"
  >
    <Column field="name" header="Ім'я" />
  </DataTable>
</div>
```

- [ ] **Step 6: Build to verify**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-app
npm run build 2>&1 | tail -10
```

Expected: no TypeScript errors.

- [ ] **Step 7: Run all FE tests**

```bash
npm run test:ci 2>&1 | tail -10
```

Expected: all tests pass including the 2 new ones.

- [ ] **Step 8: Commit**

```bash
git add src/models/enums.ts src/pages/reports.vue src/pages/__tests__/reports-without-phone.spec.ts
git commit -m "FC-110 Add NeedsClarification filter option to reports page"
```

---

## Self-Review

**Spec coverage:**
- ✅ New option in `ReportFilters` select — Task 2 (enum + auto-picked by `Object.values`)
- ✅ Backend filters by `phone IS NULL` — Task 1 (sqlSearch modification)
- ✅ Pagination reused — Task 2 (DataTable lazy + `@page="getClarificationClients"`)
- ✅ Search still works — `searchText.value` passed in `getClarificationClients`
- ✅ Single name column — Task 2 (only `<Column field="name">`)

**Placeholder scan:** None found.

**Type consistency:**
- `withoutPhone: boolean` — matches service signature (Task 1 step 1) and controller conversion `withoutPhone === 'true'` (Task 1 step 2)
- `clarificationList: ref<{ id: string; name: string }[]>` — matches the `name` field used in the Column definition (Task 2 step 5)
- `getClarificationClients` — same name in state setup, fetch definition, `onFilter` case, and `@page` binding

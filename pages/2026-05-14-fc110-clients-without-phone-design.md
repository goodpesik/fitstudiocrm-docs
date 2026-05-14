# FC-110: Add Clients Without Phone to Report Page

## Goal

Add a new "Потребують уточнення" option to the report page's main filter select. When selected, it shows a paginated list of clients who have no phone number (`phone IS NULL`), displaying only the client name column.

## Actions

1. Add `withoutPhone?: boolean` query param to the existing `GET client/report` endpoint
2. Backend filters by `phone IS NULL` when the param is true, reusing all existing pagination logic
3. Frontend adds new filter option and renders a single-column name table for this view

## Architecture

### Backend — `client/report` endpoint

**File:** `fitstudiocrm-server/src/client/client.service.ts` (or wherever the report query is built)

Add `withoutPhone?: boolean` to the query params. In the QueryBuilder for `client/report`, if `withoutPhone === true`, append:

```
.andWhere('client.phone IS NULL')
```

All existing params (`currentPage`, `pageSize`, `search`, `sort`, `sortField`, `from`, `to`) remain unchanged and continue to work normally.

Returns the same `IClientReportModel[]` shape — no new DTO needed.

### Frontend — enum + constants

**File:** `fitstudiocrm-app/src/models/enums.ts`

Add to `ReportFilters`:
```typescript
NeedsClarification = "Потребують уточнення"
```

**File:** `fitstudiocrm-app/src/models/constants.ts` (or wherever `reportFilterOptions` is defined)

Add `ReportFilters.NeedsClarification` to the options array.

### Frontend — reports.vue

**File:** `fitstudiocrm-app/src/pages/reports.vue`

When `ReportFilters.NeedsClarification` is selected:
- Call `GET client/report?withoutPhone=true&currentPage=...&pageSize=...&search=...`
- Render a table with a single "Ім'я" column (no workout counts, no plan info)
- Reuse the existing pagination component
- Search input remains functional (filters by name)

## File Map

| Action | File | Responsibility |
|---|---|---|
| Modify | `fitstudiocrm-server/src/client/client.service.ts` | Add `withoutPhone` filter to report query |
| Modify | `fitstudiocrm-server/src/client/client.controller.ts` | Accept `withoutPhone` query param |
| Modify | `fitstudiocrm-app/src/models/enums.ts` | Add `NeedsClarification` to `ReportFilters` |
| Modify | `fitstudiocrm-app/src/models/constants.ts` | Add option to `reportFilterOptions` |
| Modify | `fitstudiocrm-app/src/pages/reports.vue` | Render single-column table + API call with `withoutPhone=true` |

## Out of Scope

- No new backend endpoint — reuses `client/report`
- No export/download of this list
- No editing clients from this view (read-only)
- No additional columns beyond name

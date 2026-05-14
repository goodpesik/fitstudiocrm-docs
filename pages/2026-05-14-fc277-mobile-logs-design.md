# FC-277: Mobile App — Add Logs

## Goal

Log key user interactions from the mobile app (booking, cancellation, workout creation, time/room changes) using NestJS Logger, with user role included in every log entry.

## Actions to Log

| Endpoint | Method | Description |
|---|---|---|
| `POST /book-workout` | POST | Client/coach/admin books a workout |
| `POST /cancel-workout` | POST | Any role cancels a workout |
| `POST /create-workout` | POST | Coach/admin creates a workout |
| `PATCH /change-occurrence-time` | PATCH | Admin/coach changes occurrence time |
| `PATCH /change-occurrence-room` | PATCH | Admin/coach changes occurrence room |

## Architecture

### LoggingInterceptor

New file: `fitstudiocrm-mobile-server/src/logging/logging.interceptor.ts`

- Implements `NestInterceptor`
- Has `private readonly logger = new Logger('MobileActions')`
- Injects `DataSource` (TypeORM) directly to fetch the Customer entity — avoids circular dependency with `CustomerService`
- Uses `tap()` on the response Observable to log only after successful handler execution
- Gets `userId` from `request['userId']`
- Fetches `Customer` by `userId`, finds `customers.find(c => c.isSelected)` to get `role`
- If no selected customer found, falls back to `'unknown'`

### Log Format

```
[ROLE] user:<userId> action:<endpoint>
```

Examples:
```
[Customer] user:abc-123 action:book-workout
[Coach] user:def-456 action:create-workout
[Admin] user:ghi-789 action:change-occurrence-time
```

### Applying the Interceptor

In `customer.controller.ts`, apply `@UseInterceptors(LoggingInterceptor)` on each of the 5 methods individually (not at class level, to avoid logging unrelated endpoints).

## File Map

| Action | File |
|---|---|
| Create | `fitstudiocrm-mobile-server/src/logging/logging.interceptor.ts` |
| Modify | `fitstudiocrm-mobile-server/src/customer/customer.controller.ts` |
| Modify | `fitstudiocrm-mobile-server/src/app.module.ts` |

## Out of Scope

- No database storage of logs
- No log viewer UI
- No logging of read-only (GET) endpoints
- No retry/error-path logging (only successful responses)

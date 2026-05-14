# FC-277: Mobile App Logs Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a `LoggingInterceptor` to `fitstudiocrm-mobile-server` that logs booking, cancellation, workout creation, and occurrence time/room changes with the acting user's role.

**Architecture:** A single `NestJS` interceptor (`LoggingInterceptor`) injected into `CustomerService` dependency chain via `ConnectionService`. It resolves the user's role from the `Customer` entity (`customers.find(c => c.isSelected).role`) and calls `this.logger.log()` after each successful handler execution using `tap()` on the RxJS Observable.

**Tech Stack:** NestJS (`NestInterceptor`, `Logger`), RxJS (`tap`), TypeORM via `ConnectionService`.

---

## File Map

| Action | File | Responsibility |
|---|---|---|
| Create | `fitstudiocrm-mobile-server/src/logging/logging.interceptor.ts` | Intercept + log 5 actions with role |
| Modify | `fitstudiocrm-mobile-server/src/customer/customer.controller.ts` | Apply `@UseInterceptors(LoggingInterceptor)` on 5 methods |
| Modify | `fitstudiocrm-mobile-server/src/customer/customer.module.ts` | Register `LoggingInterceptor` as provider |

---

## Task 1: Create LoggingInterceptor

**Files:**
- Create: `fitstudiocrm-mobile-server/src/logging/logging.interceptor.ts`
- Test: `fitstudiocrm-mobile-server/src/logging/logging.interceptor.spec.ts`

- [ ] **Step 1: Write the failing test**

Create `fitstudiocrm-mobile-server/src/logging/logging.interceptor.spec.ts`:

```typescript
/* eslint-disable */
import { LoggingInterceptor } from './logging.interceptor';
import { of } from 'rxjs';
import { Customer } from '../customer/customer.entity';
import { ICustomerRolesEnum } from '../models/enums';

const mockCustomer: Partial<Customer> = {
  id: 'user-1',
  customers: [
    { id: 'c-1', isSelected: true, role: ICustomerRolesEnum.Coach } as any,
  ],
};

const mockConnectionService = {
  get: jest.fn().mockResolvedValue({
    manager: {
      findOneBy: jest.fn().mockResolvedValue(mockCustomer),
    },
  }),
};

const mockLoggerLog = jest.fn();

describe('LoggingInterceptor', () => {
  let interceptor: LoggingInterceptor;

  beforeEach(() => {
    interceptor = new LoggingInterceptor(mockConnectionService as any);
    (interceptor as any).logger.log = mockLoggerLog;
    jest.clearAllMocks();
  });

  it('logs action with role after successful handler', async () => {
    const mockContext = {
      switchToHttp: () => ({
        getRequest: () => ({
          'userId': 'user-1',
          url: '/customer/book-workout',
        }),
      }),
    } as any;

    const mockNext = {
      handle: () => of({ success: true }),
    };

    await new Promise<void>((resolve) => {
      interceptor.intercept(mockContext, mockNext).subscribe({
        complete: resolve,
      });
    });

    expect(mockLoggerLog).toHaveBeenCalledWith(
      '[Coach] user:user-1 action:book-workout',
    );
  });

  it('falls back to unknown when no selected customer', async () => {
    mockConnectionService.get.mockResolvedValueOnce({
      manager: {
        findOneBy: jest.fn().mockResolvedValue({
          id: 'user-2',
          customers: [],
        }),
      },
    });

    const mockContext = {
      switchToHttp: () => ({
        getRequest: () => ({
          'userId': 'user-2',
          url: '/customer/cancel-workout',
        }),
      }),
    } as any;

    const mockNext = { handle: () => of(null) };

    await new Promise<void>((resolve) => {
      interceptor.intercept(mockContext, mockNext).subscribe({
        complete: resolve,
      });
    });

    expect(mockLoggerLog).toHaveBeenCalledWith(
      '[unknown] user:user-2 action:cancel-workout',
    );
  });
});
```

- [ ] **Step 2: Run test to verify it fails**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-mobile-server
npx jest src/logging/logging.interceptor.spec.ts --no-coverage 2>&1 | tail -15
```

Expected: FAIL — `LoggingInterceptor` not found.

- [ ] **Step 3: Create the interceptor**

Create `fitstudiocrm-mobile-server/src/logging/logging.interceptor.ts`:

```typescript
import {
  CallHandler,
  ExecutionContext,
  Injectable,
  Logger,
  NestInterceptor,
} from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';
import { ConnectionService } from '../database/connections.service';
import { Customer } from '../customer/customer.entity';

@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  private readonly logger = new Logger('MobileActions');

  constructor(private readonly connectionService: ConnectionService) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<unknown> {
    const request = context.switchToHttp().getRequest();
    const userId: string = request['userId'];
    const action = request.url?.split('/').pop() ?? 'unknown';

    return next.handle().pipe(
      tap(async () => {
        try {
          const dataSource = await this.connectionService.get();
          const manager = dataSource.manager;
          const customer = await manager.findOneBy(Customer, { id: userId });
          const selected = customer?.customers?.find((c) => c.isSelected);
          const role = selected?.role ?? 'unknown';
          this.logger.log(`[${role}] user:${userId} action:${action}`);
        } catch {
          this.logger.log(`[unknown] user:${userId} action:${action}`);
        }
      }),
    );
  }
}
```

- [ ] **Step 4: Run test to verify it passes**

```bash
npx jest src/logging/logging.interceptor.spec.ts --no-coverage 2>&1 | tail -10
```

Expected: 2/2 PASS.

- [ ] **Step 5: Commit**

```bash
git add src/logging/logging.interceptor.ts src/logging/logging.interceptor.spec.ts
git commit -m "FC-277 Add LoggingInterceptor for mobile user actions"
```

---

## Task 2: Apply interceptor to 5 controller methods

**Files:**
- Modify: `fitstudiocrm-mobile-server/src/customer/customer.controller.ts`
- Modify: `fitstudiocrm-mobile-server/src/customer/customer.module.ts`

- [ ] **Step 1: Register LoggingInterceptor in CustomerModule**

In `fitstudiocrm-mobile-server/src/customer/customer.module.ts`, add `LoggingInterceptor` to providers:

```typescript
import { Global, Module } from '@nestjs/common';
import { CustomerService } from './customer.service';
import { CustomerController } from './customer.controller';
import { LoggingInterceptor } from '../logging/logging.interceptor';

@Global()
@Module({
  controllers: [CustomerController],
  providers: [CustomerService, LoggingInterceptor],
  exports: [CustomerService],
})
export class CustomerModule {}
```

- [ ] **Step 2: Add `@UseInterceptors(LoggingInterceptor)` to 5 methods**

In `fitstudiocrm-mobile-server/src/customer/customer.controller.ts`, add the import at the top:

```typescript
import { UseInterceptors } from '@nestjs/common';
import { LoggingInterceptor } from '../logging/logging.interceptor';
```

Then add `@UseInterceptors(LoggingInterceptor)` decorator above each of these 5 methods:

1. `cancelWorkout` (line ~152) — add `@UseInterceptors(LoggingInterceptor)` between `@Post('cancel-workout')` and the method
2. `bookWorkout` (line ~172)
3. `createWorkout` (line ~297)
4. `changeOccurrenceTime` (line ~322)
5. `changeOccurrenceRoom` (line ~338)

Example for `cancelWorkout`:
```typescript
@Post('cancel-workout')
@UseInterceptors(LoggingInterceptor)
cancelWorkout(@Req() req: Request, @Body() body: IServerRequestModel) {
  // existing body unchanged
```

- [ ] **Step 3: Build**

```bash
cd /Users/maksymlevynets/Projects/Fitstudiocrm/fitstudiocrm-mobile-server
npm run build 2>&1 | tail -10
```

Expected: no TypeScript errors.

- [ ] **Step 4: Run all tests**

```bash
npm test 2>&1 | tail -10
```

Expected: all tests pass (including the 2 new interceptor tests).

- [ ] **Step 5: Commit**

```bash
git add src/customer/customer.controller.ts src/customer/customer.module.ts
git commit -m "FC-277 Apply LoggingInterceptor to book/cancel/create/change-time/change-room"
```

---

## Self-Review

**Spec coverage:**
- ✅ Logs book-workout, cancel-workout, create-workout, change-occurrence-time, change-occurrence-room
- ✅ Role resolved from `customers.find(c => c.isSelected).role`
- ✅ Fallback to `'unknown'` if no selected customer
- ✅ Logs only after successful handler (via `tap`)
- ✅ Format: `[ROLE] user:<userId> action:<endpoint>`

**Placeholder scan:** None found.

**Type consistency:** `ConnectionService` and `Customer` used consistently across interceptor and tests.

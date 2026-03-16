# NurKit Standards
> Read when: starting a new file, unsure about style, structure, or types.
> These are principles — not library names. They work in any language, any framework.

---

## The Mindset

Before writing any code, think:
- What could go wrong with this?
- Who reads this in 6 months with no context?
- What happens when data is empty, the user is on a slow connection, or two users do this simultaneously?
- What is the smallest change that solves this correctly?

Write for that future. Not just for making it work today.

---

## File Header — Mandatory on Every File

Every file starts with this header. No exceptions. Update it every time the file is modified.

```
// ============================================
// FILE: [filename with extension]
// PURPOSE: [one sentence — what this file does and nothing else]
// STATUS: stable | in-progress | needs-refactor | has-known-issues
// ─────────────────────────────────────────────
// CONTAINS:
//   [functionName]   — [one line: what it does, inputs, output]
//   [functionName]   — [one line: what it does, inputs, output]
// ─────────────────────────────────────────────
// IMPORTS FROM: [file1, file2, ...]
// IMPORTED BY:  [file1, file2, ...]
// ─────────────────────────────────────────────
// CREATED:      [date]
// LAST UPDATED: [date]
// LAST CHANGE:  [feature or fix name e.g. feat/add-refund, fix/auth-timeout]
// ─────────────────────────────────────────────
// CHANGELOG (last 3 only — remove oldest when adding new):
//   [date]: [what changed]
//   [date]: [what changed]
//   [date]: [what changed]
// ─────────────────────────────────────────────
// ⚠ CRITICAL DEPS: [only if this file has a dependency that
//                   if removed/changed breaks many other things]
// ============================================
```

### Header Rules
- CONTAINS describes every exported function — name AND what it does
- CHANGELOG keeps only the last 3 entries — remove the oldest when adding a new one
- CRITICAL DEPS is optional — only add it when genuinely critical
- STATUS must be honest — if the file has known issues, say so
- Update LAST UPDATED and LAST CHANGE every single time the file is touched

### Header Mismatch Rule
If you open a file and the header does not match the actual code:
- Stop before doing any other work
- Identify what is wrong (header outdated? code drifted? file grown too large?)
- Resolve the mismatch first
- Never proceed with a task on a file whose header is a lie
See AGENT.md for the exact mismatch detection block to output.

---

## Folder Structure — Feature-Based, Framework-First

### The Golden Rule
**Follow the framework's conventions first. Apply feature grouping within that.**

If you are in Next.js, respect `app/` or `pages/`. If you are in Laravel, respect `Controllers/`, `Models/`. Never fight the framework to impose a structure it was not designed for.

Within the framework's structure, organise by feature — not by type.

### Feature-Based vs Type-Based

**Type-based (do NOT use):**
```
src/
├── controllers/     ← all controllers from all features mixed together
├── services/        ← all services from all features mixed together
└── models/          ← all models from all features mixed together
```
Problem: to work on one feature you jump across 3+ folders. Files from unrelated features sit next to each other.

**Feature-based (use this):**
```
src/
├── features/
│   ├── auth/
│   │   ├── index.ts            ← public door — only exports what others may use
│   │   ├── auth.controller.ts  ← HTTP layer only
│   │   ├── auth.service.ts     ← business logic only
│   │   ├── auth.middleware.ts  ← JWT validation only
│   │   ├── auth.types.ts       ← auth-specific types only
│   │   └── auth.constants.ts   ← auth-specific constants only
│   ├── orders/
│   │   ├── index.ts
│   │   ├── orders.controller.ts
│   │   ├── orders.service.ts
│   │   ├── orders.types.ts
│   │   └── orders.constants.ts
│   └── users/
│       ├── index.ts
│       └── ...
├── shared/
│   ├── types/
│   │   ├── index.ts            ← single door for all shared types
│   │   ├── common.types.ts     ← PaginatedResponse, ApiResponse, ErrorShape
│   │   └── entities.types.ts   ← entity types used across features
│   ├── utils/
│   │   ├── validation.ts
│   │   ├── formatting.ts
│   │   └── crypto.ts
│   ├── middleware/
│   │   └── error-handler.ts
│   └── constants/
│       └── app.constants.ts
└── config/
    ├── database.ts             ← DB connection only
    └── env.ts                  ← ALL environment variable reads — nowhere else
```

### Folder Rules
- Maximum 3 levels deep: `features/orders/utils/` is fine — deeper is a signal to rethink
- A new feature = a new folder dropped in — nothing else changes
- When deleting a feature = delete its folder — no hunt across multiple directories
- `shared/` only for code used by more than one feature
- If something is only used by one feature, it stays inside that feature's folder

### Index Files — The Public Door
Every feature folder has an `index` file that declares the public API of that feature:

```typescript
// features/orders/index.ts
export { createOrder } from './orders.service'
export { getOrderById } from './orders.service'
export type { Order, OrderStatus } from './orders.types'
// Internal functions are NOT exported here — they stay private
```

Other features import from the door — never from internal files:
```typescript
// CORRECT
import { createOrder } from '@/features/orders'

// WRONG — bypasses the door, creates hidden coupling
import { createOrder } from '@/features/orders/orders.service'
```

### No Cross-Feature Imports
Features never import directly from each other.
If Feature A needs something from Feature B, that something belongs in `shared/`.

```
features/auth    → can import from shared/
features/orders  → can import from shared/
features/auth    → NEVER imports from features/orders directly
features/orders  → NEVER imports from features/auth directly
```

---

## Single Source of Truth for Types

### The Two Levels of Type Ownership

**Level 1 — Feature types**
Types that belong to one feature live in that feature's types file only.
```
features/orders/orders.types.ts   ← Order, CreateOrderInput, OrderStatus
features/users/users.types.ts     ← User, UserRole, CreateUserInput
features/invoices/invoices.types.ts ← Invoice, InvoiceLineItem
```

**Level 2 — Shared types**
Types used by more than one feature live in `shared/types/` only.
```
shared/types/common.types.ts    ← PaginatedResponse, ApiResponse<T>, ErrorShape
shared/types/entities.types.ts  ← Core entity shapes shared across features
shared/types/index.ts           ← Re-exports everything — single import point
```

### The Type Check (mandatory before defining any new type)
1. Check `shared/types/index.ts` — does this type already exist?
2. Check the current feature's types file — does it exist there?
3. Only define it if it exists nowhere
4. If it exists → import it, never redefine it

### Type Import Rules
```typescript
// Shared types — always import from the single door
import type { PaginatedResponse, ApiResponse } from '@/shared/types'

// Feature types — import from the feature's types file directly
import type { Order, OrderStatus } from './orders.types'

// WRONG — redefining something that already exists
type Order = { id: string; status: string }  // ← check first, never do this
```

### The Blueprint Must Define Type Ownership
Before the checklist is generated, the blueprint must include a Type Ownership section that lists which types live where. The agent never creates a type file without this map existing first.

---

## Constants — No Magic Values

Every feature has a constants file. No magic strings or numbers anywhere in logic.

```typescript
// features/orders/orders.constants.ts
export const ORDER_STATUS = {
  PENDING: 'pending',
  CONFIRMED: 'confirmed',
  SHIPPED: 'shipped',
  CANCELLED: 'cancelled',
} as const

export const ORDER_LIMITS = {
  MAX_ITEMS_PER_ORDER: 100,
  MIN_ORDER_AMOUNT: 1,
} as const
```

App-wide constants live in `shared/constants/app.constants.ts`.

---

## Config — One File, One Place

All environment variable reads happen in exactly one file: `config/env.ts` (or equivalent).
No feature file ever reads `process.env` directly.

```typescript
// config/env.ts — THE ONLY FILE THAT READS process.env
export const config = {
  port: Number(process.env.PORT ?? 3000),
  databaseUrl: process.env.DATABASE_URL!,
  jwtSecret: process.env.JWT_SECRET!,
  jwtExpiresIn: process.env.JWT_EXPIRES_IN ?? '15m',
}

// features/auth/auth.service.ts — imports from config, never from process.env
import { config } from '@/config/env'
```

---

## Validation — Boundary Only

Validation happens at the entry point of each feature (controller or route handler).
Never inside services. Never in the database layer. Never duplicated.

```
Request arrives
→ Controller/Route: validate ALL inputs (boundary)
→ Service: trusts the input, applies business logic
→ Database/Repository: trusts the service
```

---

## Code Quality & Style

### One File, One Responsibility
- Each file does exactly one thing — named after that one thing
- If you need to scroll far to read a function, split the file
- If a file grows large, extract — never keep adding

### Function Design
- Functions do one thing, named after that one thing
- If a function needs a comment to explain what it does → rename it or split it
- Early returns over nested conditionals — fail fast, happy path at the bottom
- No function takes more than 3-4 parameters — use an options object beyond that
- No nested ternaries. Ever.

### Naming
- Names are phrases, not abbreviations (`getUsersWithExpiredTokens` not `getUsers2`)
- Booleans: `is`, `has`, `can`, `should` prefix (`isLoading`, `hasPermission`)
- Functions named after what they return or what they do
- Never single-letter variables except `i` in a short for loop
- Constants: `SCREAMING_SNAKE_CASE`

### Spacing — Logical Groups, Not Line-by-Line
```typescript
// CORRECT — blank line between logical steps, related lines stay together
const user = await getUserById(id)
user.lastLogin = Date.now()
await saveUser(user)

const token = generateAccessToken(user)
const refresh = generateRefreshToken(user)

return { token, refresh }

// WRONG — blank line between every line (destroys visual grouping)
const user = await getUserById(id)

user.lastLogin = Date.now()

await saveUser(user)
```

Rules:
- Blank line between logical steps
- Blank line before every `return`
- Blank line before and after every block (`if`, `for`, `try`)
- Never two blank lines in a row

### Comments
```typescript
// GOOD — explains the decision
// Rotating refresh tokens on every use to prevent token reuse after logout

// BAD — explains what the code already shows
// Get the user
const user = await getUser(id)
```
- Comments explain WHY — never WHAT
- TODO format: `// TODO: [reason] — [when to address]`

---

## Security Principles
- Never trust input from any source — validate server-side always
- Never expose internal errors to the client — log internally, generic message externally
- Auth tokens must expire — always implement refresh logic
- Permissions checked server-side on every protected request — never rely on UI hiding things
- Sensitive data never logged, never returned unless explicitly required
- All secrets in environment variables — never hardcoded
- Database queries always parameterised — no string concatenation near user data
- Rate limiting on any endpoint accepting user input

---

## Performance Principles
- Never fetch more data than needed — select only fields you use
- Slow operations run in background — never block a request
- Review for N+1 queries before marking any list feature done
- Consider caching for data read often and changed rarely
- API list responses always paginated — never unbounded arrays

---

## Error Handling Principles
- Every async operation has error handling — no unhandled rejections
- Errors caught at the right level — not everything to a global handler
- Log with context: user id, action, timestamp, input shape (not sensitive values)
- User errors (4xx) vs system errors (5xx) handled differently
- Never swallow errors silently

---

## Language Agnostic Note

All of the above are principles. The syntax adapts to the language:

| Principle | Python | PHP/Laravel | Go | TypeScript |
|---|---|---|---|---|
| Feature folder | `features/orders/` | same | `internal/orders/` | same |
| Public door | `__init__.py` | Service Provider | exported funcs in `orders.go` | `index.ts` |
| Constants file | `constants.py` | `OrderConstants.php` | `constants.go` | `orders.constants.ts` |
| Types file | dataclasses / type hints | DTO classes | structs | `orders.types.ts` |
| Config centralised | `config.py` | config class | `config.go` | `config/env.ts` |

The structure stays the same. The syntax changes. The agent adapts to the project's language — it does not fight it.

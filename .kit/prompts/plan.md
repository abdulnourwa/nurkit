# NurKit — /kit plan prompt
> Context: {{CONTEXT}}
> Vision: {{VISION}}

---

You are a senior software architect producing a complete project blueprint.
This is the most important document in the project. Everything else is generated from it.
Be thorough. Be specific. Leave nothing vague. Do not write any code.

---

## Your Output: BLUEPRINT.md

Use this exact structure. Every section is mandatory.

---

### 1. Project Overview
One paragraph — what this is, who it is for, what problem it solves.

---

### 2. Tech Stack Recommendation
List the recommended stack based on the project's requirements.
Include brief reasoning for each choice.
Note: this will be finalised in STACK.md — keep it recommendation, not prescription.

---

### 3. Architecture Overview
- Architecture pattern (monolith / modular monolith / microservices — and why)
- How frontend and backend communicate
- Authentication approach and token strategy
- Data flow for the 2-3 most important operations

---

### 4. Folder Structure — COMPLETE AND EXACT
This section is critical. List every planned file with its one-line purpose.
Follow the feature-based structure from STANDARDS.md.
Follow the framework's conventions first, then apply feature grouping within.

Rules for this section:
- Every feature folder must contain: index file, controller/handler, service, types file, constants file
- `shared/types/` must be listed with its contents
- `shared/utils/` must be listed with its contents
- `config/` must list every config file
- No file listed without a purpose comment
- The agent builds ONLY inside this structure — new files outside it must be flagged

Example format:
```
src/
├── features/
│   ├── auth/
│   │   ├── index.ts              — public exports for auth feature
│   │   ├── auth.controller.ts    — HTTP request handling for auth routes
│   │   ├── auth.service.ts       — auth business logic: login, register, refresh
│   │   ├── auth.middleware.ts    — JWT validation middleware
│   │   ├── auth.types.ts         — User, LoginInput, TokenPair types
│   │   └── auth.constants.ts     — TOKEN_EXPIRY, AUTH_ERRORS constants
│   └── orders/
│       ├── index.ts              — public exports for orders feature
│       └── ...
├── shared/
│   ├── types/
│   │   ├── index.ts              — re-exports all shared types
│   │   ├── common.types.ts       — PaginatedResponse, ApiResponse, ErrorShape
│   │   └── entities.types.ts     — shared entity types used across features
│   ├── utils/
│   │   ├── validation.ts         — reusable input validation helpers
│   │   └── formatting.ts         — date, currency, string formatters
│   └── constants/
│       └── app.constants.ts      — app-wide constants
└── config/
    ├── env.ts                    — ALL environment variable reads — nowhere else
    └── database.ts               — database connection and configuration
```

---

### 5. Type Ownership Map
List every significant type and where it lives.
The agent uses this map to find or place types — it never searches, it looks here first.

Format:
```
## Shared Types (shared/types/)
- PaginatedResponse<T>   — used by all list endpoints
- ApiResponse<T>         — standard API response wrapper
- ErrorShape             — standard error response format

## Feature Types
- Order, OrderStatus, CreateOrderInput    → features/orders/orders.types.ts
- User, UserRole, CreateUserInput         → features/users/users.types.ts
- Invoice, InvoiceLineItem                → features/invoices/invoices.types.ts
```

---

### 6. Database Design
For every table or collection:
- Fields: name, type, constraints, description
- Relationships: foreign keys, cardinality
- Indexes: which fields and why

---

### 7. API Design
Group endpoints by feature.
For every endpoint:
- Method and path
- Who can call it (which roles)
- What it accepts (body/params/query shape)
- What it returns
- Edge cases and error responses

---

### 8. Feature Specifications
For every feature:

**[Feature Name]**
- Who uses it: [roles]
- Purpose: [what it does]
- Client workflow: [step by step — what client sees and does]
- Admin workflow: [step by step — what admin sees and does]
- Business rules: [rules that must never be broken]
- Data involved: [which tables/fields read or written]
- API endpoints: [list]
- UI screens: [list]
- Edge cases: [list]
- Validation rules: [every input field, its type, constraints]

---

### 9. UI Screens
For every screen:
- Route/path
- Accessible by: [roles]
- Purpose
- Components on this screen
- States: loading / empty / populated / error
- Actions available and where they navigate
- Mobile behaviour

---

### 10. Auth & Permissions
- Complete auth flow
- Token strategy (access + refresh)
- Permission checking approach
- Role permission matrix — what each role can and cannot do

---

### 11. Environment Variables
List every env variable needed with description.
These will be documented fully in ENV.md.

---

### 12. Phases Overview
List implementation phases in order.
For each phase: name, type (Backend/Frontend/DevOps), goal, what it depends on.
Frontend and backend phases must be separate — never mixed.

---

### 13. Open Questions
Anything still unclear after planning that needs user input before checklist is generated.
Do not guess — flag here.

---

## When Complete

Tell the user:
"Blueprint complete. Saved to [filename]. Run ./kit analyze to verify nothing was lost from the vision."

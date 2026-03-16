---
activation: model_decision
description: Apply when the agent is about to define a new type, interface, or data structure
---

# NurKit — Type Ownership Rules

Before defining any new type, interface, struct, or data class:

1. Check `.nurkit/` for the Type Ownership Map in the latest blueprint
2. Check `shared/types/index.ts` (or equivalent) — does this type exist?
3. Check the current feature's types file — does it exist there?
4. Only define it if it exists nowhere
5. If it exists → import it, never redefine it

## Where Types Live

- Types used by ONE feature → `features/[name]/[name].types.ts`
- Types used by MULTIPLE features → `shared/types/`
- All shared types exported through `shared/types/index.ts` only

## Wrong

```typescript
// Redefining something that already exists somewhere
type Order = { id: string; status: string }
```

## Correct

```typescript
// Import from the single source of truth
import type { Order } from '@/features/orders/orders.types'
import type { PaginatedResponse } from '@/shared/types'
```

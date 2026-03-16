# NurKit — /kit checklist prompt
> Context: {{CONTEXT}}
> Blueprint: {{BLUEPRINT}}
> Stack: {{STACK}}

---

You are converting a complete blueprint into an executable phased task list. The blueprint is finalised. Translate it into granular, specific tasks any engineer or AI agent can execute without making architectural decisions.

Use CHECKLIST-TEMPLATE.md as your shape reference.

## Rules for Writing Tasks

### Be Specific
- Bad: "Build auth system"
- Good: "Create JWT token generation and validation functions — target: `src/features/auth/auth.service.ts`"

### Include Target Files
Every task references the exact file it operates on.

### Frontend and Backend Are Always Separate Phases
Never mix them. All backend for a feature before its frontend.

### Label Every Phase
`[TYPE: Backend]`, `[TYPE: Frontend]`, or `[TYPE: DevOps]`

### Model Hints at Phase Type Transitions
When phase type changes add:
`⚡ MODEL HINT: This phase is [type]. Consider switching to a [type]-focused model.`

### Mark Critical Tasks
Tasks that block everything else: `[CRITICAL]` prefix.

### Include the Non-Obvious Tasks (always required, always forgotten)
Every phase must include where applicable:
- Create/update file header comments for every new file
- Empty state component for every list view
- Loading state for every async operation
- Error state for every async operation
- Form validation for every input field
- Confirmation dialog for every destructive action
- User feedback (toast/notification) for every action
- Update ENV.md when a new env variable is introduced
- Update STACK.md when a new dependency is added
- Update types file when new types are added
- Git commit after each task

### Types Tasks
Include explicit tasks for:
- Create `shared/types/common.types.ts` — define shared types
- Create `features/[name]/[name].types.ts` — define feature types
These must appear before any task that uses those types.

## Phase Order
1. Project setup & configuration (DevOps/Backend)
2. Database schema & types (Backend)
3. Shared types and utilities (Backend)
4. Core backend services (Backend)
5. Authentication & authorisation (Backend)
6. Feature-specific backend — one phase per major feature (Backend)
7. Admin UI — one phase per major feature area (Frontend)
8. Client UI — one phase per major feature area (Frontend)
9. Integration & end-to-end (Backend/Frontend)
10. Deployment & launch (DevOps)

## Output

Follow CHECKLIST-TEMPLATE.md exactly. Include the progress tracker table at the bottom.

When complete: "Checklist generated. [N] phases, [N] total tasks. Backend: [N] phases. Frontend: [N] phases. Run ./kit build"

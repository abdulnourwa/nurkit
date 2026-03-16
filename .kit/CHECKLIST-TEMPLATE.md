# NurKit Checklist Template
> This file is the permanent shape reference. Never modify it.
> Agent: use this structure when generating any checklist.

---

# Checklist — [PROJECT NAME] — v[N]
> Generated: [date]
> Blueprint: [blueprint filename]
> Gaps reviewed: [gaps filename]
> Total phases: [N]

---

## How to Read This Checklist

- `[TYPE: Backend]` — strong reasoning model recommended
- `[TYPE: Frontend]` — UI-focused model recommended
- `[TYPE: DevOps]` — strong reasoning model recommended
- `⚡ MODEL HINT` — suggested model switch point for the user
- `[CRITICAL]` — must be done before this phase can close
- Every task includes target file so agent knows exactly where to work

---

## Phase 1 — Project Setup & Configuration
[TYPE: DevOps/Backend]
> Goal: Working foundation — repo, env, database connection, folder structure
> Depends on: Nothing

- [ ] [CRITICAL] Initialise project and install core dependencies — target: `package.json`
- [ ] Create complete folder structure as defined in blueprint — target: `src/`
- [ ] Create `config/env.ts` — centralised env variable reads — target: `config/env.ts`
- [ ] Create `.env.example` with all variables from ENV.md — target: `.env.example`
- [ ] Configure database connection — target: `config/database.ts`
- [ ] Create `shared/types/common.types.ts` — PaginatedResponse, ApiResponse, ErrorShape — target: `shared/types/`
- [ ] Create `shared/types/index.ts` — re-export all shared types — target: `shared/types/index.ts`
- [ ] Create `shared/constants/app.constants.ts` — app-wide constants — target: `shared/constants/`
- [ ] Update ENV.md with all variables created this phase

**Phase 1 complete when:** Server starts, connects to database, folder structure matches blueprint

---

## Phase 2 — [Feature Name]
[TYPE: Backend]
> Goal: [one sentence]
> Depends on: Phase 1 complete

- [ ] [CRITICAL] Create `features/[name]/[name].types.ts` — define all feature types — target: `features/[name]/`
- [ ] Create `features/[name]/[name].constants.ts` — feature constants — target: `features/[name]/`
- [ ] Create `features/[name]/[name].service.ts` — business logic — target: `features/[name]/`
- [ ] Create `features/[name]/[name].controller.ts` — HTTP handlers — target: `features/[name]/`
- [ ] Create `features/[name]/index.ts` — public exports only — target: `features/[name]/`
- [ ] Add validation for all inputs at controller boundary
- [ ] Add error handling for all service functions
- [ ] Update shared/types if any types are used by multiple features

**Phase 2 complete when:** [specific verifiable condition]

---

## Phase N — [Frontend Feature Name]
[TYPE: Frontend]
⚡ MODEL HINT: Entering frontend work. Consider switching to a UI-focused model.

> Goal: [one sentence]
> Depends on: Backend phases complete

- [ ] [CRITICAL] Create screen component — target: `features/[name]/screens/[ScreenName].tsx`
- [ ] Implement loading state — target: same file
- [ ] Implement empty state — target: same file or `[ScreenName].empty.tsx`
- [ ] Implement error state with user-friendly message — target: same file
- [ ] Implement all form validation with field-level error messages
- [ ] Add confirmation dialog for all destructive actions
- [ ] Add toast/notification feedback for all user actions
- [ ] Verify mobile layout works correctly
- [ ] Update feature index.ts to export new components if needed

**Phase N complete when:** All screens render correctly in all states for all roles

---

## Phase Final — Deployment
[TYPE: DevOps]
⚡ MODEL HINT: Back to infrastructure. Strong reasoning model recommended.

> Goal: Live on production, verified, monitored
> Depends on: All previous phases complete

- [ ] [CRITICAL] Configure Nginx reverse proxy — target: DEPLOY.md + server
- [ ] [CRITICAL] Install and configure SSL certificate
- [ ] Configure PM2 process manager with restart policy
- [ ] Run ./kit deploy (staging) and verify all flows
- [ ] Run smoke test — critical user flows per role
- [ ] Run ./kit deploy --prod after staging verified
- [ ] Update DEPLOY.md with deploy history entry

**Final phase complete when:** Production health check passing, all critical flows verified

---

## Progress Tracker

| Phase | Name | Type | Tasks | Status |
|---|---|---|---|---|
| 1 | Setup | DevOps/Backend | 0/N | Not started |
| 2 | [name] | Backend | 0/N | Not started |
| N | Deployment | DevOps | 0/N | Not started |

---

## Agent Notes
- Read STACK.md before starting any phase
- Read the target file's header before editing it
- One task = one commit. Never batch.
- After each task: fill TASK COMPLETE block, update CHANGELOG.md, commit
- After each phase: notify user, wait for confirmation before next phase
- If unexpected finding: stop, log in KNOWN-ISSUES.md, ask user
- Before defining any type: check shared/types/ and feature types file first

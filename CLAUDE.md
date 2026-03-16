# NurKit — CLAUDE.md
# Claude Code reads this file automatically at every session start.
# This is a copy of .kit/AGENT.md — keep both in sync when AGENT.md is updated.

---

# NurKit Agent — Laws & Rituals
> NurKit Version: 1.0.0
> Read this file fully. Every session. No exceptions.
> For code standards, folder rules, and type rules → read .kit/STANDARDS.md when starting a new file.

---

## SESSION START — PRINT THIS BLOCK BEFORE ANYTHING ELSE

```
🔄 SESSION START
─────────────────────────────────────────────
□ AGENT.md read:                    yes
□ CONTEXT.md read:                  yes
  → Current phase:                  [phase name and number]
  → Last completed:                 [exact last task]
  → Next task:                      [exact next task]
□ STACK.md read:                    yes
  → Stack summary:                  [one line e.g. Node/Express/Postgres/Prisma]
□ Current checklist phase read:     yes
  → Tasks remaining in phase:       [N]
─────────────────────────────────────────────
Ready to continue. Please confirm.
```

Wait for user confirmation. Do not write a single line of code before this.

---

## TASK COMPLETE — PRINT THIS BLOCK AFTER EVERY SINGLE TASK

```
✅ TASK COMPLETE
─────────────────────────────────────────────
Task:              [exact task name from checklist]
─────────────────────────────────────────────
Files created:     [list every new file, or "none"]
Files modified:    [list every changed file, or "none"]
What changed:      [specific description — not "updated the file"]
What was NOT done: [anything skipped and why, or "nothing skipped"]
─────────────────────────────────────────────
□ File header updated (LAST UPDATED, LAST CHANGE, CHANGELOG, CONTAINS)
□ .kit/CHANGELOG.md updated with clear entry
□ Task checked off in active checklist
□ Impact check done
  → Files that import this:         [list, or "none"]
  → Verified none are broken:       yes / no — [explain if no]
□ STACK.md updated                  [yes if new dep added / n/a]
□ ENV.md updated                    [yes if new env var added / n/a]
□ DECISIONS.md updated              [yes if architectural decision / n/a]
□ ASSUMPTIONS.md updated            [yes if assumption made / n/a]
─────────────────────────────────────────────
Git commit message: [feat/fix/refactor: specific description]
─────────────────────────────────────────────
Next task: [exact next task name]
```

Do not proceed to the next task until every field is filled.

---

## EVERY 5 TASKS — PRINT THIS CHECKPOINT

```
🔁 CHECKPOINT — 5 tasks completed
─────────────────────────────────────────────
□ Re-read CONTEXT.md:     yes — still on track / [deviation found]
□ Re-read checklist:      yes — [N] tasks remaining in phase
□ Drift detected:         yes — [describe] / no
─────────────────────────────────────────────
Continuing with: [next task name]
```

Files are truth. Conversation is temporary.

---

## HEADER MISMATCH — STOP AND RESOLVE FIRST

When opening any file, if the header PURPOSE, CONTAINS, or STATUS does not match the actual code:

```
⚠️ HEADER MISMATCH DETECTED
─────────────────────────────────────────────
File:           [filename]
Header says:    [what the header claims]
Code does:      [what the code actually does]
─────────────────────────────────────────────
Which is correct?
A) Header is wrong → update header to match code
B) Code is wrong → move misplaced logic to correct file first
C) File grown too large → flag for extraction in KNOWN-ISSUES.md
─────────────────────────────────────────────
I will not proceed until this is resolved.
```

---

## THE NON-NEGOTIABLE LAWS

### Honesty
- Never say "done" — fill the TASK COMPLETE block
- Never say "updated" — state exactly what changed and in which file
- If you did not do something, state it in "What was NOT done"
- If something is unclear, stop and ask — never guess and proceed

### Before Touching Any File
1. Read the full header — PURPOSE, STATUS, CONTAINS, IMPORTS FROM, IMPORTED BY
2. Check for header mismatch — resolve before anything else
3. Ask: what else imports from this file?
4. Make the smallest possible change that solves the problem

### Never Do These
- Never refactor while fixing a bug
- Never rename things outside scope of current task
- Never add a library not in `.kit/STACK.md` without user confirmation
- Never commit secrets or credentials
- Never skip the file header on a new file
- Never put more than one component or feature in one file
- Never define a type that already exists in `shared/types/` or a feature types file
- Never create a file outside the folder structure in the blueprint
- Never import directly from another feature's internal files — use its index file

### New Files
Every new file gets the full header from `.kit/STANDARDS.md`. No exceptions.

### New Environment Variables
Document in `.kit/ENV.md` immediately — before writing any code that uses it.

### Architectural Decisions
Log in `.kit/DECISIONS.md` with reasoning and alternatives considered.

### Unexpected Findings
Stop. Log in `.kit/KNOWN-ISSUES.md`. Surface to user. Then continue.

### Assumptions
Log in `.kit/ASSUMPTIONS.md` immediately.

### Types — Search Before Defining
1. Check `shared/types/index.ts` — does this type exist?
2. Check the feature's types file — does it exist?
3. Only define if it exists nowhere
4. If it exists → import it, never redefine it

---

## READING ORDER

| File | When |
|---|---|
| CLAUDE.md (this file) | Every session start |
| `.kit/CONTEXT.md` | Every session start |
| `.kit/STACK.md` | Every session start |
| Current checklist phase | Every session start |
| `.kit/STANDARDS.md` | When creating a new file or unsure about style/structure/types |
| Latest blueprint | When task needs architectural understanding |
| `.kit/ASSUMPTIONS.md` | When something feels unclear |
| `.kit/KNOWN-ISSUES.md` | When debugging |
| `.kit/DECISIONS.md` | When considering architectural change |
| `.kit/ENV.md` | When adding or using env variables |
| `.kit/GAPS-TEMPLATE.md` | Only during ./kit gaps |

---

## MODEL HINTS — FOR THE USER, NOT THE AGENT

- `./kit clarify` `./kit plan` `./kit analyze` `./kit gaps` `./kit review` → Most capable model
- `./kit checklist` + backend build phases → Strong reasoning model
- Frontend build phases → UI-focused model (checklist shows ⚡ MODEL HINT)
- `./kit commit` `./kit sync` `./kit status` → Any model

---

## FILE HEADER FORMAT (quick reference)

```
// ============================================
// FILE: [filename]
// PURPOSE: [one sentence]
// STATUS: stable | in-progress | needs-refactor | has-known-issues
// ─────────────────────────────────────────────
// CONTAINS:
//   [functionName]   — [what it does]
// ─────────────────────────────────────────────
// IMPORTS FROM: [list]
// IMPORTED BY:  [list]
// ─────────────────────────────────────────────
// CREATED:      [date]
// LAST UPDATED: [date]
// LAST CHANGE:  [feature/fix name]
// ─────────────────────────────────────────────
// CHANGELOG (last 3):
//   [date]: [what changed]
// ─────────────────────────────────────────────
// ⚠ CRITICAL DEPS: [only if genuinely critical]
// ============================================
```

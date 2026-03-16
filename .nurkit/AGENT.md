# NurKit Agent — Laws & Rituals
> NurKit Version: 1.0.0
> This file is short by design. Read it fully. Every session. No exceptions.
> For code standards, folder rules, and type rules → read STANDARDS.md when starting a new file.

---

## SESSION START — PRINT THIS BLOCK BEFORE ANYTHING ELSE

You must output this exact block at the start of every session.
Do not write a single line of code until all boxes are confirmed.

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
```

### New Project Detection

After printing the SESSION START block, check the Current State in CONTEXT.md.

If phase is "Not started" and last completed is "Nothing yet":

Print this exact message and stop — do not scan files, do not analyze the codebase,
do not suggest options:

```
👋 New project detected. Nothing has been started yet.

To begin, type /clarify — the agent will ask you questions about your idea
and document everything before any planning or code is written.

When you have an existing idea document, type /clarify your-idea-file.md
```

Do not do anything else until the user types a command.

### Existing Project Detection

If phase is NOT "Not started" — continue normally with the SESSION START
block and proceed with the task.

---

## TASK COMPLETE — PRINT THIS BLOCK AFTER EVERY SINGLE TASK

You must output this exact block after completing any task.
Every field must be filled. Empty fields mean the task is not done.

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
□ CHANGELOG.md updated with clear entry
□ Task checked off in active checklist
□ Impact check done
  → Files that import this:         [list, or "none"]
  → Verified none are broken:       yes / no — [explain if no]
□ STACK.md updated                  [yes if new dep added / n/a]
□ ENV.md updated                    [yes if new env var added / n/a]
□ DECISIONS.md updated              [yes if architectural decision made / n/a]
□ ASSUMPTIONS.md updated            [yes if assumption was made / n/a]
─────────────────────────────────────────────
Git commit message: [feat/fix/refactor: specific description]
─────────────────────────────────────────────
Next task: [exact next task name]
```

Do not proceed to the next task until this block is fully filled.

---

## EVERY 5 TASKS — PRINT THIS CHECKPOINT BLOCK

```
🔁 CHECKPOINT — 5 tasks completed
─────────────────────────────────────────────
□ Re-read CONTEXT.md:     yes — still on track / [deviation found]
□ Re-read checklist:      yes — [N] tasks remaining in this phase
□ Any drift detected:     yes — [describe] / no
─────────────────────────────────────────────
Continuing with: [next task name]
```

Files are truth. Conversation is temporary. Always verify against files.

---

## HEADER MISMATCH — STOP AND RESOLVE FIRST

When opening any existing file, if PURPOSE, CONTAINS, or STATUS in the header
does not match the actual code inside the file:

```
⚠️ HEADER MISMATCH DETECTED
─────────────────────────────────────────────
File:           [filename]
Header says:    [what the header claims]
Code does:      [what the code actually does]
─────────────────────────────────────────────
Which is correct?
A) Header is wrong → I will update the header to match the code
B) Code is wrong → I will move misplaced logic to the correct file first
C) File grown too large → I will flag for extraction in KNOWN-ISSUES.md
─────────────────────────────────────────────
I will not proceed with any task until this is resolved.
```

Never work on a task while a header mismatch exists.
A wrong header means the map is wrong. Every decision built on a wrong map is wrong.

---

## THE NON-NEGOTIABLE LAWS

### Honesty
- Never say "done" — fill the TASK COMPLETE block instead
- Never say "updated" — state exactly what changed and in which file
- Never say "handled" — show the exact logic that handles it
- If you did not do something, state it explicitly in "What was NOT done"
- If something is unclear, stop and ask — never guess and proceed

### Before Touching Any Existing File
1. Read the file header fully — PURPOSE, STATUS, CONTAINS, IMPORTS FROM, IMPORTED BY
2. Check for header mismatch — resolve before doing anything else
3. Ask: what else imports from this file?
4. Make the smallest possible change that solves the problem
5. After the change, fill the TASK COMPLETE block completely

### Never Do These
- Never refactor while fixing a bug
- Never improve unrelated code while implementing a feature
- Never rename things outside the scope of the current task
- Never add a library not in STACK.md without flagging user first and getting confirmation
- Never commit secrets, API keys, or credentials
- Never skip the file header on a new file
- Never put more than one component or feature in one file
- Never define a type that already exists in shared/types/ or in a feature types file
- Never guess an architectural decision — check the latest blueprint first
- Never create a file outside the folder structure defined in the blueprint

### New Files — Always Start With the Header
See STANDARDS.md for the exact header format.
Every new file gets the full header. No exceptions. Ever.

### New Environment Variables
Document in ENV.md immediately when added. Before writing any code that uses it.

### Architectural Decisions
Log in DECISIONS.md with reasoning and what alternatives were considered.

### Unexpected Findings During Build
Stop. Describe what was found. Log in KNOWN-ISSUES.md. Ask user how to proceed.

### Assumptions
Log in ASSUMPTIONS.md immediately. Include what breaks if the assumption is wrong.

### Types — Search Before Defining
Before writing any new type definition:
1. Check shared/types/index.ts — does this type already exist?
2. Check the current feature's types file — does it exist there?
3. Only define it if it exists nowhere in the codebase
4. If it exists → import it, never redefine it
See STANDARDS.md for full type ownership rules.

---

## READING ORDER

| File | When to read |
|---|---|
| AGENT.md (this file) | Every session start — fully |
| CONTEXT.md | Every session start |
| STACK.md | Every session start |
| Current checklist phase only | Every session start |
| STANDARDS.md | When creating a new file, or unsure about style/structure/types |
| Latest blueprint | When a task needs architectural understanding |
| ASSUMPTIONS.md | When something feels unclear about the plan |
| KNOWN-ISSUES.md | When debugging or reviewing |
| DECISIONS.md | When considering any architectural change |
| ENV.md | When adding or using environment variables |
| GAPS-TEMPLATE.md | Only during ./kit gaps |

---

## MODEL HINTS — FOR THE USER, NOT THE AGENT

The agent cannot switch models. These are reminders for you.

- `./kit clarify` `./kit plan` `./kit analyze` `./kit gaps` `./kit review` → Most capable model
- `./kit checklist` `./kit build` backend phases → Strong reasoning model
- `./kit build` frontend phases → UI-focused model (checklist will show ⚡ MODEL HINT)
- `./kit commit` `./kit sync` `./kit status` → Any model, even cheapest

---

## DEFINITION OF DONE — QUICK REFERENCE

Task done: code written + header updated + TASK COMPLETE block filled + committed.
Phase done: all tasks done + full phase re-read + user confirmed before next phase.
Full reference: DEFINITION-OF-DONE.md

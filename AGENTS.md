# NurKit — OpenCode Agent Rules
> This file is read by OpenCode automatically at every session start.
> Claude Code users: see CLAUDE.md instead.
> Full standards reference: @nurkit/STANDARDS.md (loaded when needed)

---

## SESSION START — PRINT THIS BLOCK BEFORE ANYTHING ELSE

```
🔄 SESSION START
─────────────────────────────────────────────
□ AGENTS.md read:                   yes
□ CONTEXT.md read:                  yes
  → Current phase:                  [phase name and number]
  → Last completed:                 [exact last task]
  → Next task:                      [exact next task]
□ STACK.md read:                    yes
  → Stack summary:                  [one line]
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
□ .nurkit/CHANGELOG.md updated with clear entry
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

When opening any file, if PURPOSE, CONTAINS, or STATUS in the header
does not match the actual code:

```
⚠️ HEADER MISMATCH DETECTED
─────────────────────────────────────────────
File:           [filename]
Header says:    [what the header claims]
Code does:      [what the code actually does]
─────────────────────────────────────────────
A) Header is wrong → update header to match code
B) Code is wrong → move misplaced logic to correct file first
C) File grown too large → flag for extraction in KNOWN-ISSUES.md
─────────────────────────────────────────────
I will not proceed until this is resolved.
```

---

## EXTERNAL FILE REFERENCES

Load these files only when the task actually needs them — do not load all at once:

- Code standards and folder rules: @nurkit/STANDARDS.md
- Gaps audit master checklist: @nurkit/GAPS-TEMPLATE.md
- Definition of done: @nurkit/DEFINITION-OF-DONE.md
- Full architecture reference: read the latest file in .nurkit/blueprints/
- Current task list: read the latest file in .nurkit/checklists/
- Known issues: @nurkit/KNOWN-ISSUES.md
- Architectural decisions: @nurkit/DECISIONS.md
- Environment variables: @nurkit/ENV.md
- Assumptions log: @nurkit/ASSUMPTIONS.md
- Deploy configuration: @nurkit/DEPLOY.md

---

## THE NON-NEGOTIABLE LAWS

### Honesty
- Never say "done" — fill the TASK COMPLETE block instead
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
- Never add a library not in .nurkit/STACK.md without user confirmation
- Never commit secrets or credentials
- Never skip the file header on a new file
- Never put more than one component or feature in one file
- Never define a type that already exists in shared/types/ or a feature types file
- Never create a file outside the folder structure defined in the blueprint
- Never import directly from another feature's internal files — use its index file

### New Files
Every new file gets the full header. See @nurkit/STANDARDS.md for exact format.

### New Environment Variables
Document in .nurkit/ENV.md immediately — before writing any code that uses it.

### Architectural Decisions
Log in .nurkit/DECISIONS.md with reasoning and alternatives considered.

### Unexpected Findings
Stop. Log in .nurkit/KNOWN-ISSUES.md. Surface to user. Then continue.

### Assumptions
Log in .nurkit/ASSUMPTIONS.md immediately.

### Types — Search Before Defining
1. Check shared/types/index.ts — does this type exist?
2. Check the feature's types file — does it exist?
3. Only define if it exists nowhere
4. If it exists → import it, never redefine it

---

## MODEL HINTS — FOR THE USER, NOT THE AGENT

The agent cannot switch models. These are reminders for you.

- /clarify /plan /analyze /gaps /review → Use your most capable model
- /checklist /build backend phases → Strong reasoning model
- /build frontend phases → UI-focused model (you will see ⚡ MODEL HINT)
- /commit /sync /status → Any model

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

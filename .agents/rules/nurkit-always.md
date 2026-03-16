---
activation: always
---

# NurKit — Always Active Rules

You are working inside a NurKit-managed project.
NurKit is a structured AI development system. All project memory,
plans, and state live in the `.nurkit/` folder.

## On Every Session Start

Read these files in this exact order before doing anything else:
1. `.nurkit/AGENT.md` — your laws and session rituals
2. `.nurkit/CONTEXT.md` — current state and last session summary
3. `.nurkit/STACK.md` — tech stack in use
4. Current phase only from the latest file in `.nurkit/checklists/`

Then print this block:

```
🔄 SESSION START
─────────────────────────────────────────────
□ AGENT.md read:                    yes
□ CONTEXT.md read:                  yes
  → Current phase:                  [phase name and number]
  → Last completed:                 [exact last task]
  → Next task:                      [exact next task]
□ STACK.md read:                    yes
  → Stack summary:                  [one line]
□ Current checklist phase read:     yes
  → Tasks remaining in phase:       [N]
─────────────────────────────────────────────
Ready to continue. Please confirm.
```

Wait for user confirmation before doing anything.

## After Every Task

Print this block — every field must be filled:

```
✅ TASK COMPLETE
─────────────────────────────────────────────
Task:              [exact task name]
Files created:     [list, or "none"]
Files modified:    [list, or "none"]
What changed:      [specific description]
What was NOT done: [anything skipped, or "nothing skipped"]
─────────────────────────────────────────────
□ File header updated
□ .nurkit/CHANGELOG.md updated
□ Task checked off in checklist
□ Impact check done
  → Files that import this:         [list, or "none"]
  → Verified none are broken:       yes / no
□ STACK.md updated                  [yes if new dep / n/a]
□ ENV.md updated                    [yes if new env var / n/a]
□ DECISIONS.md updated              [yes if decision made / n/a]
□ ASSUMPTIONS.md updated            [yes if assumption made / n/a]
─────────────────────────────────────────────
Git commit message: [feat/fix/refactor: description]
─────────────────────────────────────────────
Next task: [exact next task name]
```

## Core Laws

- Never say "done" — fill the TASK COMPLETE block
- Never define a type that already exists in shared/types/ or a feature types file
- Never add a library not in .nurkit/STACK.md without user confirmation
- Never create a file outside the folder structure in the blueprint
- Never work on a file with a header mismatch — resolve it first
- Files are truth. Conversation is temporary.
- Read .nurkit/STANDARDS.md when creating any new file

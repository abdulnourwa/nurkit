# NurKit — /kit sync prompt
> Context: {{CONTEXT}}
> Checklist: {{CHECKLIST}}

---

Update CONTEXT.md with a complete session summary.
Keep the current state section at the top (overwrite it).
Append the session summary to the session history at the bottom — never delete old entries.

```markdown
# NurKit Context
## Project: [name]
## Scope: [full-app / single-feature]
## NurKit Version: 1.0.0

---

## Current State
- Phase: [current phase name and number]
- Last completed: [exact last task — be specific]
- Next action: [exact next task or command]
- Active checklist: [filename]
- Active blueprint: [filename]

## Open Items
- [anything flagged, unresolved, or needing attention]

---

## Session History

### [datetime] — Session summary
- Completed: [list of tasks completed this session]
- Decisions made: [any architectural or product decisions]
- Files modified: [list]
- New types added: [list with location]
- Issues found: [anything logged in KNOWN-ISSUES.md]
- Next session starts at: [exact task]

[previous session entries below — never delete them]
```

After writing: "Session saved. Context updated. Safe to close. Next session continues at [exact task]."

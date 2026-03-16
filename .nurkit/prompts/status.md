# NurKit — /kit status prompt
> Context: {{CONTEXT}}
> Checklist: {{CHECKLIST}}

---

Provide a clear project status report. Be factual. Only state what is confirmed done.

```
## NurKit Status — [datetime]
### Project: [name]
### Current Phase: [name and number]

---
### Progress
[Phase bars — use completed/total tasks]

Phase 1 — [name] [TYPE]    ████████░░  8/10  [IN PROGRESS]
Phase 2 — [name] [TYPE]    ██████████  6/6   [COMPLETE]
Phase 3 — [name] [TYPE]    ░░░░░░░░░░  0/12  [NOT STARTED]

Overall: [N]/[total] tasks complete ([%])

---
### Last Completed
[Most recent checked-off task]

### Next Task
[Exact next uncompleted task with file target]

### Open Issues
[From KNOWN-ISSUES.md — open items only]

### Recent Changes (last 5 changelog entries)
[From CHANGELOG.md]

### Types Health
[Any type ownership issues detected — or "Type ownership map intact"]
```

---
activation: glob
glob: "**/*.ts,**/*.tsx,**/*.js,**/*.jsx,**/*.py,**/*.go,**/*.php"
---

# NurKit — Code Standards

When creating or editing any code file, follow these rules.
Full reference: `.nurkit/STANDARDS.md`

## File Header (mandatory on every file)

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
// ============================================
```

## Header Mismatch

If the header does not match the actual code, stop and print:

```
⚠️ HEADER MISMATCH DETECTED
File:        [filename]
Header says: [what header claims]
Code does:   [what code actually does]
Resolve before proceeding.
```

## Structure Rules

- One file, one responsibility
- Feature-based folders — not type-based
- Features never import directly from each other — use shared/
- Config reads env variables in one place only
- Validation happens at the boundary only — never inside services
- Check shared/types/ and feature types file before defining any new type

## Code Style

- Names are phrases not abbreviations
- Booleans: is, has, can, should prefix
- Blank line between logical steps — not between every line
- Comments explain WHY not what
- No magic numbers or strings — always named constants
- No nested ternaries

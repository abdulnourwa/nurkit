# NurKit — /kit review prompt
> Context: {{CONTEXT}}
> Blueprint: {{BLUEPRINT}}
> Stack: {{STACK}}
> Checklist: {{CHECKLIST}}

---

You are doing a drift analysis — comparing what was planned against what was actually built.

## Your Process

### Step 1 — Review Feature Completeness
For each completed phase, check actual files against blueprint:
- Does the implementation match blueprint specifications?
- Are all edge cases handled as defined?
- Are all roles and permissions correctly implemented?
- Are all UI states present (empty, loading, error, populated)?

### Step 2 — Review Code Quality
- Every file has a header comment block?
- Headers match actual code (no mismatches)?
- STANDARDS.md principles followed?
- No files doing more than one job?
- No hardcoded values that should be env variables?
- Feature folders followed correctly?
- No cross-feature imports?

### Step 3 — Review Type Integrity
- Are all types in the Type Ownership Map in the correct locations?
- Are any types redefined in multiple places?
- Are shared types correctly in shared/types/?

### Step 4 — Review Security
- Every protected endpoint authenticated and authorised?
- All inputs validated server-side?
- No obvious security holes?

### Step 5 — Report

```
## Review Complete

### Drift (planned but not implemented):
- [feature/detail]: [what is missing]

### Quality issues:
- [file/area]: [what needs improvement]

### Type integrity issues:
- [type]: [problem and fix]

### Security concerns:
- [concern]: [recommendation]

### Recommended actions:
1. [action]
```

Log all findings in KNOWN-ISSUES.md.

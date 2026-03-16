# DEFINITION OF DONE — [Project Name]
> This file defines what "done" means at every level.
> Agent: verify every item before marking anything complete.

---

## A Task Is Done When:

- [ ] Code is written and saved to the correct file
- [ ] File follows the one-responsibility rule
- [ ] File header created (new file) or updated (existing file):
  - [ ] LAST UPDATED updated to today
  - [ ] LAST CHANGE updated to current feature/fix name
  - [ ] CHANGELOG line added (last 3 only — remove oldest)
  - [ ] CONTAINS updated if functions added/removed/changed
  - [ ] STATUS updated if file health changed
- [ ] No hardcoded values — config and secrets in env variables
- [ ] No library introduced not in STACK.md
- [ ] No type redefined that already exists in shared/types/ or feature types file
- [ ] TASK COMPLETE block printed in chat with all fields filled
- [ ] Impact check done — related files verified as unbroken
- [ ] CHANGELOG.md updated with clear entry
- [ ] Task checked off in active checklist
- [ ] Git commit made with meaningful conventional message

---

## A Feature Is Done When:

- [ ] All tasks done by the above definition
- [ ] Happy path works end to end
- [ ] All role permissions correctly enforced
- [ ] Empty state implemented for every list or data view
- [ ] Loading state implemented for every async operation
- [ ] Error state implemented with user-friendly message
- [ ] Destructive actions have confirmation dialogs
- [ ] All form inputs validated server-side
- [ ] User receives feedback for every action
- [ ] Feature works on mobile viewport
- [ ] No console errors or warnings in browser
- [ ] All API endpoints return correct status codes
- [ ] Types are in the correct location per Type Ownership Map

---

## A Phase Is Done When:

- [ ] All features done by the above definition
- [ ] Agent re-read the full phase checklist — nothing skipped
- [ ] Any issues found are logged in KNOWN-ISSUES.md
- [ ] CHANGELOG.md reflects all work done in this phase
- [ ] Version number bumped (minor bump for completed feature phase)
- [ ] User notified and confirmed before next phase starts

---

## A Deployment Is Done When:

- [ ] All phases complete by the above definition
- [ ] All env variables set on server (verified against ENV.md)
- [ ] Database migrations ran successfully
- [ ] Health check endpoint returns 200
- [ ] SSL certificate active and valid
- [ ] PM2 process running and set to restart on crash
- [ ] Smoke test of critical user flows completed per role
- [ ] Deploy history entry added to DEPLOY.md
- [ ] No Critical items open in KNOWN-ISSUES.md

# NurKit — /kit deploy prompt
> Context: {{CONTEXT}}

---

Guide a VPS deployment. Read DEPLOY.md for project-specific configuration.

## Pre-Deploy Checklist
- [ ] All tests passing (if test suite exists)
- [ ] No uncommitted changes
- [ ] Pushed to GitHub successfully
- [ ] ENV variables on server match ENV.md (verify manually — never log secrets)
- [ ] STACK.md dependencies match what is installed on server
- [ ] Database migrations ready if schema changed
- [ ] shared/types verified — no type mismatches between frontend and backend

## Staging Deploy Steps
1. SSH into staging VPS
2. Navigate to project directory
3. Pull latest: `git pull origin main`
4. Install/update dependencies
5. Run database migrations if applicable
6. Build if build step needed
7. Restart process manager (PM2 or equivalent)
8. Verify health check endpoint responds
9. Quick smoke test of most critical user flow
10. Report: "Staging deploy complete. Verify at [URL] before deploying to production."

## Production Deploy (only after staging verified)
Same steps targeting production VPS.
Confirm before executing: "About to deploy to PRODUCTION. Staging verified. Proceeding."

## After Successful Deploy
Update DEPLOY.md:
```
### Deploy — [datetime]
- Target: [staging / production]
- Commit: [git commit hash]
- Status: Success
- Notes: [anything notable]
```

## If Deploy Fails
1. Check process manager logs for the error
2. If error in new code: `git revert HEAD` and redeploy
3. If infrastructure error: check Nginx, process manager, port
4. Log failure in DEPLOY.md
5. Report exact error with recommended fix

# NurKit — Deploy

Deploy to staging. Pass --prod as argument for production.

## Steps

1. Read `.nurkit/prompts/deploy.md` completely
2. Read `.nurkit/DEPLOY.md` for server configuration
3. If argument is --prod: tell user "About to deploy to PRODUCTION" and require
   them to type "yes" before proceeding
4. Otherwise target staging
5. Run pre-deploy checklist
6. Execute deploy steps from DEPLOY.md
7. After successful deploy, append entry to Deploy History table in `.nurkit/DEPLOY.md`
8. Confirm: "Deploy complete. [target] is live."

---
description: Deploy to staging. Use --prod argument for production.
model: anthropic/claude-sonnet-4-6
---

Read .kit/prompts/deploy.md and follow it exactly.
Read .kit/DEPLOY.md for server configuration.
If $ARGUMENTS contains "--prod" then target production — require the user to confirm by typing "yes" before proceeding.
Otherwise target staging.
After successful deploy, append a new entry to the Deploy History table in .kit/DEPLOY.md

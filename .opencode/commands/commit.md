---
description: Generate a meaningful commit message and update CHANGELOG.md. Any model works.
---

Read .kit/prompts/commit.md and follow it exactly.
Generate a conventional commit message for the current uncommitted changes.
Append the message as a new entry in .kit/CHANGELOG.md with today's date.
Then run: git add -A && git commit -m "[the generated message]"

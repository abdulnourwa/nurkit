# NurKit — Commit

Generate a meaningful commit message and update CHANGELOG.md.

## Steps

1. Read `.nurkit/prompts/commit.md` completely
2. Review current uncommitted changes
3. Generate a conventional commit message
4. Append a new entry to `.nurkit/CHANGELOG.md` with today's date
5. Run: git add -A && git commit -m "[generated message]"
6. Confirm: "Committed: [message]"

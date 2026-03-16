# NurKit — /kit commit prompt
> Context: {{CONTEXT}}

---

Generate a meaningful git commit message for the current changes.

Rules:
- Conventional commit format: `type: description`
- Types: `feat`, `fix`, `refactor`, `docs`, `style`, `test`, `chore`, `deploy`
- Lowercase, present tense, under 72 characters
- If multiple changes, use most significant as main, list others as bullets

Examples:
- `feat: add JWT refresh token rotation in auth service`
- `fix: prevent double-submit on payment form`
- `refactor: extract email validation to shared utils`
- `chore: update ENV.md with new SMTP variables`
- `feat: add shared PaginatedResponse type to shared/types`

Output only the commit message. Nothing else.

# NurKit Gaps Template
> This file is never modified. It is the master template.
> Every ./kit gaps run copies this and fills it as a new dated file in gaps/
> Agent: work through every section. Do not skip. Do not assume.

---

# Gaps Audit — [PROJECT NAME] — [DATE]
> Blueprint reviewed: [blueprint filename]
> Feature scope: [full project / feature name]

---

## SECTION 1 — UI Completeness

### Empty States
- [ ] Every list view — what shows when there are 0 records?
- [ ] Every dashboard — what shows for a brand new user?
- [ ] Every search — what shows when no results match?
- [ ] Every feed or activity log — what shows when history is empty?

### Loading States
- [ ] Every async data fetch has a visible loading indicator
- [ ] Every form submission has a loading/disabled state
- [ ] Every file upload shows progress
- [ ] Page-level vs component-level loading defined

### Error States
- [ ] Every API call has a user-friendly error message
- [ ] Network failure — what does the user see?
- [ ] Server error (500) — what does the user see?
- [ ] Session expired — what happens, where does user go?

### Success & Feedback
- [ ] Every user action has confirmation feedback (toast, notification, redirect)
- [ ] Every destructive action has a confirmation dialog
- [ ] Every form has clear success feedback
- [ ] Every async operation resolves visibly

### Forms
- [ ] Every input field has validation rules (type, required, min, max, format)
- [ ] Validation fires on submit AND on blur
- [ ] Every validation error has a specific user-friendly message
- [ ] Forms disabled during submission
- [ ] Forms reset/redirect correctly after success
- [ ] Double-submit prevented

### Navigation & Flow
- [ ] First screen each role sees after login defined
- [ ] After every major action — where does user go?
- [ ] Browser back button behaviour defined
- [ ] Unauthenticated user hitting protected route — what happens?
- [ ] Lower role hitting higher role route — what happens?
- [ ] 404 page defined
- [ ] 403 page defined

### Mobile & Responsive
- [ ] Every screen defined for mobile
- [ ] Navigation behaviour on mobile
- [ ] Tables and data-heavy views on small screens
- [ ] Touch targets minimum 44x44px
- [ ] Forms usable on mobile keyboard

---

## SECTION 2 — Role & Permission Completeness

For each role:
- [ ] What does [ROLE] see on the dashboard?
- [ ] What can [ROLE] create / read / edit / delete?
- [ ] What is [ROLE] explicitly NOT allowed to do?
- [ ] What happens when [ROLE] tries something forbidden?
- [ ] If role is changed mid-session — when does it take effect?
- [ ] If account is suspended — what happens to active session?
- [ ] Can a user have multiple roles? If yes — conflict resolution defined?

---

## SECTION 3 — Auth & Session Edge Cases

- [ ] Wrong password — response and lockout behaviour defined
- [ ] Too many failed attempts — rate limit and lockout defined
- [ ] Password reset flow — complete end to end
- [ ] Email verification (if applicable) — complete end to end
- [ ] JWT access token expiry mid-session — what happens?
- [ ] Refresh token rotation — old token invalidated after use?
- [ ] Remember me / persistent login — defined?
- [ ] Logout — all tokens invalidated server-side?
- [ ] Concurrent sessions from multiple devices — allowed or not?
- [ ] Password change — other sessions invalidated?

---

## SECTION 4 — Data & Business Logic Edge Cases

- [ ] Zero records — every query handles empty result
- [ ] Large dataset — pagination defined, no unbounded queries
- [ ] Concurrent edits — two users editing same record simultaneously
- [ ] Deleted dependency — cascade, restrict, or nullify defined for every relationship
- [ ] Numeric extremes — zero, negative, very large, decimal handling
- [ ] Currency — precision, rounding, display format defined
- [ ] Dates/times — timezone handling and storage format defined (UTC?)
- [ ] Text extremes — empty string, very long string, special characters, emoji
- [ ] File uploads — max size, allowed types, rejection handling
- [ ] Optional vs required — every field explicitly defined

---

## SECTION 5 — Spam & Abuse

- [ ] Form submission spam — rate limit per user/IP
- [ ] Button double-click / rapid resubmit — prevented
- [ ] API endpoint abuse — rate limiting per endpoint
- [ ] Search/filter abuse — expensive queries debounced or limited
- [ ] File upload abuse — size and frequency limits
- [ ] Account creation abuse — CAPTCHA or email verification?
- [ ] Recovery path defined (auto-unblock after time, manual review?)

---

## SECTION 6 — Notifications & Communication

- [ ] What events trigger a notification?
- [ ] Channels defined (in-app, email, push, SMS)?
- [ ] Per-role notification rules defined?
- [ ] User can opt out of any notification?
- [ ] Delivery failure handling defined?
- [ ] Every email type has subject and content defined?

---

## SECTION 7 — Performance & Scale

- [ ] Expected user count defined in VISION.md
- [ ] Database indexes identified for frequently queried fields
- [ ] N+1 query problems reviewed for all list endpoints
- [ ] Slow endpoints identified with mitigation noted
- [ ] File/image storage strategy defined
- [ ] CDN considered for static assets?
- [ ] Background jobs defined for slow operations?

---

## SECTION 8 — Security

- [ ] All inputs validated server-side
- [ ] All queries parameterised
- [ ] Auth checked on every protected endpoint
- [ ] Sensitive data not returned unless needed
- [ ] Sensitive data not logged
- [ ] HTTP headers hardened
- [ ] HTTPS enforced in production
- [ ] Secrets in environment variables — none hardcoded
- [ ] File uploads validated for malicious content
- [ ] Admin routes extra-protected?

---

## SECTION 9 — Deployment & Infrastructure

- [ ] All env variables documented in ENV.md
- [ ] Staging separate from production
- [ ] Database backup strategy defined
- [ ] Process manager configured (restart on crash)
- [ ] Reverse proxy configured
- [ ] SSL certificate — provider and renewal
- [ ] Rollback procedure documented
- [ ] Health check endpoint defined
- [ ] Error monitoring defined
- [ ] VPS down recovery plan?

---

## SECTION 10 — Onboarding & First-Run

- [ ] First login experience defined per role
- [ ] Onboarding flow defined?
- [ ] Each role's zero-data state defined?
- [ ] Seed or demo data needed?
- [ ] First admin/super admin account creation defined?
- [ ] Setup or configuration step before app is usable?

---

## SECTION 11 — Types & Structure

- [ ] Type Ownership Map exists in blueprint?
- [ ] All types used in feature specs listed in ownership map?
- [ ] Types used by multiple features placed in shared/types/?
- [ ] No type defined in more than one location?
- [ ] shared/types/index.ts exports all shared types through single door?
- [ ] Every feature has its own types file listed in folder structure?
- [ ] Every feature has its own constants file listed in folder structure?
- [ ] Every feature has an index file (public door)?
- [ ] No circular imports between features?
- [ ] Config reads env vars in one place only?

---

## Gaps Found — Summary

| # | Gap Found | Severity | Resolution Added to Blueprint |
|---|---|---|---|
| 1 | | | |

---

## Sign-Off
- [ ] All 11 sections reviewed
- [ ] All gaps logged in summary table
- [ ] Blueprint updated with gap resolutions
- [ ] Type ownership map updated if needed
- [ ] User notified: "Gaps complete. Blueprint updated. Run ./kit checklist"

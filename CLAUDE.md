# CLAUDE.md — whirl-sites

## Overview
Marketing/legal web presence for **Whirl** (see sibling repo `../whirl`), the parent-facing "what should we do today?" app. This repo hosts:
- Public marketing/landing page(s) for the app.
- Legal docs: Terms of Service, Privacy Policy (and any other required policy pages).
- Any other static app-adjacent pages (support, account deletion instructions, etc. as needed).

This is **not** the app itself — no product features, no auth, no database. Content-first, static-first.

## Status
- Repo just initialized (LICENSE + `.gitignore` only, no site code yet).
- **Urgent driver:** the iOS app (`../whirl`) ships with placeholder legal URLs hardcoded in `Configuration.plist`:
  - `TERMS_OF_SERVICE_URL` → `https://whirl.app/terms`
  - `PRIVACY_POLICY_URL` → `https://whirl.app/privacy`
  - `PRIVACY_POLICY_VERSION` → `2026-07-05`
  - This is a tracked **ship blocker** in the whirl repo (TODO(R13)): these must resolve to real, live legal docs before App Store submission. Whatever routes/paths this site ships must match those exact URLs (or the app config must be updated to match — coordinate before changing either side).
- Privacy Policy content must reflect what the app actually does: camera/photo access (barcode scan + photo override), location permission (primed in onboarding, not yet consuming any feature until Phase 3), Supabase-backed auth + storage, child age stored in months (no DOB) for PDPA/COPPA/GDPR-K alignment. Don't draft generic boilerplate that contradicts actual data practices — check `../whirl/CLAUDE.md` and `../whirl/concept/USER_FEATURE.md` for what's actually collected before writing policy text.

## Locked Decisions
- Static-first site (no backend/database needed for this repo's scope).
- Content must stay factually in sync with the actual app's data practices — legal text is not boilerplate, it's a compliance surface for a children-adjacent app (Singapore PDPA / COPPA / GDPR-K).
- Domain target: `whirl.app` (per the URLs already baked into the iOS app config).

## Tech Stack
TBD — not yet decided. Route through `web-developer` agent for framework choice (likely static-first React/Next.js or Astro per that agent's default stance) when site work begins.

## Working With This Project
- This repo is separate from `../whirl` (the app). Cross-reference `../whirl/CLAUDE.md` for product context, but don't duplicate app implementation details here.
- Any change to the legal-doc URL paths/structure must be checked against `../whirl/ios/app/whirl/whirl/Config/Configuration.plist` (`TERMS_OF_SERVICE_URL`, `PRIVACY_POLICY_URL`) — keep them in sync, and bump `PRIVACY_POLICY_VERSION` in that plist whenever Privacy Policy content materially changes.
- Non-trivial site/feature work → route through the `sdd` skill pipeline with `web-developer`. Trivial/mechanical edits (copy tweaks, typos) can be done directly.

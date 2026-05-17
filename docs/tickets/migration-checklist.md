# Ticket: Migrate Signal 1.0 assets to Signal 2.0

**Ticket ID:** SIGNAL2-001
**Sprint:** Sprint 2.1 (Weeks 2–3, 25 May – 7 June 2026)
**Owner:** Chris Cross
**Status:** Open
**Priority:** High. Blocks subsequent Phase 2 sprints.
**Created:** 17 May 2026
**Repo:** [DevonTallMan/Signal_2.0](https://github.com/DevonTallMan/Signal_2.0)

---

## Context

Signal 2.0 is a fresh repository replacing the old Signal project. This ticket covers a structured migration of components and config from the previous codebase while explicitly leaving behind the AI-generated body content and any deprecated infrastructure.

The Computer Misuse Act page rebuild is the POC scope. All other topics are out of scope.

## Blockers

- [ ] **Deployment URL decision.** Resolve before this ticket can complete, because the privacy notice (Sprint 2 of Phase 1) references the production URL.
    - Option A: random Cloudflare subdomain (e.g. `signal-2-xyz.pages.dev`)
    - Option B: custom subdomain on an owned domain (e.g. `dev.signal.yourdomain.com`)

## Acceptance criteria

- Signal 2.0 repo contains a working Astro + Cloudflare Pages scaffold and deploys cleanly to the chosen URL
- Cyberpunk visual identity preserved on a fresh layout
- Computer Misuse Act page exists as a tile-grid structural shell with no body content
- Old AI-generated content is not present anywhere in the new repo
- Old Firebase or Firestore code is not present
- Old Signal repo is archived on GitHub with README pointing to Signal 2.0
- Old deployment URL has a documented deprecation plan

## Tasks

### Take cleanly from the old repo

- [ ] Astro project config (`astro.config.mjs`, `tsconfig.json`, `package.json`)
- [ ] Audit and prune `package.json` dependencies for current relevance
- [ ] Cloudflare Pages deployment config (`wrangler.toml` if present)
- [ ] `.gitignore` and base README structure
- [ ] Environment variable templates (`.env.example` or equivalent)

### Take with review and refactor

- [ ] Cyberpunk styling: CSS variables, font imports, colour tokens
- [ ] Base layout component, with old metadata and `<head>` tags stripped
- [ ] Site nav and footer, with all links verified or updated
- [ ] Computer Misuse Act page tile-grid structure only (no body content)
- [ ] Tile and card components used on the topic page

### Confirm NOT migrated (verification step)

- [ ] AI-generated body content from the old Computer Misuse page is absent
- [ ] All other topic pages (Business & Professional Context, the rest of Paper 1) are absent
- [ ] Firebase or auth code from the old repo is absent
- [ ] Old Firestore security rules are absent
- [ ] Abandoned experiments or unused components are absent

### Cutover housekeeping

- [ ] Archive the old Signal repo on GitHub (Settings → Archive this repository)
- [ ] Update the old repo's README to point to Signal 2.0 with the transition date
- [ ] Document deprecation timing for `signal-dev-3bx.pages.dev` (do not take it down before Signal 2.0 is on a stable URL)
- [ ] Update inbound links: client communications, portfolio, anywhere else the old URL is shared

## Notes and risks

The temptation will be to bulk-copy the old codebase. Resist it. The point of starting fresh is to leave the AI content and the historic Firestore rules behind. Cherry-pick deliberately.

If a component has no obvious purpose within Signal 2.0's scope (one topic page, auth and per-user state, exam grading, GDPR flows), default to not migrating. It can always be copied later if a real need surfaces.

The old Cloudflare Pages deployment must stay live until Signal 2.0 is on a working URL. Do not kill the old environment before the new one is verified.

## Related artefacts

- [Project Charter](./project-charter.md)
- Sprint 2.1 plan: Foundations
- Decision log entry (to be created): "Signal 2.0 as fresh repo, 17 May 2026"
- Risk register entry (to be created): Phase 2 dependency on completed migration

## Definition of Done

- All "take cleanly" and "take with review" items checked
- All "confirm not migrated" items verified
- Cutover housekeeping items checked
- Signal 2.0 deploys successfully to its chosen Cloudflare Pages URL
- Computer Misuse Act page renders as an empty tile grid with the cyberpunk styling intact
- Old Signal repo archived, README updated

---

## Change log

| Date | Author | Change |
|---|---|---|
| 17 May 2026 | PM | Initial ticket created |

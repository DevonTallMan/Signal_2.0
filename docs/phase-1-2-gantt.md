# Detailed Gantt: Phase 1 and Phase 2

**Project:** Signal Computer Misuse POC (Signal 2.0)
**Scope:** Phase 1 (Legal and admin) and Phase 2 (Auth and state)
**Duration:** 18 May 2026 to 19 July 2026 (9 weeks)
**Capacity assumption:** 1.5 effort days per week
**Last updated:** 17 May 2026
**Maintained by:** Project Manager

---

## How to read this chart

Tasks are grouped by sprint. Critical-path items (those that block downstream work or compliance) are marked `crit` and render in a different colour on GitHub. Milestones (sprint retros, go/no-go gates) appear as diamond markers. Dependencies use `after` where the chain is strict; flexible tasks use absolute dates within their sprint window.

Phase 1 runs four weekly sprints. Phase 2 runs five sprints of varying length, starting Week 2 and continuing parallel to Phase 1.

The diagram renders natively on GitHub. If viewing this file in a non-Mermaid editor, the diagram appears as code until rendered.

---

## Schedule

```mermaid
gantt
    title Signal 2.0 - Phase 1 and Phase 2 Detailed Schedule
    dateFormat YYYY-MM-DD
    axisFormat %d %b
    tickInterval 1week

    section P1 Sprint 1: Open channels
    Register with ICO                       :p1s1a, 2026-05-18, 1d
    Email college DPO                       :p1s1b, 2026-05-18, 1d
    Email safeguarding lead                 :p1s1c, 2026-05-18, 1d
    Contract clause check                   :p1s1d, 2026-05-19, 1d
    Document age policy                     :p1s1e, 2026-05-20, 2d
    Sprint 1 retro and go/no-go gate        :milestone, p1s1f, 2026-05-22, 0d

    section P1 Sprint 2: Draft notice
    Data inventory                          :p1s2a, 2026-05-25, 1d
    Privacy notice template setup           :p1s2b, 2026-05-25, 1d
    Privacy notice v0.1 draft               :crit, p1s2c, after p1s2b, 2d
    Consent flow wireframe under-16         :p1s2d, 2026-05-28, 1d
    Consent flow wireframe 16-17            :p1s2e, 2026-05-28, 1d
    Consent flow wireframe 18+              :p1s2f, 2026-05-29, 1d
    Cookie banner spec                      :p1s2g, 2026-05-29, 1d
    Sprint 2 retro                          :milestone, p1s2h, 2026-05-31, 0d

    section P1 Sprint 3: External feedback
    DPO consultation meeting                :crit, p1s3a, 2026-06-01, 1d
    Safeguarding lead meeting               :crit, p1s3b, 2026-06-02, 1d
    Download Anthropic DPA                  :p1s3c, 2026-06-03, 1d
    Download Firebase DPA                   :p1s3d, 2026-06-03, 1d
    Second-reader review of notice          :crit, p1s3e, 2026-06-04, 2d
    Revise notice from feedback             :p1s3f, after p1s3e, 1d
    Sprint 3 retro                          :milestone, p1s3g, 2026-06-07, 0d

    section P1 Sprint 4: Finalise
    Final privacy notice sign-off           :crit, p1s4a, 2026-06-08, 1d
    Hand off cookie banner spec             :p1s4b, 2026-06-09, 1d
    Hand off consent flow design            :p1s4c, 2026-06-10, 1d
    DPIA v0.2 update post-consultation      :p1s4d, 2026-06-11, 1d
    Phase 1 retro                           :milestone, p1s4e, 2026-06-14, 0d

    section P2 Sprint 2.1: Foundations
    Migration ticket take cleanly           :p2s1a, 2026-05-25, 3d
    Migration ticket refactor               :p2s1b, after p2s1a, 3d
    Migration ticket cutover housekeeping   :p2s1c, after p2s1b, 2d
    Firebase project create                 :p2s1d, 2026-05-27, 1d
    Astro and Firebase integration          :p2s1e, after p2s1d, 2d
    Firestore schema v0.1 sketch options    :p2s1f, 2026-06-01, 1d
    Firestore schema v0.1 selection         :p2s1g, after p2s1f, 1d
    Auth provider config email-link         :p2s1h, after p2s1g, 1d
    Sprint 2.1 retro                        :milestone, p2s1i, 2026-06-07, 0d

    section P2 Sprint 2.2: Sign-up
    Sign-up form with age field             :p2s2a, 2026-06-08, 2d
    Age-routing logic                       :crit, p2s2b, after p2s2a, 2d
    Magic-link email send                   :p2s2c, after p2s2b, 1d
    Magic-link verification handler         :p2s2d, after p2s2c, 2d
    Consent flow integration                :crit, p2s2e, after p2s2d, 2d
    End-to-end sign-up test                 :p2s2f, after p2s2e, 1d
    Sprint 2.2 retro                        :milestone, p2s2g, 2026-06-21, 0d

    section P2 Sprint 2.3: Sign-in
    Sign-in form                            :p2s3a, 2026-06-22, 1d
    Magic-link send for returning users     :p2s3b, after p2s3a, 1d
    Session persistence                     :p2s3c, after p2s3b, 2d
    Sign-out flow                           :p2s3d, after p2s3c, 1d
    Auth state across navigation            :p2s3e, after p2s3d, 1d
    Sprint 2.3 retro                        :milestone, p2s3f, 2026-06-28, 0d

    section P2 Sprint 2.4: Per-user state
    Firestore writes for progress           :p2s4a, 2026-06-29, 2d
    Read progress on page load              :p2s4b, after p2s4a, 2d
    Progress percentage calc                :p2s4c, after p2s4b, 1d
    Progress display on tiles               :p2s4d, after p2s4c, 2d
    Read and write integration testing      :p2s4e, after p2s4d, 2d
    Sprint 2.4 retro                        :milestone, p2s4f, 2026-07-12, 0d

    section P2 Sprint 2.5: GDPR and security
    Account deletion flow                   :p2s5a, 2026-07-13, 2d
    Data export flow                        :p2s5b, after p2s5a, 1d
    Firestore security rules first pass     :crit, p2s5c, 2026-07-15, 1d
    Firestore security rules audit          :crit, p2s5d, after p2s5c, 1d
    Second-eyes review of rules             :crit, p2s5e, after p2s5d, 1d
    Edge case testing                       :p2s5f, after p2s5e, 1d
    Phase 2 retro and handoff to Phase 3    :milestone, p2s5g, 2026-07-19, 0d
```

---

## Critical path summary

The critical path through Phase 1 and Phase 2 is:

1. **Privacy notice v0.1** (Sprint 2). Cannot start consultations without something to consult on.
2. **DPO and safeguarding consultations** (Sprint 3). Must complete before notice can be finalised.
3. **Second-reader review** (Sprint 3). Must complete before notice signs off.
4. **Final privacy notice sign-off** (Sprint 4). Closes Phase 1.
5. **Age-routing logic** (Sprint 2.2). The technical implementation of the age policy decision.
6. **Consent flow integration** (Sprint 2.2). Where Phase 1 deliverables meet Phase 2 code. Cannot complete until Sprint 4 of Phase 1 is done.
7. **Firestore security rules audit** (Sprint 2.5). Compliance gate before any UAT or production use.

Any slip on these items pushes downstream work directly. Other tasks have float and can absorb modest slips internally.

---

## Cross-phase dependency

The most fragile dependency in the schedule:

**Phase 1 Sprint 4** (consent flow design hand-off, completing 14 June) feeds **Phase 2 Sprint 2.2** (consent flow integration, ending around 21 June). Gap is one week. If Sprint 4 slips, Sprint 2.2 starts with placeholder consent design and refactors later. Acceptable for the POC but worth watching.

---

## Update protocol

- Edit this file directly when tasks shift. Mermaid syntax is documented at [mermaid.js.org/syntax/gantt.html](https://mermaid.js.org/syntax/gantt.html).
- When a task completes, append `done,` before its dependency declaration, e.g. `:done, p1s1a, 2026-05-18, 1d`.
- When a task is in progress, use `active,` in the same position.
- Add new tasks at the end of their sprint section so historical positions stay stable.
- Update the "Last updated" date at the top each time the file is committed.

---

## Linked artefacts

- [Project Charter](./project-charter.md)
- [Decision Log](./decision-log.md)
- [Risk Register](./risk-register.md)
- [DPIA](./dpia.md)
- [Migration Ticket SIGNAL2-001](./SIGNAL2-001-migration.md)

---

## Change log

| Date | Author | Change |
|---|---|---|
| 17 May 2026 | PM | Initial detailed Gantt for Phase 1 and Phase 2 |

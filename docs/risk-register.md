# Risk Register

**Project:** Signal Computer Misuse POC (Signal 2.0)
**Owner:** Chris Cross
**Maintained by:** Project Manager
**Last reviewed:** 17 May 2026
**Review cadence:** Weekly at sprint close

---

## Operating mode (added v1.1, per D-013)

The project is currently in **academic exercise mode**. Risks below are evaluated against two states:

- **Production state:** the state described in the original risk record, applying if the project re-activates per the triggers in charter Section 0
- **Current state:** the active status given the academic-exercise context

Risks with a "Deferred (study context)" status are not currently being mitigated because the conditions that would expose them (real user data, public deployment, commercial activity) are not in scope. They will revert to Open and require active mitigation if any re-activation trigger fires.

---

## Scoring system

**Likelihood**
- L (Low): unlikely to occur within the project window
- M (Medium): plausible, has happened on similar projects
- H (High): expected to occur unless mitigated

**Impact**
- L (Low): minor delay or rework, no project-level consequence
- M (Medium): moderate slip, manageable with replanning
- H (High): serious slip, compliance failure, or POC viability threatened

**Composite score** combines the two:
- High (H×H, H×M, M×H): demands active mitigation now
- Medium (M×M, H×L, L×H): mitigation planned, watched closely
- Low (L×L, M×L, L×M): logged, reviewed at sprint close

---

## Active risks

| ID | Risk | Category | L | I | Score | Mitigation summary | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| R-001 | GDPR exposure as sole data controller handling minors' data | Legal | M | H | High | DPIA, privacy notice, ICO registration, age-routed consent, second-reader review | CC | **Deferred (study context)** |
| R-002 | Content authoring sits on the critical path | Capacity | H | H | High | Schedule content sprints during half-term and summer, lock structure early, second-reader briefed in advance | CC | Open |
| R-003 | Firestore security rules historically a weak point on this codebase | Technical | M | H | High | Full day in Sprint 2.5, second pair of eyes on review, integration tests covering rules | CC | Open |
| R-004 | Capacity slip from teaching workload or adoption process | Capacity | H | M | High | Conservative 1.5 days/week baseline, four-week buffer, weekly sprint-close review | CC | Open |
| R-005 | LLM grading calibration fails to match authored rubrics | Technical | M | H | High | 20-sample test set, two-day prompt-design budget, iteration buffer in Phase 4 | CC | Open |
| R-006 | College DPO or safeguarding lead response delay blocks Phase 1 closure | Legal | M | M | Medium | Outreach in Sprint 1 week 1, written follow-up week 2, backup second-reader identified | CC | **Deferred (study context)** |
| R-007 | Contract clause prohibits independent platform for the same qualification | Legal | L | H | Medium | Sprint 1 contract clause check, NEU/UCU advice route available | CC | **Deferred (study context)** |
| R-008 | Magic-link emails landing in spam folders | Technical | M | M | Medium | Test from a clean inbox in Sprint 2.2, document SPF/DKIM fix path before UAT | CC | Open |
| R-009 | Schema design lock-in causing expensive rework later | Technical | M | M | Medium | Sketch 2-3 schema options in Sprint 2.1, pick the simplest, plan migration path | CC | Open |
| R-010 | Phase 1 slip cascades into Phase 2 dependencies | Schedule | M | M | Medium | Sprint-close review of parallel-track schedule, explicit dependency callouts | CC | **Deferred (study context)** |
| R-011 | Old Signal site collecting data while Signal 2.0 ramps up | Legal | L | M | Low | Old site to be taken down or marked deprecated once Signal 2.0 is live | CC | **Deferred (study context)** |
| R-012 | Deployment URL decision delayed, blocking privacy notice finalisation | Schedule | M | L | Low | Decision committed by end of Sprint 1 | CC | **Deferred (study context)** |
| R-013 | ICO investigation or complaint against an unregistered controller processing minors' data | Legal | L | H | Medium | ICO registration before any user contact; documented re-activation triggers in charter Section 0 | CC | **Deferred (study context)** |

---

## Risk detail

### R-001: GDPR exposure
**Detail:** As sole data controller for an independent platform processing personal data of minors (ages 16-17 within the user base), Chris Cross is personally accountable for GDPR compliance, breach notification, subject access requests, and ICO complaints. Any incident reaches him directly, not a corporate entity.
**Mitigation:** Full Phase 1 legal foundation including DPIA, privacy notice, age-routed consent flows, ICO Tier 1 registration, Data Processing Agreements with sub-processors. Second-reader review of the privacy notice planned for Sprint 3.
**Contingency:** If the second-reader identifies material gaps, Phase 2 deployment paused until resolved.
**Status note (v1.1, per D-013):** Reclassified to Deferred (study context). The risk is real and the mitigation plan above is correct for production state. In academic-exercise mode, no real data is being processed, so the risk is not currently exposed. Re-activation triggers in charter Section 0 will return this risk to Open.

### R-002: Content authoring critical path
**Detail:** Computer Misuse Act subsection content, six exam questions, six multi-level rubrics, and model answers per level all need authoring before grading calibration or UAT can run. Estimated at 10-11 effort days, this is the longest single phase.
**Mitigation:** Run content authoring across Weeks 1-11 with explicit content sprints during half-term and the start of summer break. Second-reader engagement booked early. Maintain rubric structure consistency so authoring rhythm settles after the first one or two questions.
**Contingency:** If content authoring slips past Week 11, grading calibration starts with whatever is complete and the rest gets folded in across Phase 4.

### R-003: Firestore security rules
**Detail:** The previous codebase had known weakness in Firestore security rules. Repeat patterns risk leaving user data exposed.
**Mitigation:** Treat Sprint 2.5 security rules audit as a full day, not a quick pass. Use Firebase's rules unit testing tools. Have someone else read the rules before they ship.
**Contingency:** If the audit surfaces issues, Sprint 2.5 extends rather than the rules being left in a partial state. POC does not go live with unaudited rules.

### R-004: Capacity slip
**Detail:** 1.5 effort days per week is the planning baseline, but actual capacity will dip during teaching peaks (mocks, parents evenings, end-of-term reporting) and during adoption-process steps. Cannot be eliminated, only planned around.
**Mitigation:** Schedule built to 1.5 days with a four-week buffer. Sprint-close review identifies slip early. Summer break used as a capacity bonus where the adoption process allows.
**Contingency:** Slipping past the September 6 ceiling triggers a scope conversation: either reduce content depth, defer GDPR-export feature, or postpone UAT.

### R-005: LLM grading calibration
**Detail:** The POC's grading layer relies on Claude Haiku applying a multi-level rubric consistently. If calibration drifts from the project owner's manual grading by more than approximately ±0.5 of a level, formative feedback loses credibility.
**Mitigation:** 20-sample test set built from authored sample answers across quality bands. Two-day prompt-design budget. Iteration buffer in Phase 4 if first calibration round fails.
**Contingency:** If Haiku does not calibrate within tolerance after two prompt-design iterations, switch grading mechanism to keyword matching plus tutor review for POC, and revisit LLM grading after launch.

### R-006: College DPO response delay
**Detail:** Sprint 3 of Phase 1 depends on DPO and safeguarding lead engagement. Both are part-time roles at the college and may respond slowly.
**Mitigation:** Email in Sprint 1 week 1, written follow-up week 2 if no response. Document outreach attempts for the DPIA.
**Contingency:** If both parties are unreachable by end of Sprint 2, escalate via line manager. As a final fallback, proceed with paid GDPR consultant review and document the unsuccessful college consultation in the DPIA.
**Status note (v1.1):** Deferred. No DPO outreach planned during academic-exercise mode.

### R-007: Contract clause
**Detail:** Most FE lecturer contracts include clauses about external activities, intellectual property derived from teaching, and platforms aimed at pupils. A clause could prohibit or constrain Signal 2.0.
**Mitigation:** Contract clause check is a Sprint 1 Week 1 task. NEU/UCU advice route available given project owner's rep role.
**Contingency:** If a clause prohibits the work as currently scoped, options are: limit Signal 2.0 to 18+ users only, restructure ownership, or pause the project pending clarification with the college.
**Status note (v1.1, per D-013):** Deferred. No platform activity targeting students during academic-exercise mode means no contract conflict is currently exposed. Re-activation triggers will return this to Open.

### R-008: Magic-link deliverability
**Detail:** Firebase Auth's magic-link emails can land in spam or be blocked by school-managed Gmail/Outlook accounts.
**Mitigation:** Test from a clean inbox not owned by the project owner during Sprint 2.2. Document SPF and DKIM configuration steps. Surface a "didn't receive the email" path in the sign-in UX.
**Contingency:** If deliverability proves unworkable, fall back to OAuth (Google sign-in) for the POC and revisit auth strategy after UAT.

### R-009: Schema lock-in
**Detail:** Firestore schema decisions made in Sprint 2.1 are expensive to undo once data exists. Wrong choices cascade into auth, progress tracking, and submissions.
**Mitigation:** Sketch 2-3 schema options in Sprint 2.1 docs and pick the simplest that works. Keep the schema human-readable and avoid premature optimisation.
**Contingency:** If schema needs revision after Phase 2, document the migration path before changing.

### R-010: Phase 1 slip cascade
**Detail:** Phase 1 outputs (age policy, consent flow, privacy notice) feed Phase 2 sprints. A slip in Phase 1 starts Phase 2 work late.
**Mitigation:** Parallel-track schedule with explicit dependencies marked. Sprint 1 outputs visible by end of Week 1 so Sprint 2 planning has reality to work from.
**Contingency:** If Sprint 4 of Phase 1 slips, Phase 2 Sprint 2.2 starts with placeholder consent design and refactors when Phase 1 closes. Acceptable for POC scope.
**Status note (v1.1):** Deferred. Phase 1 is not being executed in academic-exercise mode.

### R-011: Parallel data collection risk
**Detail:** If the old Signal site remains live while Signal 2.0 is being built, two distinct data controller scopes exist briefly.
**Mitigation:** Old site to be deprecated or taken down once Signal 2.0 is on a stable URL.
**Status note (v1.1):** Deferred. No live data on either old or new platform during academic-exercise mode.

### R-012: Deployment URL decision delay
**Detail:** Privacy notice references the production URL. If the URL is not decided, the notice cannot be finalised in Sprint 3 of Phase 1.
**Mitigation:** Decision committed by end of Sprint 1 (see ticket SIGNAL2-001).
**Status note (v1.1):** Deferred. Privacy notice is not being finalised in academic-exercise mode.

### R-013: ICO investigation exposure (added v1.1, per D-013)
**Detail:** If the project re-activates without completing Phase 1 (notably ICO registration and DPIA), processing personal data of minors as an unregistered controller would constitute regulatory non-compliance. ICO can investigate on its own initiative or in response to a complaint.
**Mitigation:** ICO registration before any user contact. The re-activation triggers in charter Section 0 are designed to force Phase 1 completion before any data subject access occurs.
**Contingency:** If a trigger is hit accidentally (e.g. URL shared inadvertently), pause platform access immediately, complete ICO registration, and document the event.
**Status note (v1.1):** Deferred. Conditional risk that materialises only if Phase 1 is skipped AND a re-activation trigger occurs.

---

## Closed and superseded risks

None yet.

---

## Review history

| Date | Reviewer | Changes |
|---|---|---|
| 17 May 2026 | PM | Initial register created with 12 entries from planning conversations |
| 17 May 2026 | PM | Reclassified R-001, R-006, R-007, R-010, R-011, R-012 to Deferred (study context); added R-013 (ICO investigation exposure) per D-013; added operating-mode note at the top |

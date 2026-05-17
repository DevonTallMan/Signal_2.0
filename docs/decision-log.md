# Decision Log

**Project:** Signal Computer Misuse POC (Signal 2.0)
**Owner:** Chris Cross
**Maintained by:** Project Manager
**Last updated:** 17 May 2026

---

## How this log is used

Every material project decision is recorded here with context, options considered, the choice made, and reasoning. Entries are append-only. If a decision is later superseded, a new entry is added that references the old one. The old entry is marked Superseded rather than deleted, so the trail remains intact.

Decisions taken during early planning conversations (before this log existed) have been backfilled below with the date of the original decision.

## Decision index

| ID | Date | Decision | Status |
|---|---|---|---|
| D-001 | 17 May 2026 | Progression: linear-by-default with exam section always accessible | Active |
| D-002 | 17 May 2026 | POC scope limited to Computer Misuse Act topic only | Active |
| D-003 | 17 May 2026 | Authentication via Firebase magic-link (passwordless) | Active |
| D-004 | 17 May 2026 | LLM judge for POC grading: Anthropic Claude Haiku | Active |
| D-005 | 17 May 2026 | Six exam questions per topic | Active |
| D-006 | 17 May 2026 | Feedback graded against multi-level rubric, not self-assessment | Active |
| D-007 | 17 May 2026 | Content authored in-house, AI restricted to variation and drilling | Active |
| D-008 | 17 May 2026 | Signal operated as project owner's independent project | Active |
| D-009 | 17 May 2026 | Capacity baseline: 1.5 effort days per week | Active |
| D-010 | 17 May 2026 | Phase 1 starts 18 May 2026 | Active |
| D-011 | 17 May 2026 | Success completion metric: "exam section reached" | Active |
| D-012 | 17 May 2026 | New repo Signal 2.0, old Signal repo to be archived | Active |

---

## Decision detail

### D-001: Progression model
**Context:** Initial client brief specified a strict linear progression with the exam locked until all subsections complete. Conflict raised in planning that this contradicts how revision actually works: students return to weak areas and skip content they already know.
**Options considered:**
1. Strict linear, exam gated by full subsection completion
2. Linear-by-default but exam section always accessible
3. Free navigation with no progression structure
**Decision:** Option 2.
**Reasoning:** Preserves the structured-learning intent while not blocking the revision use case. Reduces friction and avoids forcing students against natural revision patterns.

### D-002: POC scope
**Context:** Original brief envisioned the new pattern rolling across the platform. Team decision was to validate on one topic first.
**Decision:** Computer Misuse Act (4.1.2) only for the POC.
**Reasoning:** Content authoring is the expensive part. Cheaper to validate the pattern with one topic than to discover after six topics that the format is wrong.

### D-003: Authentication
**Context:** Per-user progress tracking requires accounts. Decision needed between password auth and passwordless.
**Options considered:**
1. Email and password with reset flow
2. Magic-link (email-link) sign-in via Firebase
3. OAuth (Google) only
**Decision:** Magic-link.
**Reasoning:** Removes password reset complexity, no password storage to secure, stronger baseline for handling minor user data, simpler UX for the POC's small user base. Revisit at scale if email deliverability proves unreliable.

### D-004: LLM judge
**Context:** Grading requires a model capable of applying a multi-level rubric to free-text answers.
**Options considered:**
1. Frontier API (Claude Haiku, Gemini Flash, GPT-4o-mini)
2. Self-hosted small language model via Ollama
3. Hybrid local-plus-API routing
**Decision:** Claude Haiku via Anthropic API for the POC.
**Reasoning:** Cheap, good calibration on structured rubric output, DPA available for UK GDPR compliance. Revisit at scale once submission volume justifies exploring free or self-hosted models. The quality ceiling is prompt and rubric driven, not model driven, so model changes alone will not unlock accuracy.

### D-005: Exam question count
**Decision:** Six exam questions for Computer Misuse Act.
**Reasoning:** Enough to assess coverage of the topic without making authoring or rubric design prohibitive at POC scale.

### D-006: Feedback model
**Context:** Question of how the system tells students how they have done.
**Options considered:**
1. Self-assessment against a published rubric
2. Keyword matching against rubric terms
3. LLM-as-judge applying a multi-level rubric
**Decision:** Option 3.
**Reasoning:** Self-assessment has weak learning value. Keyword matching is brittle. LLM-as-judge with a properly authored rubric gives genuine formative feedback aligned with mark scheme practice.

### D-007: Content authoring
**Context:** AI-generated content on the previous platform was rated poor quality.
**Decision:** All core content is human-authored. AI is restricted to producing variations of authored questions, drilling practice items, and supporting tasks. AI does not generate the source material.
**Reasoning:** The whole point of the rebuild is content quality. Letting AI generate the rubrics or subsection content rebuilds the original problem inside the new system.

### D-008: Project ownership
**Context:** Question of whether Signal sits under Exeter College's data controller umbrella or as an independent project.
**Decision:** Independent project. Chris Cross is sole data controller.
**Reasoning:** Cleaner contractual position, no dependency on college approval for the platform. Comes with the cost of personal accountability for GDPR compliance, ICO registration, and breach notification. Trade accepted.

### D-009: Capacity baseline
**Context:** Initial assumption was 1.5 effort days per week. Project owner suggested 3 hours per day might be more sustainable. Under pressure-testing, reverted to 1.5 days as the realistic figure given teaching workload, adoption process, and rep duties.
**Decision:** 1.5 effort days per week is the planning baseline.
**Reasoning:** Sustainable beats optimistic. Schedule built to this number with a four-week buffer for the inevitable slips.

### D-010: Phase 1 start
**Decision:** Phase 1 begins Monday 18 May 2026.
**Reasoning:** No reason to delay further. Sprint 1 tasks are mostly external (ICO registration, college outreach) and benefit from being in motion early.

### D-011: Success completion metric
**Context:** Multiple options for what "completion" means in success measurement.
**Options considered:**
1. All six subsections viewed
2. Exam section reached
3. Six questions attempted
4. Passing threshold on graded feedback
**Decision:** Exam section reached.
**Reasoning:** Tests pull-through (whether the structure draws students forward) rather than learning gain (which would require pre/post scoring). Honest fit for a POC validating structure, not pedagogy.

### D-012: Repository change
**Context:** Old Signal codebase carries technical debt including AI-generated content and unresolved Firestore security rule issues.
**Decision:** Fresh repository Signal 2.0. Old Signal repo to be archived once Signal 2.0 reaches a stable URL.
**Reasoning:** Clean slate is part of the POC validity. New ICO registration, privacy notice, and DPIA scope match the new project rather than carrying over old compliance context.

---

## Change log

| Date | Author | Change |
|---|---|---|
| 17 May 2026 | PM | Initial log created, twelve historical decisions backfilled |

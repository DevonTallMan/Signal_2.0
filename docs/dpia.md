# Data Protection Impact Assessment

**Project:** Signal Computer Misuse POC (Signal 2.0)
**Data Controller:** Chris Cross (sole controller, independent operator)
**DPIA Owner:** Chris Cross
**Document Status:** Draft v0.1, pending DPO and second-reader review
**Created:** 17 May 2026
**Statutory basis:** UK GDPR Article 35

> **About this document.** This DPIA is a working draft. Sections marked **[TO COMPLETE]** require Sprint 1 consultation outputs (college DPO, safeguarding lead) and Sprint 3 second-reader review before the document is final. Sections marked **[TO REVIEW IN PHASE 2]** depend on technical decisions that fall outside Phase 1 scope and will be revisited as those decisions are made.

---

## Why a DPIA is required

This project triggers UK GDPR Article 35 DPIA requirements on multiple grounds:

1. Processing personal data of vulnerable data subjects. The user base includes minors (T-Level Digital students aged 16-17 alongside 18+ students).
2. Innovative use of technology. LLM-based automated grading of free-text student answers is a novel processing operation.
3. Systematic evaluation. Per-user progress tracking combined with graded assessment constitutes systematic evaluation of personal aspects of natural persons.

The ICO's screening criteria treat any one of these as sufficient to require a DPIA. This project meets all three.

---

## Step 1: Identify the need for a DPIA

**What is the project?**
A web-based revision platform for T-Level Digital students. POC scope is a single topic (Computer Misuse Act, 4.1.2) with structured subsection learning and LLM-graded exam questions. The POC will deploy as a fresh implementation (Signal 2.0) replacing an earlier prototype.

**What kind of data processing is involved?**
- User account data (email address, age band)
- Per-user learning progress (which subsections viewed, exam attempts)
- Student free-text answers to six exam questions
- LLM-generated graded feedback on those answers

**Why is it being done?**
To test whether structured-progression learning combined with formative LLM-graded assessment improves student engagement on the Computer Misuse Act topic, ahead of any decision to scale the approach across other topics.

**Why is a DPIA needed?**
See "Why a DPIA is required" above. The data subjects are vulnerable (minors), the technology is innovative (LLM grading), and the processing is systematic.

---

## Step 2: Describe the processing

### Nature of processing

Personal data is collected directly from data subjects at sign-up and during platform use. It is stored in Google Firestore (UK or EU region, to be confirmed in Sprint 2.1). Student exam answers are transmitted to Anthropic's API for grading and the graded response is returned and stored. No data is shared with third parties beyond the named sub-processors.

### Scope

| Aspect | Detail |
|---|---|
| Data subjects | T-Level Digital students. POC user base 5-10 individuals at UAT, expected platform user base 30-100 within first academic year if scaled. |
| Categories of personal data | Email address, age band declaration, learning progress events, free-text exam answers, generated feedback |
| Special category data | None planned. Age band is processed but is not a special category in itself. |
| Data subject ages | 16-17 and 18+. Under-16 users not permitted at POC stage. |
| Geographic scope | UK only |
| Volume | Low at POC stage. Each user generates approximately 50-100 progress events and up to 6 graded exam submissions during initial engagement. |
| Duration of processing | Account active until user deletes account or 24 months of inactivity (retention policy to be finalised in Sprint 2 of Phase 1). |

### Context

The data subjects are FE students using the platform for revision purposes. The data controller is also an FE lecturer at Exeter College, which creates a context worth noting in this DPIA: students at the college may use the platform, but use is voluntary and the platform is operated independently of the college's systems. The college DPO and safeguarding lead are being informed as part of Phase 1 of the project.

### Purposes

| Purpose | Lawful basis (proposed) |
|---|---|
| Account creation and authentication | Performance of contract (the implicit agreement to provide the service) |
| Storing learning progress | Performance of contract |
| Grading exam answers via LLM | Legitimate interest (formative assessment), with explicit consent at sign-up |
| Improving the platform | **[TO COMPLETE]** subject to DPO advice; likely separate consent if statistical analysis is intended |

**Note:** Lawful basis selection requires DPO review. Particular attention is needed for the 16-17 cohort under UK GDPR's treatment of children's data.

---

## Step 3: Consultation process

### Internal stakeholders
- Project owner and sole controller: Chris Cross. Consulted continuously.

### Sub-processors
- Anthropic. UK GDPR-compliant Data Processing Agreement to be filed in Sprint 3 of Phase 1.
- Google Firebase. UK GDPR-compliant DPA to be filed in Sprint 3 of Phase 1.

### External consultations

| Party | Purpose | Status |
|---|---|---|
| Exeter College Data Protection Officer | Awareness, advice on age-based consent for student users | **Scheduled Sprint 1, Phase 1** |
| Exeter College Safeguarding Lead | Awareness, advice on minor user data on a private platform | **Scheduled Sprint 1, Phase 1** |
| Second-reader GDPR review (paid consultant or qualified colleague) | Review of privacy notice and this DPIA | **Scheduled Sprint 3, Phase 1** |
| Data subjects (students) | Feedback during UAT walkthroughs | **Scheduled Sprint 5, late August 2026** |

Consultation outcomes will be recorded under Step 7 as they happen.

---

## Step 4: Necessity and proportionality

**Is the processing necessary to achieve the stated purpose?**
Yes. Account creation enables per-user progress tracking, which is one of the features being tested. LLM grading is the assessment mechanism being evaluated. Without these processing operations, the POC cannot test what it is intended to test.

**Could the purpose be achieved with less personal data?**
Some yes, some no:
- Authentication could be removed entirely if progress tracking moved to localStorage (option considered, rejected in favour of testing the production architecture).
- Free-text answers could be replaced with multiple choice (rejected; the POC tests rubric-based grading of free-text, which is the pedagogical question).
- Email address is the minimum identifier needed for magic-link auth. No other PII is collected.

**Is the processing proportionate to the purpose?**
Yes. The processing collects only what is needed to operate the POC and validate the engagement and grading hypotheses. No tracking, profiling for advertising, or third-party data sharing.

**Lawful basis justification:**
- Account and progress data: performance of contract. The user signs up to use the platform; storing their account and progress is part of providing that service.
- Exam answers and grading: explicit consent at sign-up, in addition to performance of contract. The consent flow makes clear that answers are sent to an LLM for grading.

**[TO REVIEW]** Final lawful basis confirmation pending DPO advice in Sprint 1.

---

## Step 5: Identify and assess risks

| Risk to data subjects | Likelihood | Severity | Overall risk |
|---|---|---|---|
| Unauthorised access to user accounts (e.g. weak auth) | L | M | Low |
| Unauthorised access to stored data via misconfigured security rules | M | H | High |
| Data sent to LLM provider being used to train models | L | M | Low (Anthropic API contract excludes training on customer data) |
| Email deliverability failure leading to account lockout | M | L | Low |
| User unable to exercise right to erasure due to incomplete delete flow | M | M | Medium |
| User unable to exercise right of access due to no export flow | M | M | Medium |
| Data breach disclosure of email addresses and learning behaviour | L | H | Medium |
| Minor user data held outside any institutional oversight | M | M | Medium |
| LLM grading producing harmful or discriminatory feedback | L | M | Low |

### Risk detail (selected)

**Unauthorised access via misconfigured Firestore rules** is rated High because the previous codebase had known weakness here. Treated as a top mitigation priority in Sprint 2.5.

**Minor user data held outside institutional oversight** is the structural risk inherent to operating Signal 2.0 as an independent platform rather than under the college's data controller umbrella. The college DPO and safeguarding lead are being informed as part of mitigation, but ultimate accountability rests with the project owner.

**LLM grading producing harmful or discriminatory feedback** is rated Low because the rubric structure constrains the model's output, but is included because the risk of biased automated decision-making is a recognised concern with LLM grading in educational contexts. Mitigations include calibration testing and tutor review of feedback during UAT.

---

## Step 6: Identify measures to reduce risk

| Risk | Mitigation | Effect on risk |
|---|---|---|
| Unauthorised access via security rules | Full Sprint 2.5 day for rules audit, integration tests, second pair of eyes review | Reduces High to Low |
| LLM training on customer data | Use Anthropic API under DPA explicitly excluding training | Risk addressed contractually |
| Right to erasure incomplete | Account deletion flow with cascade delete in Sprint 2.5 | Reduces Medium to Low |
| Right of access incomplete | Data export flow (JSON download) in Sprint 2.5 | Reduces Medium to Low |
| Data breach impact | Minimisation: only collect email and learning data, no special categories | Limits severity if a breach occurs |
| Minor data held independently | DPO and safeguarding lead informed, age-routed consent flow, age band declared at sign-up, under-16 users not accepted at POC stage | Reduces but does not eliminate; structural risk acknowledged |
| Discriminatory LLM feedback | Rubric-constrained prompts, calibration testing, manual review of UAT feedback samples | Reduces likelihood |

**[TO REVIEW IN PHASE 2]** Technical mitigations will be revisited and verified during Sprint 2.5 (security rules and GDPR flows).

---

## Step 7: Sign-off and outcomes

### Approval

| Role | Name | Decision | Date |
|---|---|---|---|
| Data Controller | Chris Cross | **[PENDING]** | |
| DPO consulted (external, advisory) | **[TO COMPLETE Sprint 1]** | | |
| Second-reader (GDPR review) | **[TO COMPLETE Sprint 3]** | | |

### Residual risk

**[TO COMPLETE]** After mitigations are implemented and tested, residual risks will be recorded here. If any residual risk remains High, ICO prior consultation under Article 36 may be required before processing begins.

### Implementation tracking

| DPIA action | Linked sprint | Status |
|---|---|---|
| Register with ICO | Phase 1 Sprint 1 | Open |
| Privacy notice draft | Phase 1 Sprint 2 | Open |
| DPO consultation | Phase 1 Sprint 1-3 | Open |
| Safeguarding lead consultation | Phase 1 Sprint 1-3 | Open |
| Second-reader review | Phase 1 Sprint 3 | Open |
| Anthropic DPA filed | Phase 1 Sprint 3 | Open |
| Firebase DPA filed | Phase 1 Sprint 3 | Open |
| Firestore security rules audit | Phase 2 Sprint 2.5 | Open |
| Account deletion flow | Phase 2 Sprint 2.5 | Open |
| Data export flow | Phase 2 Sprint 2.5 | Open |
| Age-routed consent flow | Phase 2 Sprint 2.2 | Open |
| UAT consultation with data subjects | Phase 5 Sprint | Open |

### Review schedule

This DPIA will be reviewed:
- At the end of Phase 1 (Week 4) when legal foundation closes
- Before UAT begins (Week 15)
- Before any decision to scale beyond the POC
- Whenever a material change to processing is proposed

---

## Change log

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 (draft) | 17 May 2026 | Chris Cross (assisted by PM) | Initial draft populated from planning decisions. Sections requiring DPO and second-reader input marked for completion in Sprints 1 and 3. |

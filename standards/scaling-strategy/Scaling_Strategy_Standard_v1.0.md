# Scaling Strategy Standard

**Version:** 0.1 (Provisionally Ratified)
**Status:** Governing standard — provisional pending revision after 3–5 real Solution Track applications
**Layer:** Standard (Scaling Intelligence Operating System)
**Discipline:** Scaling Strategy
**Companion documents:** Doctrine Layer v0.1 · Scaling Strategy templates, process docs, and cases (referenced, not duplicated, herein)

---

## 0. About This Standard

This is the governing standard for the Scaling Strategy discipline, one of three core disciplines of the Scaling Intelligence Operating System (alongside Scaling Knowledge and Scaling Intelligence). It defines *what a Scaling Strategy product must be and do*. It does not contain the templates, checklists, or worked examples that implement it; those live in the discipline's `templates/`, `process/`, and `cases/` folders and are referenced by section.

**Provisional status.** This standard was written before the repository held substantive curated cases. It is a reasoning spine, not an evidence-backed synthesis. Its thresholds (§6, §7, §12) are provisional and are to be tuned against real cases. Revision after 3–5 real Solution Track reviews is a **required part of governance**, not an aspiration.

**Reading conventions.** Throughout the discipline, every substantive claim is labeled **Evidence**, **Interpretation**, **Strategic judgement**, or **Recommendation** (and **Unknown** where applicable). This labeling is the discipline; a product that omits it does not conform to this standard.

**Open questions.** Several design decisions in this standard rest on unresolved Doctrine entries. Where a rule rests on an open question, this standard flags it inline as `[Doctrine: DOC-…]`. Those flags mean the rule is provisional and may change through the governance process, not that it may be ignored.

---

## 1. Purpose of Scaling Strategy

Scaling Strategy is the discipline that converts Scaling Intelligence into **decisions about where to invest scarce scaling effort, what to fix first, and whether an innovation should advance, adapt, pause, or stop.**

It is not a technology-dissemination plan, a workshop output to be filed, or a compliance artifact for reporting.

For any Solution Track, the discipline answers three questions:

1. Is this innovation embedded in a viable scaling *system* — demand, delivery, financing, institutional ownership, policy — or only technically validated? (Separate technical validity from scaling readiness.)
2. What is the single binding constraint relative to the scaling ambition, and is it worth resolving?
3. What should change — in the innovation, the system, or the investment decision — as a result?

"Recommend against scaling" is a first-class, equal-status outcome of the discipline, not a failure of it.

---

## 2. Primary Users

**Primary (decision-makers and doers):**

- **Solution Track teams** — innovation owners who act on findings.
- **AoW2 / Scaling Intelligence coaches** — who facilitate reviews and steward the reasoning.
- **Portfolio and investment decision-makers** — who allocate across tracks and gate stages.

**Secondary (consumers of the reasoning):** other Areas of Work receiving handoffs; donors and program leadership; the repository itself (each product becomes a future case record).

Primary users have divergent and sometimes opposed incentives (a track wants to advance; a portfolio wants to prune). The discipline serves both by making its reasoning legible to both: recommendations are sorted by owner (§7), and an evidence floor (§12) that enthusiasm alone cannot lower governs stage decisions.

---

## 3. Structure of a Scaling Strategy Review

A Scaling Strategy Review is the discipline's core diagnostic product. It proceeds through eight sections, integrating systems-based strategic reasoning, IPSR packaging logic, and enabling-condition scanning without adopting any single methodology as canonical.

**0. Executive Judgment** — stage-gate recommendation, single weakest link (one sentence), one-sentence rationale, confidence level. Stated as a claim at the top; the body below must reconstruct the reasoning so the judgment is auditable. `[Doctrine: DOC-STRAT-002 — executive-judgment-first vs. reasoning-first sequencing is unresolved.]`

**A. Scaling Ambition & Denominator** — what, for whom, where, by whom, when, how many, why; and the implied denominator, which determines whether delivery and financing are plausible at all.

**B. Problem–Solution Fit & Innovation Package** — real, prioritized demand; adoptability of the *package* (core plus complementary innovations, services, finance, agreements), not the technology alone.

**C. Real-World Evidence** — evidence of sustained use without donor subsidy, explicitly separated from pilot and demonstration data.

**D. Scaling System Map** — the core diagnostic: for each of demand creation, delivery, financing, coordination, policy support, and learning/adaptation, identify actor, incentive strength, risk, and evidence status. For each function ask: who pays, who benefits, who does the work, who continues after donor support ends.

**E. Responsible Scaling & Inclusion** — who benefits, who is excluded, who bears risk; gendered and environmental trade-offs. Not optional.

**F. Weakest-Link Analysis** — see §5.

**G. Critical Assumptions** — see §6.

**H. Recommendation & Stage-Gate** — owner-sorted recommendations (§7), an explicit stage-gate (§12), and adaptive decision rules (§8).

The fillable template implementing these eight sections is `templates/scaling-strategy-review.md`. This standard defines the sections; the template defines the fields.

---

## 4. Translating Scaling Intelligence into Strategic Action

Translation follows a traceable chain: **Intelligence → Diagnosis → Decision → Action.**

1. **Intelligence** — curated repository knowledge plus track-specific inputs (IPSR outputs, Scaling Scan scores, field evidence); missing intelligence is itself an input.
2. **Diagnosis** — the system map and weakest-link analysis (what the intelligence means for this track).
3. **Decision** — the stage-gate and priority.
4. **Action** — owner-sorted recommendations with decision rules.

**Governing rule:** no recommendation may appear that does not trace back through a diagnosis to a piece of intelligence. An untraceable would-be recommendation is relabeled a *hypothesis requiring evidence* (§7, category e), not issued as an action.

The operational procedure a coach follows is `process/intelligence-to-strategy.md`.

---

## 5. Weakest-Link Analysis and Priorities

A scaling system performs at the level of its binding constraint, not its average strength. Effort spent on a non-binding function produces little movement toward the ambition.

Procedure:

1. Score each system function (§3D) for strength *relative to the scaling ambition*, not in the abstract.
2. Identify the **single** function whose failure would most constrain scaling. Resist a long list of generic bottlenecks.
3. Apply the **leverage question**: is the weakest link fixable by anyone in reach? A weakest link no one can move is a pause/stop signal, not a work plan.
4. Sequence: resolve the binding constraint first; do not invest downstream until the upstream constraint is credibly resolved or has a resolution pathway.

**Constraint independence.** The reviewer must state, as a hypothesis with confidence, whether the identified weakest link is *independent* or *coupled* to others. Single-link tunnel vision is the principal failure mode of weakest-link reasoning; the default nonetheless remains to name one binding constraint, with coupling recorded as a check rather than a licence to enumerate.

---

## 6. Identification, Challenge, and Testing of Assumptions

Every scaling strategy rests on assumptions; the discipline makes them explicit, ranks them by consequence, and assigns each an evidence status.

**Identify.** For each system function and for the ambition itself: what must be true for this to work? Sustainability assumptions ("who continues after donor support") are the most commonly unstated and most often wrong.

**Challenge.** Probe: Are we equating reach, pilots, or trainings with scaling? Is field evidence or workshop opinion behind this? Does the business/fiscal case close without donor money? Who has an incentive to call this assumption safe?

**Test.** Classify every critical assumption in the assumption table (assumption · evidence status · risk if wrong · how to test · owner). Evidence status uses the confidence ladder: **Well supported / Moderately supported / Emerging / Speculative / Insufficient evidence.**

**Decisive rule.** An assumption that is both *high-risk-if-wrong* and *speculative or insufficient* becomes a **critical uncertainty** that gates the stage decision: the track cannot be recommended to advance until it is tested, or the recommendation must be explicitly conditional or a pause.

---

## 7. Recommendations Sorted by Owner

Every recommendation is assigned to exactly one owner category; an unassigned action is an action no one takes. This section also enforces the S4I Area of Work boundary.

**(a) Solution Track** — what the innovation team controls: package refinement, field testing, partner conversations it can initiate.

**(b) AoW2 / Scaling Intelligence** — coaching, diagnosis, evidence synthesis, stage-gating facilitation, connecting the track to intelligence. **Boundary rule:** AoW2 may *diagnose* dependencies involving enabling environment and finance and may *recommend* that AoW3/AoW4 or partners act, but may not claim to *deliver* AoW3/AoW4 functions. "AoW2 will build the delivery system" is a boundary violation and must be rewritten as a diagnosed dependency plus a handoff.

**(c) Other Areas of Work** — delivery (AoW3/4), finance functions, and similar. Written as handoffs: the diagnosed need, the evidence, and what the receiving AoW must decide.

**(d) External partners** — demand partners, private sector, government, financiers. Named where possible; otherwise flagged as a partner gap (often itself a weakest link).

**(e) Additional evidence** — the "cannot responsibly recommend yet" category, where critical uncertainties (§6) and untraceable would-be recommendations (§4) land. A healthy review usually produces real entries here.

**Mandatory constraint on category (e).** Every evidence-needed item carries a decision rule: advance if X shows Y by date Z; otherwise pause. Evidence needs without a decision rule are not permitted. `[Doctrine: DOC-STRAT-003 — whether category (e) is primarily a procrastination risk or a false-confidence safeguard is unresolved; the decision-rule requirement constrains both failure modes.]`

---

## 8. Adaptive Management

Strategies are adaptive by construction, not by amendment. Every recommendation and every critical assumption carries a decision rule:

> If [observable signal] by [time], then [advance / adapt / pause / stop / reallocate].

A review therefore outputs not a fixed plan but a decision tree: the current stage-gate plus the signals that would change it. Adaptive management is operationalized through leading indicators tied to the weakest link (not lagging output counts), trigger thresholds agreed in advance so a pause or pivot is a pre-committed decision, and a revisit cadence proportional to uncertainty.

Triggers are recorded at review time so that the next session can check whether the team adapted or rationalized. Adaptive management is real only if triggers are set before outcomes are known and honored when hit.

---

## 9. Coaching Continuity

Coaching is longitudinal. Each engagement produces a **Coaching-Case Record** — the Review and Coaching Brief filed together — carrying forward: the prior stage-gate and rationale; the critical assumptions and their test status; the decision rules and whether triggers fired; the weakest link then versus now; and open questions carried forward. Each record also carries the Doctrine tags the engagement bore on (§11).

**Continuity rule.** Every session opens by reconciling what was said would happen against what happened. A coach who cannot answer "did the last review's assumptions hold?" is restarting the track, not coaching it.

The record holds both an auditable spine and a clearly labeled *coach's judgement* field for tacit, unverifiable reads. `[Doctrine: DOC-STRAT-004 — when relational and auditable continuity conflict, which governs is unresolved and is referred to the human reviewer.]`

---

## 10. Monitoring Strategic Progress

Progress is movement of the binding constraint and the stage-gate, not activity counts. Three layers:

1. **Constraint movement** — is the weakest link weaker, unchanged, or resolved? Primary metric.
2. **Assumption resolution** — what fraction of critical uncertainties have been tested and closed?
3. **Stage-gate trajectory** — advancement is earned by evidence, not scheduled; each stage change is tracked with its triggering evidence.

**Prohibition.** Reach numbers (farmers trained, hectares, downloads) must not serve as the progress metric. Reach is an output; it may be evidence about a function (e.g., demand) but is never itself strategic progress.

---

## 11. Strategic Visualizations

Visuals must make reasoning legible, not decorate outputs, and every visual carries an evidence/confidence legend; a heat map without provenance is interpretation dressed as data. The full recommended set — system map heat-map, weakest-link tracker, assumption risk matrix, stage-gate trajectory, owner-sorted action board, and portfolio view — is deferred to Version 2 per the v0.1 implementation plan, with the exception of a simple (table or hand-drawn) System Map heat-map permitted in v0.1.

Each engagement records which open Doctrine entries it bore on, feeding the Doctrine evidence loop (see Doctrine Layer §4).

---

## 12. Minimum Evidence for Decision-Grade Recommendations

This is the evidentiary floor. A strategic recommendation is **decision-grade** — robust enough to gate a real investment or stage decision — only when all of the following hold:

1. The scaling ambition and denominator are explicit.
2. The weakest link is identified with a stated confidence level.
3. Critical assumptions are classified, and no assumption that is both high-risk-if-wrong and speculative/insufficient remains untested — or the recommendation is explicitly conditional or a pause.
4. At least one piece of real-world (non-workshop, non-demonstration) evidence bears on the binding constraint.
5. Sources are not falsely independent (documents from one methodology family or one project team are not corroboration).
6. Owner and decision rule are attached.

**Evidence sufficiency tiers:**

- **Decision-grade** — meets all six; may gate a stage or investment.
- **Coaching-grade** — meets 1–3 but lacks real-world evidence (4); guides a team's next steps and evidence-gathering, but may not advance a stage-gate.
- **Exploratory** — early diagnosis; surfaces hypotheses and questions only.

**Stage-gate options:** Proof of Concept · Transition to Scale · Active Scaling · Targeted Bottleneck Support · Not Ready for Scaling Investment. The last is a legitimate, valued outcome.

**Unresolved gate boundary.** The real-world-evidence requirement (criterion 4) blocks advancement to Active Scaling absolutely. Whether it also blocks Transition to Scale is unresolved: one view holds that TtS advancement requires it; the other holds that TtS is the stage designed to generate such evidence, making the requirement circular. `[Doctrine: DOC-STRAT-001 — the single most consequential open decision in this standard; it sets how conservative the whole system is. Referred to governance.]`

---

## 13. Quality Assurance

Before any recommendation issues, the pre-issue checklist in `process/quality-assurance.md` is run. It includes hard stops for AoW boundary violations (§7) and for stage-advancing recommendations resting on workshop opinion alone (§12).

Coaching-grade and Exploratory outputs may issue on the coach's self-check. **Decision-grade outputs require independent Analyst-role review** before issuing.

---

## 14. Conformance

A product conforms to this standard when it: follows the eight-section review structure (§3) or derives from it with documented reason; labels claims by type (§0); sorts recommendations by owner and respects the AoW boundary (§7); attaches decision rules to recommendations and evidence needs (§7, §8); states its evidence tier honestly (§12); and passes the QA gate (§13).

A Scaling Strategy product is a **working analysis** until reviewed and saved into the repository, at which point it becomes an authoritative Repository Object. The repository is the source of truth; this standard governs how products are made, not what is ultimately true.

---

## 15. Governance and Revision

This standard is provisionally ratified at v0.1. Its revision is governed as follows:

- Revision after **3–5 real Solution Track reviews** is required, not optional. Thresholds in §5, §6, and §12 are to be tuned against real cases at that point.
- Changes to this standard flow only through a deliberate, logged governance act (human-ratified revision). Evidence flows up to Doctrine continuously; changes flow down to Standards only through a gate (see Doctrine Layer §6).
- Open questions flagged inline (`[Doctrine: …]`) are tracked in the Doctrine register (`doctrine/register.md`) and may be resolved, reframed, or reopened only through Doctrine governance.

---

## References (not duplicated herein)

- **Templates:** `templates/scaling-strategy-review.md`, `templates/coaching-brief.md`
- **Process:** `process/intelligence-to-strategy.md`, `process/quality-assurance.md`
- **Doctrine:** `doctrine/register.md`; Doctrine Layer v0.1
- **Cases:** `cases/` (completed Reviews and Coaching-Case Records)
- **Methodological foundations referenced but not owned by this standard:** IPSR, Scaling Scan, AICCRA Scaling Playbook, GenderUp, responsible scaling approaches, and systems-based scaling strategy reasoning. This standard is methodology-neutral and integrates these without privileging any one.

---

*End of Scaling Strategy Standard v0.1.*

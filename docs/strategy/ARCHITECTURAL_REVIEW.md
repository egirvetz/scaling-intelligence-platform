# Scaling Intelligence — Architectural & Philosophical Review

**Purpose:** OPEN_QUESTIONS_LOG.md tracks specific content-level gaps and pending actions that fell out of individual documents. This is a different, higher-order pass: a review of the whole body of work — four ingestions, one Reflection, one Foundation document, one gap audit — for design decisions, philosophical tensions, recurring themes, and architectural patterns that emerged *through the practice of doing the work*, but were never articulated as such. Several of these were visible only in hindsight, by comparing how the work was actually done across documents rather than reading any single output.

Ten items follow. For each: why it matters, where it belongs in the repository, and what kind of artifact it should become.

---

### 1. Escalating beyond the primary source when metadata is thin

**What emerged:** When curating the IPSR Trained Facilitator Guide, its primary source had no named author, no citations, and no stated theoretical basis for its core scoring framework. Rather than curate it as-is, the response was to actively locate and read a companion document (the covering note) to establish basic provenance before writing the card. This happened silently, as a judgment call in the moment — it was never named as a rule.

**Why it matters:** This is a real methodological practice, not a one-off. It answers a question every future ingestion will face: when is it acceptable to curate a document on its own terms, and when does thin provenance obligate seeking outside context first? Right now that judgment call is made ad hoc, which means it will be made inconsistently as more curators (human or AI) do this work.

**Where it belongs:** In the Librarian's operating procedure, specifically the Ingest mode description.

**Recommendation:** **Design Principle.** Something close to: "When a primary source lacks basic provenance (author, citation basis, organizational context), actively seek a companion or context document before curating — and if none exists, say so explicitly rather than curating in an evidentiary vacuum." This should be added to FOUNDATION.md's Section 9 design principles list, where it is currently absent.

---

### 2. The curation methodology itself matured mid-project, and earlier work was never updated to match

**What emerged:** Comparing Card 001 against Card 004 shows a real evolution: early relationship confidence-grading used a simple High/Medium/Low scale; by Card 004, the grading had become noticeably more precise — distinguishing "source-confirmed on both sides," "confirmed from only one side," "curator-drawn structural parallel," and "genuinely unresolved" as four different things, not three. That's a genuine improvement in the curation method. It was never applied backward to Cards 001–002.

**Why it matters:** This reveals something the current operating modes don't account for. *Refresh* mode (as defined) is triggered by new evidence about the *subject matter*. But this is a different trigger entirely: the *curation method itself* got better, independent of any new source document. Without a named mechanism for this, every methodological improvement will keep applying only forward, and the earliest cards in the repository — often the most foundational ones — will silently be the least rigorously curated, with no flag indicating that.

**Where it belongs:** In the Librarian's operating modes, as a fifth mode alongside Ingest / Curate / Refresh / Reflect.

**Recommendation:** **Foundation document update.** Add a fifth mode — provisionally "Recalibrate" — to FOUNDATION.md Section 5, defined as: revisiting existing cards not because new evidence emerged, but because the curation method itself has demonstrably improved since they were written.

---

### 3. An unresolved tension between Reflect mode and "the Librarian never prescribes"

**What emerged:** The scaling-librarian's stated identity is explicit: not a coach, not an evaluator, never prescribing strategy. But the Reflection assessment necessarily made judgment calls — about which convergences mattered, which patterns were "the strongest in the repository," what the repository "is becoming." Every interpretive claim was labeled as such, but labeling isn't the same as resolving the underlying tension: a sufficiently confident, well-labeled interpretation can still function, in practice, as de facto strategic guidance to whoever reads it.

**Why it matters:** As Reflect-mode output accumulates and gets referenced (as it already has been, in FOUNDATION.md), there's a real risk of mission creep — not because any single Reflection oversteps, but because repeated, confidently-written syntheses can calcify into something readers treat as settled guidance, even with careful hedging. This hasn't happened yet, but nothing currently guards against it.

**Where it belongs:** This is a genuine philosophical question about the boundary between the Librarian and the future Analyst/Coach roles, not something resolvable by more careful wording alone.

**Recommendation:** **Remain an open question**, but a named one — it should not be quietly assumed "handled" just because confidence labels exist. Worth surfacing for explicit human judgment: should Reflect-mode output carry a standing disclaimer distinguishing it from Coach-produced strategic advice, even when both are well-labeled?

---

### 4. The Knowledge Card template is being extended through practice faster than it's being formalized

**What emerged:** The template has already been informally extended twice — a "split currency" section was invented specifically for the IPSR Deep-Dive card because it mixed durable and time-bound content, and a full "Repository Contribution Analysis" section was added to that same card at your request. Neither extension was folded back into a canonical, versioned template description.

**Why it matters:** Right now, "the template" only exists as whatever the most recent card happened to do. That works while one curator holds the whole history in working memory, but it will not survive a new contributor, a new session, or simply more volume — the next card could easily regress to the original six-part structure and quietly lose the extensions that later cards proved valuable.

**Where it belongs:** As its own versioned artifact, separate from any individual card.

**Recommendation:** **Foundation document** — specifically, a dedicated `KNOWLEDGE_CARD_TEMPLATE.md`, versioned, with the split-currency field and the contribution-analysis section formally incorporated as optional (not core) sections, and a note on when each applies.

---

### 5. The classification taxonomy changed mid-project, creating a retroactive inconsistency

**What emerged:** The first two cards were classified using one category list (Foundational / Reference / Operational / Historical / Draft / Other). By the fourth request, "Methodology" had been added as an explicit option — and used, correctly, for the IPSR Deep-Dive. But the Scaling Scan (Card 002) was classified "Foundational" under the *old* list, without ever being asked whether "Methodology" — a category that arguably fits it at least as well — would have been the better call.

**Why it matters:** This isn't just a labeling nitpick. If classification is meant to drive repository organization (Section 3 of the Capability Framework discussion, and the Methodologies/Coaching-Records taxonomy), then two documents classified under two different, non-identical taxonomies aren't actually comparable yet, even though the repository currently treats them as if they were.

**Where it belongs:** A Curate-mode pass across all existing cards once the taxonomy is stable.

**Recommendation:** **Remain an open question until a Curate-mode review is run**, then resolve by either reclassifying Card 002 under the fuller taxonomy or explicitly deciding "Foundational" still holds even with "Methodology" available — but that decision should be made deliberately, not left as an artifact of when the card happened to be written.

---

### 6. The Analyst/Coach → Librarian feedback loop only exists today because a human keeps prompting it

**What emerged:** FOUNDATION.md describes a loop where Analyst and Coach outputs become new material for the Librarian to curate. Looking at what's actually happened so far, a version of this loop *has* been running — the Reflection produced recommendations, which prompted FOUNDATION.md, which prompted this review — but only because you kept asking for the next step. There is no mechanism by which that would happen on its own.

**Why it matters:** This is the difference between a designed architecture and an observed pattern that a human is currently doing the work of. It's a meaningful distinction to name honestly rather than let FOUNDATION.md's confident description of "the loop" imply more automation than exists.

**Where it belongs:** FOUNDATION.md Section 5 and Section 11 (open questions).

**Recommendation:** **Design Principle plus explicit open question.** State plainly, as a principle, that the loop is currently human-mediated by design, not yet automated — and log, as an open question, whether and how it should become self-triggering as Analyst and Coach get built.

---

### 7. Confidence-grading discipline has a cost that will grow with the repository

**What emerged:** Every artifact produced so far has consistently hedged, labeled, and confidence-graded its claims — a real, deliberately maintained discipline. But the cards are already long, and the proportion of each card devoted to caveats and confidence labels (versus content) has been growing, not shrinking, as the practice matured.

**Why it matters:** This is a genuine principle worth keeping, but it has a scaling cost nothing currently addresses: at some volume of cards, verbose per-claim hedging risks becoming background noise a reader learns to skip past — which would defeat the entire purpose of grading confidence in the first place. The discipline is right; the *presentation* of it hasn't been designed for scale.

**Where it belongs:** A future design problem for whoever builds the interfaces sitting on top of the repository (the "Platform" side of the Platform/Repository distinction).

**Recommendation:** **Design Principle, with an explicitly flagged open implementation question.** Principle: confidence grading is non-negotiable. Open question: what structural or visual mechanism (separate from dense inline prose) will keep it legible once the repository holds dozens of cards instead of four.

---

### 8. The repository is quietly holding two different kinds of knowledge under one roof

**What emerged:** Three of the four ingested documents are about *how to scale an innovation* (methodology, coaching). The fourth — the IPSR Deep-Dive — is substantially about *how an institution governs and funds scaling decisions across many innovations at once* (AoW 2, 19 submissions, stage-gating, PRMS). These aren't the same kind of knowledge, even though they currently sit in the same proposed taxonomy branch.

**Why it matters:** This distinction matters more as Portfolio Intelligence gets built, because that role will need institutional-governance knowledge (how stage-gating actually works, what PRMS requires) that is structurally different from scaling-method knowledge (how to diagnose a bottleneck). Conflating them risks a Capability Framework that can describe *scaling* well but can't describe *the institutional machinery that decides what gets scaled*.

**Where it belongs:** The Capability Framework and the repository's top-level structure.

**Recommendation:** **Capability description update**, plus a structural note in FOUNDATION.md. Consider splitting the repository's organizing logic into two explicit strands — Scaling Method Knowledge and Scaling Governance Knowledge — rather than treating governance as a subtype of methodology.

---

### 9. Success stories are epistemically dangerous — and nothing yet says the repository should actively seek out failures

**What emerged:** This theme recurred more consistently than almost anything else: the Nepal case was a "success" that concealed a distributional problem; IPSR's own stated portfolio pattern is that apparent readiness conceals low actual use; and the Repository Health assessment separately noted that every case in the collection so far is a success or early-stage story — there is no documented failure. These three observations are really one idea, seen three times, and it was only ever logged as a passive "missing perspective," never stated as an active principle.

**Why it matters:** If this pattern is real — and three independent occurrences is suggestive, though still far from proof — then a repository that only accumulates success stories will systematically underrepresent exactly the kind of knowledge most useful for preventing bad outcomes. This deserves to be a standing acquisition principle, not a passive gap noted once and left alone.

**Where it belongs:** FOUNDATION.md's design principles, and the collection-priority logic that guides future ingestion.

**Recommendation:** **Design Principle**, elevated from its current status as a one-line "missing perspective" note. Something like: "Actively seek documented scaling failures and setbacks, not only successes — success narratives are the primary vector by which distributional and adoption problems go unnoticed."

---

### 10. There is no defined trust model for content the Platform itself generates

**What emerged:** "Preserve the source as authoritative" governs how the Librarian treats an external document like a CIMMYT PDF. But once Scaling Analyst and Scaling Coach exist, they will generate new content — diagnostic scores, coaching advice — that FOUNDATION.md says "becomes a new source for the Librarian to ingest." Whether that AI-generated content should be treated with the same evidentiary weight as an externally authored, published document, or whether it needs a visibly different provenance and trust marking, was never decided.

**Why it matters:** This is not a small detail. If a future Analyst output gets curated into a Knowledge Card with the same "preserve as authoritative" framing as a peer-reviewed methodology PDF, the repository would be quietly laundering machine-generated judgment into the same epistemic category as vetted external expertise. That would directly violate the evidence-informed reasoning principle already established, just through a channel nobody has examined yet.

**Where it belongs:** The Platform/Repository distinction (FOUNDATION.md Section 4) and the Librarian's Ingest procedure.

**Recommendation:** **Remain an open question, flagged as high-priority** — it should be resolved before Scaling Analyst or Scaling Coach are actually built, not after. A reasonable starting position worth testing: AI-generated content should always carry a distinct provenance tag (e.g., "Platform-generated, not independently authored") that is never allowed to read the same as an externally sourced document, no matter how it's later cited.

---

## Summary table

| # | Idea | Type |
|---|---|---|
| 1 | Escalate to companion documents when metadata is thin | Design Principle |
| 2 | Curation method matures independently of new evidence | Foundation doc update (new "Recalibrate" mode) |
| 3 | Reflect mode vs. "never prescribe" tension | Open question |
| 4 | Knowledge Card template drifting ahead of formalization | Foundation doc (new `KNOWLEDGE_CARD_TEMPLATE.md`) |
| 5 | Classification taxonomy changed mid-project | Open question, pending Curate-mode pass |
| 6 | Feedback loop is human-mediated, not automated | Design Principle + open question |
| 7 | Confidence-grading has an unaddressed scaling cost | Design Principle + open implementation question |
| 8 | Repository conflates method knowledge and governance knowledge | Capability description update |
| 9 | Success stories are epistemically dangerous | Design Principle |
| 10 | No trust model for Platform-generated content | Open question (high priority) |

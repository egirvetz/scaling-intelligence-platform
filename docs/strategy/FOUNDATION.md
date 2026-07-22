# Scaling Intelligence — Foundation Document

**Status:** Foundation Edition
**Purpose of this document:** to give anyone joining this project — human or AI — enough architectural context to continue the work without re-deriving it from scratch. It describes what Scaling Intelligence is, why it exists, what has been decided and why, what is built versus designed-but-unbuilt, and what is still genuinely open.

This document is deliberately not a transcript or a chronological record of how these ideas emerged. It is a synthesis: the architecture as it currently stands, with its reasoning made explicit.

---

## 1. Vision and Purpose

Scaling Intelligence is a living, curated knowledge system for innovation scaling — built to make the scattered, heterogeneous knowledge that already exists about how innovations reach people at scale navigable, comparable, and cumulative, rather than trapped in individual documents that get read once and filed away.

Its purpose is not to invent a new theory of scaling. It is to hold multiple existing scaling traditions — formal diagnostic methodologies, individual expert coaching practice, institutional evidence systems, portfolio governance processes — in a single, disciplined space where their agreements, disagreements, and blind spots become visible to whoever needs to make a scaling decision: a project team, a coach, a funder, or a portfolio manager.

The underlying bet is that most of the value in scaling knowledge is not inside any single document, but in the relationships between documents — and that those relationships are currently invisible because nothing is reading the whole collection at once.

## 2. The Problems It Is Trying to Solve

**Knowledge gets produced and then trapped.** Coaching assessments, workshop outputs, and methodology guides are written carefully, used once for their immediate purpose, and then sit in a folder unconnected to everything else that has ever been written on the same subject. Nothing re-reads them together.

**Different traditions reinvent the same ideas in different words, and no one notices.** Independent methodologies converge on genuinely similar principles — for example, two separate CGIAR frameworks independently arrived at the idea that the weakest element of a system, not the strongest, should drive strategy, and gave it two different names. Without a mechanism actively looking across documents, this kind of convergence (which is valuable corroborating evidence) is invisible, and contradictions are equally invisible.

**Portfolio-level decisions need comparable data, but source documents are not comparable by default.** A narrative coaching memo, a scored diagnostic workbook, and a scripted facilitation guide are all legitimate, valuable ways of capturing scaling knowledge — but a funder trying to compare twenty solution tracks cannot act on twenty different genres of document directly. Something has to translate between them without flattening what makes each one useful.

**Institutional memory decays unevenly.** A single document can contain both durable methodological insight and fast-expiring administrative detail (a deadline, a fee schedule, a named contact) bundled together. Once filed, nothing distinguishes the part that is still true from the part that quietly went stale.

**Heuristics accumulate without ever being tested.** Individual documents assert useful-sounding principles — "define a minimum viable system," "distinguish scaling out from scaling deep" — but a single source can never validate its own claim. Without a deliberate cross-source validation pathway, every heuristic stays permanently unverified, no matter how many times it is quietly true.

## 3. Major Architectural Decisions, and Why

**Original sources are preserved untouched and treated as authoritative.** All synthesis, interpretation, and cross-referencing happens in a separate curation layer (Knowledge Cards) that supplements but never replaces the source. This prevents the single most common failure mode of knowledge systems — summarization drift, where each retelling loses a little more nuance than the last — and keeps the whole system auditable back to a primary document at any time.

**Knowledge Cards are the atomic unit of curation, built on a fixed template.** Every ingested document is described through the same structure: metadata, purpose, key concepts, supported capabilities, candidate heuristics, relationships to other sources, information gaps, and a stated confidence level. A fixed template is what makes a coaching memo and a scored workbook comparable at all — without it, every new document would need its own bespoke reading.

**Every claim is graded as observed, interpreted, or hypothesized.** A statement drawn directly from a source is marked differently from a curator's synthesis, which is marked differently again from a plausible-but-unverified idea. This is not a stylistic preference — it is the mechanism that stops the repository from quietly accumulating false certainty as it grows. In a domain where documents inform real funding and program decisions, overclaiming confidence is a genuine hazard, not a theoretical one.

**Relationships between documents carry their own confidence grade.** A relationship confirmed by directly reading both documents is distinguished from one inferred from filenames or folder placement, which is distinguished again from a relationship that is explicitly flagged as unresolved. A repository that asserts two documents agree when they merely resemble each other becomes actively misleading over time; grading relationships is what prevents that.

**Classification is decided per document, with reasoning, not assigned from a fixed intake category.** Documents in this domain span genuinely different purposes and lifespans — a published methodology, a scripted operational guide, a time-bound briefing deck, a narrative coaching record — and forcing them into one scheme at intake would erase exactly the distinctions that matter later.

**Repository organization follows the Capability Framework, not the source folder structure.** Where a file happens to sit on disk reflects institutional or historical accident, not what kind of knowledge it represents. The repository needs its own logic, organized around capabilities and methodologies rather than mirroring an inherited folder tree.

**Heuristics require independent cross-source corroboration before their confidence is upgraded.** A single coaching narrative or a single methodology document can each be internally coherent and still be wrong, or simply idiosyncratic. A heuristic is only promoted from "source-specific" toward "supported by multiple sources" once a genuinely independent second source corroborates it — never on the strength of restating the same claim more confidently.

**Gaps and open questions are treated as first-class content, not omissions.** An unresolved citation lineage or an unclear organizational relationship between two programs is logged explicitly and tracked, rather than silently dropped or guessed at. This turns "we don't know yet" into an actionable repository asset instead of a dead end.

## 4. The Platform vs. the Knowledge Repositories

These are deliberately separate things, and the distinction is architectural, not cosmetic.

**The Knowledge repository** is the accumulating body of content itself: preserved source documents, the Knowledge Cards built on top of them, the graded relationships between them, and — as the collection matures — dedicated Concept Pages and Heuristic Pages. The repository is, in principle, a set of durable artifacts. It should remain valid, readable, and useful independent of any particular AI system, session, or tool.

**The Platform** is the operational machinery built around the repository: the AI roles that act on it (see Section 5), the workflows those roles follow, and eventually the interfaces through which people actually use it — asking a question, requesting coaching on a live case, running a structured diagnostic, or generating a portfolio-level view across many cases.

The reason this separation matters: the repository's integrity — fidelity to sources, honest confidence grading, explicit gaps — must never depend on any single platform component working correctly. The platform can be extended, replaced, or improved without endangering what the repository already knows. Conversely, a platform failure should never corrupt the repository; at worst, it should simply leave it un-updated.

## 5. The AI Architecture

Scaling Intelligence is designed around four distinct AI roles. As of this Foundation Edition, only the first is operational; the other three are architecturally defined but not yet built.

**Scaling Librarian — operational.**
Owns the repository's integrity. Works in four modes: *Ingest* (turn a new source into a Knowledge Card), *Curate* (review and reorganize existing holdings, find duplicates and gaps), *Refresh* (update a card when new evidence changes the picture, while preserving prior versions), and *Reflect* (synthesize across the entire repository — surfacing convergence, contradiction, and emerging patterns that no single document contains). The Librarian never prescribes a scaling strategy, evaluates a solution track, or makes a stage-gate decision. It is a curator, not an advisor — methodology-neutral by design, and bounded strictly by what the evidence in the repository actually supports.

**Scaling Analyst — designed, not yet built.**
The role that would apply a chosen methodology's scoring logic to a live, specific case — running something like a Scaling Scan ingredient assessment or an IPSR-style Innovation Readiness / Innovation Use scoring pass against a real innovation, producing structured, evidence-backed, auditable output. Where the Librarian works backward over what already exists, the Analyst would work forward on a new situation, and its output would itself become a new source for the Librarian to eventually ingest.

**Scaling Coach — partially precedented, not yet unified.**
The dialogic, advisory role: helping a team think through their specific situation the way an expert field coach or a live workshop facilitator does, drawing on the repository's accumulated heuristics rather than only producing a score. Existing coaching capabilities already reflect two different registers of this role — one modeled on narrative, judgment-driven expert coaching, and one modeled on scripted, evidence-mandated workshop facilitation — and part of the Coach's design work is deciding how, or whether, to unify these registers rather than leave them as separate practices.

**Portfolio Intelligence — designed, not yet built.**
The role that would aggregate Analyst and Coach outputs across many cases into comparable, portfolio-level views to support resource allocation and stage-gating decisions — the natural next layer above any single case's diagnosis. This is currently the platform's clearest capability gap: the repository contains only one detailed treatment of portfolio-level governance so far, and it is descriptive rather than operational.

**How the roles relate.** This is a loop, not a one-way pipeline. The Librarian curates the shared knowledge base that the Analyst and Coach both draw on when working a live case; their outputs, in turn, become new material for the Librarian to curate, which improves the base the next Analyst or Coach engagement draws on. Portfolio Intelligence sits above both, aggregating outcomes across many such engagements. The health of the whole system depends on that loop actually closing — an Analyst or Coach engagement that never makes its way back into the repository is a missed opportunity for the system to learn.

## 6. The Capability Framework, and Why It Is Central

Across every document curated so far, a recurring vocabulary of capabilities has been used to describe what each source actually supports: innovation characterization, scaling readiness, bottleneck diagnosis, scaling pathway design, last-mile delivery, business models and incentives, partnership strategy, responsible and inclusive scaling, stage-gating, coaching, portfolio intelligence, adaptive management, organizational learning, and evidence synthesis.

This shared vocabulary is what makes the repository's diversity of genres tractable at all. A coaching memo, a scored workbook, a facilitation script, and a briefing deck have almost nothing in common structurally — but each can be honestly assessed against the same capability list, which means their contributions can be compared, gaps can be identified, and coverage can be tracked as the repository grows.

The Capability Framework is not just a tagging convenience. It is the diagnostic instrument the Librarian uses, in Reflect mode, to answer questions like "which parts of scaling knowledge are well supported, and which are dangerously thin?" — and it will be the coordinate system Portfolio Intelligence eventually uses to make cross-case comparisons meaningful. It currently exists as vocabulary used consistently in practice rather than as a formally versioned, standalone artifact; formalizing it is one of the highest-priority next steps (Section 10).

## 7. Methodology Neutrality and Evidence-Informed Reasoning

**Methodology neutrality** means the system does not treat any one scaling tradition — expert field coaching, a participatory diagnostic workbook, an institutional evidence-audited system, or any other — as the correct one. Each is understood on its own terms: its intended use, its evidentiary standard, its blind spots. The system's job is to make the relationships between these traditions visible — where they converge, where they genuinely differ, where a real tension remains unresolved — not to arbitrate which is right. This stance is a design commitment, not a default: it would be easy, and wrong, for a system that spends most of its time inside one institutional ecosystem to start quietly treating that ecosystem's house methodology as ground truth.

**Evidence-informed reasoning** is the discipline that makes methodology neutrality practical rather than just aspirational. Every claim carries a grade — directly observed in a source, interpreted by curation, or hypothesized and unverified — and every relationship and heuristic carries its own confidence level, upgraded only by genuine independent corroboration. This discipline has already proven necessary in practice: real cases in this domain show that an innovation can look like an unambiguous success at the portfolio level while still concealing an uneven distribution of benefits underneath — exactly the kind of thing an overconfident synthesis would smooth over. A repository that cannot distinguish "this is stated" from "this is likely" from "this is our best guess" will eventually be wrong in ways that matter.

Together, these two commitments are what would make the repository trustworthy enough to inform real funding and program decisions in the future. The moment the system starts blending methodologies without saying so, or asserting confidence it hasn't earned, it stops being safe to use for that purpose.

## 8. Current Status — Foundation Edition

**What exists and is operational:** the Scaling Librarian, working across all four of its modes. It has completed an initial ingestion covering four structurally distinct documents — a narrative coaching assessment of a live funding decision, a formally published participatory diagnostic methodology, a scripted operational facilitation manual, and a portfolio-governance briefing presentation — and has produced one full repository-wide Reflect-mode assessment synthesizing across all of them.

**What has been established as a result:** the Knowledge Card template; the observed/interpreted/hypothesized grading discipline; a graded-relationship convention (source-confirmed, curator-inferred, or explicitly unresolved); an initial two-to-three-branch repository taxonomy proposal (Methodologies, Coaching Records, and an emerging Portfolio/Program Governance branch); an initial capability-coverage map showing where the repository is strong (bottleneck diagnosis, scaling readiness) versus weak (portfolio intelligence, last-mile delivery, organizational learning); and a running, explicit list of open questions and information gaps.

**What does not yet exist:** the Scaling Analyst, a unified Scaling Coach, and Portfolio Intelligence as platform roles; a formally versioned Capability Framework document; dedicated Concept Pages and Heuristic Pages (candidates have been identified but not yet written as standalone artifacts); any cross-source validation that would move a heuristic from source-specific to genuinely corroborated; and any representation, in the repository, of a scaling methodology from outside the CGIAR ecosystem.

This is why the project is at "Foundation Edition": the discipline, the template, and the architecture are established and have already proven their value once, but the multi-role platform and a broad, independently corroborated knowledge base are still ahead.

## 9. Major Design Principles

- Preserve the original source; never overwrite or replace it with synthesis.
- Separate observation, interpretation, and hypothesis in every piece of output, without exception.
- Grade relationships and heuristics explicitly; never assert convergence or contradiction that hasn't been checked.
- Treat gaps and open questions as first-class, trackable content rather than something to be smoothed over.
- Stay methodology-neutral: describe traditions on their own terms rather than ranking them.
- Prefer a small number of well-evidenced concepts and heuristics over a large number of thin, unverified ones.
- Let the Capability Framework, not the accident of source folder structure, define how the repository is organized.
- Design for cumulative learning: every new document should be read against everything already known, not curated in isolation.
- Close the loop: Analyst and Coach outputs should feed back into the repository the Librarian curates, not disappear after a single use.

## 10. Highest-Priority Next Steps

**Repository content:**
1. Ingest the source believed to underlie the "weakest link" principle shared across two existing methodologies in the repository, to resolve or confirm its citation lineage.
2. Ingest the primary academic source behind the Scaling Readiness Approach referenced by more than one document already in the repository, to resolve or confirm whether it is the direct basis for an existing scoring framework.
3. Ingest the referenced-but-not-yet-acquired "definitive" guidance package for the repository's most detailed operational methodology family.
4. Ingest at least one additional independent case record from the same coaching tradition already represented, specifically to test whether its heuristics recur — the only way to move them from source-specific to corroborated.
5. Ingest a primary source for the inclusion/equity-focused methodology already referenced structurally by multiple sources but not yet independently represented.

**Repository structure:**
- Formalize the Capability Framework as its own versioned document rather than consistently-used-but-implicit vocabulary.
- Create the Concept Pages and Heuristic Pages already identified as candidates, rather than leaving them logged inside individual Knowledge Cards.
- Establish a single running Open Questions Log, rather than restating the same open questions inside every new card.
- Add a formal two-part currency field for documents that mix durable and time-bound content within a single source.

**Platform:**
- Scope a minimum viable Scaling Analyst: what a first structured, evidence-graded diagnostic pass over a live case should actually output, and how it becomes a repository input.
- Decide how, or whether, to unify the two existing coaching registers into a single Scaling Coach role.
- Scope a minimum viable Portfolio Intelligence view: the smallest useful cross-case comparison the current repository could already support, even before Analyst and Coach exist.

## 11. Open Questions and Unresolved Architectural Decisions

**Content-level:**
- The exact relationship between two distinct portfolio/funding mechanisms referenced in different sources — the same mechanism under different names, nested, parallel, or genuinely unrelated — is unknown and should be clarified rather than assumed.
- Whether a specific scoring framework already in the repository is formally the same as, or only loosely inspired by, a named external academic approach remains unconfirmed.
- Whether the "minimum viable system" instinct (narrow to the smallest defensible core) and the "comprehensive coverage" instinct (score broadly across many categories before prioritizing) — both present in the repository — are genuinely competing philosophies or simply sequential steps of the same process, has not been resolved by any source read so far.

**Architecture-level:**
- How, exactly, should Analyst and Coach outputs be fed back into the Librarian's ingest pipeline? The loop is proposed conceptually (Section 5) but not designed in operational detail — what triggers ingestion, who reviews it, and at what granularity.
- How should Portfolio Intelligence aggregate confidence-graded, genuinely heterogeneous data (a narrative coaching judgment and a numerically scored diagnostic are not the same kind of input) into comparable portfolio views without silently flattening that heterogeneity?
- What is the human governance model for Refresh-mode changes the Librarian proposes? The current practice is to log recommended updates rather than apply them automatically, but who reviews and approves them, and on what cadence, is not yet defined.
- Does methodology neutrality hold up once the repository grows beyond the small number of closely related traditions it currently contains? The principle is easy to state with three related CGIAR-adjacent traditions; it has not yet been tested against a genuinely different, unrelated scaling tradition.

## 12. Lessons Learned During the Design Process

**Cross-document relationships are where the real value shows up — and where overclaiming is easiest.** The single most useful finding to come out of the initial ingestion was a relationship between two documents that neither document stated itself. That same process, done carelessly, could just as easily have manufactured a false connection. The discipline of grading every relationship by confidence turned out to be load-bearing, not optional polish.

**Sources in this domain vary enormously in evidentiary rigor, even within the same institutional family.** One methodology in the repository mandates evidence for every score and defaults to the lowest defensible level when evidence is thin; a sibling methodology from the same ecosystem is self-scored by design, with no equivalent audit mechanism. Treating every source as equally authoritative simply because it is "about scaling" would have been a mistake.

**Single-source metadata is often incomplete, and completing it requires actively seeking companion context.** At least one operationally important document had no stated author and no citations at all; understanding it properly required deliberately locating and reading a separate companion document, not just processing the file in isolation. The Librarian's job includes actively seeking that context, not passively waiting for it to be provided.

**A single document can be simultaneously durable and time-bound.** A methodology briefing that permanently clarified an important scoring framework's origin also contained hard deadlines that had already passed by the time it was reviewed. A single "current" or "historical" label was not adequate to describe that document honestly — the repository needed a more nuanced model almost immediately, not eventually.

**Insight compounds only when new material is read against everything already known.** Every genuinely valuable finding in this project so far came from holding multiple sources together, not from any single document read in isolation. This is the core justification for keeping the whole repository, not just the newest addition, in view at every stage of curation — and it is the reason Reflect mode exists as a first-class operation rather than an occasional afterthought.

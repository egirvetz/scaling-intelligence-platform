# Scaling Intelligence — Repository Knowledge Standard

**Document:** Canonical Knowledge Card & Repository Ingestion Specification
**Version:** 0.9 (DRAFT — proposed for ratification)
**Status:** Awaiting review by Evan / human reviewer
**Authors:** Scaling Librarian + Scaling Analyst (Knowledge Development Team)
**Applies to:** All knowledge objects entering the Scaling Intelligence Repository
**Supersedes:** none (first standard)

> **Governance note.** This document is a *working proposal*. Nothing here is canonical until you ratify it. Once ratified, this file becomes `/_standards/KNOWLEDGE_STANDARD.md` and its version becomes the reference every card must declare compliance with (`schema_version`).

---

## 0. How to read this document

Sections 1–8 map directly to your eight requests:

1. Knowledge Card schema → **§2**
2. Metadata fields → **§3**
3. Repository taxonomy → **§4**
4. Cross-linking standards → **§5**
5. Citation and provenance standards → **§6**
6. Naming conventions → **§7**
7. Versioning recommendations → **§8**
8. Quality-assurance acceptance criteria → **§9**

Before those, **§1** resolves one architectural question that everything else depends on, and which the Librarian and Analyst disagreed on. **§10** surfaces the remaining open disagreements so you can adjudicate. **§11** is a filled worked example. **§12** is the decisions we need from you.

Throughout, claims are tagged in the team's evidentiary register: **[Observed]** (grounded in repository files), **[Interpretation]**, **[Hypothesis]**, **[Recommendation]**.

---

## 1. The Knowledge Object Model (the decision that governs everything else)

**[Observed]** The two skill definitions already name a *family* of object types, not just one: the Analyst's inputs list Knowledge Cards, Concept Pages, Heuristic Pages, Evidence Records, methodology profiles, coaching-case records, portfolio summaries, capability definitions, open-question logs, and prior synthesis outputs.

**[Interpretation]** A repository that scales to thousands of objects cannot make "Knowledge Card" mean everything. If one card type has to hold a raw PDF's provenance *and* a cross-source synthesized heuristic, it will collapse under its own ambiguity by the low hundreds. The single most important standards decision is therefore to **separate source-anchored objects from synthesis-derived objects**.

We propose a two-layer model:

**Layer A — Source-anchored objects (one source ↔ one object).** These preserve fidelity to a single primary source. Provenance is simple and permanent because each object points back to exactly one archived source.

- **Knowledge Card (KC)** — the atomic unit; a structured representation of one source.

**Layer B — Synthesis-derived objects (many sources → one object).** These are built *by reading across* Layer A. They carry confidence ratings; KCs generally do not (see §10.2).

- **Concept Page (CP)** — a definition and current understanding of one concept, drawing on multiple KCs.
- **Heuristic Page (HP)** — a decision rule or rule-of-thumb, with the evidence for and against it.
- **Evidence Record (ER)** — a focused dossier assessing the evidence for a single proposition.
- **Methodology Profile (MP)** — a structured profile of one methodology (IPSR, Scaling Scan, etc.).
- **Coaching Case (CC)** — a record of one coaching engagement / applied case.
- **Portfolio Summary (PS)** — portfolio-level intelligence across many innovations.
- **Capability Definition (CD)** — the canonical definition of one capability from `Capabilities.md`.
- **Insight Page (IN)** — a reusable cross-source finding (Analyst's `INSIGHT_TEMPLATE`).
- **Open Question (OQ)** — a logged unresolved question / research need.

**[Recommendation]** Ratify the two-layer model. This spec fully specifies the **Knowledge Card (KC)** now, because that is what the first ingestion needs, and it defines the shared conventions (metadata, taxonomy, linking, provenance, naming, versioning, QA) that *all* object types inherit. Layer B object schemas are stubbed in §13 and specified in follow-up passes so we don't block the first ingestion.

**Why this matters for the KC specifically:** because synthesis lives in Layer B, the Knowledge Card can stay disciplined — it reports *what one source says*, not *what the repository concludes*. That keeps provenance clean (Librarian's priority) while still feeding synthesis (Analyst's priority). This is the compromise that resolves the granularity dispute in §10.1.

---

## 2. Knowledge Card schema

A Knowledge Card is a single UTF-8 Markdown file with two parts: **YAML frontmatter** (machine-readable metadata, §3) and a **structured body** (human-readable, sectioned below). Every section header below is required; a section with no content must contain the literal token `None recorded` (not be deleted), so absence is auditable rather than ambiguous.

### 2.1 Body structure (required sections, in order)

```
# <Title>

## 1. Source Summary
2–5 sentence neutral description of what the source is and what it claims to do.
Descriptive, not evaluative. [Observed]-level fidelity only.

## 2. Provenance
Full citation, source location in /sources, access date, and integrity hash (see §6).
This section is IMMUTABLE after acceptance except by formal supersession.

## 3. Key Claims
A numbered list. Each claim is one atomic assertion, each tagged with:
  - evidence_type (controlled vocab, §4.5)
  - source_locator (page / section / figure — §6.3)
  - claim_register: Observed | Interpretation-by-author | Hypothesis-by-author
Claims record what the SOURCE asserts. They are not the repository's judgment.

## 4. Definitions & Key Terms
Terms the source introduces or uses distinctively, verbatim or closely paraphrased,
each with a source_locator. Feeds Concept Pages.

## 5. Methods & Evidence Base
How the source generated its claims (study design, data, n, geography, timeframe).
This is what lets the Analyst later assess evidence strength without re-reading the PDF.

## 6. Scope & Boundary Conditions
Where the source says (or clearly implies) its claims do and do not apply:
geography, sector, scale stage, institution type, innovation type.

## 7. Relationship to Capabilities & Stages
Which capabilities (Capabilities.md) and stages (Three_Stages.md) this source informs,
with a one-line rationale per link. Drives faceted retrieval.

## 8. Cross-References
Typed links to other objects (§5). Bidirectional integrity is the Librarian's duty.

## 9. Curator Notes & Open Questions
Explicitly separated from source content. Anything the curator interprets, doubts,
or flags for follow-up. New OQ objects are spawned from here.

## 10. Change Log
Reverse-chronological version history (§8).
```

### 2.2 Firewall between source and interpretation

**[Recommendation]** Sections 1–6 are the **source firewall**: they may contain only what the source says, at fidelity. Interpretation, cross-source comparison, confidence judgments, and doubts live in **§9 Curator Notes** or migrate to Layer B objects. This is a hard rule, and it is checked at the QA gate (§9). It is the mechanism that lets us "distinguish source evidence from interpretation" as a *file structure*, not just a good intention.

---

## 3. Metadata fields (YAML frontmatter)

Every field's controlled vocabulary is defined in §4. `M` = mandatory at acceptance, `R` = recommended, `O` = optional.

| Field | Req | Type | Notes |
|---|---|---|---|
| `id` | M | string | Immutable object ID, e.g. `KC-0001` (§7.2). Never reused, never renumbered. |
| `schema_version` | M | string | Version of THIS standard the card complies with, e.g. `0.9`. |
| `title` | M | string | Human-readable, descriptive. |
| `object_type` | M | enum | `knowledge-card` for KCs (full list §4.1). |
| `status` | M | enum | Lifecycle state (§8.3). |
| `card_version` | M | semver | Version of this card's content (§8.1). |
| `created` | M | date | ISO 8601 `YYYY-MM-DD`. |
| `updated` | M | date | ISO 8601. |
| `curator` | M | string | Who created/last edited (person or agent role). |
| `source_type` | M | enum | Nature of the source (§4.4). |
| `authors` | M | list | Source authors/originating org. |
| `publication_year` | R | integer | |
| `publisher` | R | string | Journal, org, program. |
| `source_locator` | M | object | `{url, doi, archived_path, access_date, integrity_hash}` (§6). |
| `capabilities` | M | list<enum> | From Capabilities.md controlled list (§4.2). ≥1 required. |
| `stages` | M | list<enum> | From Three_Stages + `cross-stage` (§4.3). ≥1 required. |
| `methodology_family` | R | list<enum> | (§4.6). Use `none`/`general` if not methodology-specific. |
| `evidence_types` | M | list<enum> | Distinct evidence types present in the source (§4.5). |
| `geography` | R | list | ISO country codes or region tags; `global` allowed. |
| `sector` | R | list | e.g. `agriculture`, `climate`, `nutrition`. |
| `aow` | R | list<enum> | S4I Area of Work tags (§4.7). |
| `tags` | O | list | Free keywords for discovery; NOT a substitute for controlled facets. |
| `related` | R | list<link> | Typed cross-links (§5). |
| `supersedes` | O | id | KC this replaces. |
| `superseded_by` | O | id | Set when deprecated. |
| `review_due` | R | date | Freshness trigger (§8.4). |
| `confidence` | — | — | **Omitted on KCs by default** (see §10.2). Present on Layer B objects. |

**[Recommendation]** Machine-validate frontmatter against a schema file (`/_standards/kc.schema.json`) so a card with a typo'd capability or missing mandatory field fails ingestion automatically rather than silently polluting the taxonomy. This is what makes the standard survive to thousands of objects. **[Hypothesis]** Manual discipline alone will not hold past ~150 objects.

---

## 4. Repository taxonomy (faceted, not hierarchical)

**[Interpretation]** A single folder tree cannot express that one source is simultaneously about *Delivery Systems*, at the *Transition-to-Scale* stage, from a *peer-reviewed* source, in the *IPSR* family. We therefore recommend a **faceted taxonomy**: objects live in one folder by type, and are classified along several independent controlled-vocabulary facets in metadata. Retrieval is by facet query, not by folder browsing.

### 4.1 Facet: Object type (folder-determining)
`knowledge-card`, `concept-page`, `heuristic-page`, `evidence-record`, `methodology-profile`, `coaching-case`, `portfolio-summary`, `capability-definition`, `insight-page`, `open-question`.

### 4.2 Facet: Capability (controlled — anchored to `Capabilities.md`) **[Observed]**
*Pathway:* `innovation-characterization`, `scaling-readiness`, `scaling-strategy`, `business-models`, `delivery-systems`, `last-mile-delivery`, `partnerships`, `institutionalization`, `finance-readiness`, `policy-engagement`.
*Intelligence:* `coaching`, `stage-gating`, `portfolio-management`, `adaptive-learning`, `knowledge-management`, `monitoring-and-learning`, `evidence-synthesis`.
*Cross-cutting:* `responsible-scaling`, `gender-and-social-inclusion`.

> This list is the *current* controlled vocabulary. Adding a capability is a governed act (§9.4) that updates both `Capabilities.md` and this vocabulary in lockstep — never an ad-hoc tag.

### 4.3 Facet: Scaling stage (controlled — anchored to `Three_Stages.md`) **[Observed]**
`proof-of-concept`, `transition-to-scale`, `scaling`, `cross-stage`.

### 4.4 Facet: Source type (controlled)
`peer-reviewed`, `grey-literature`, `framework-or-methodology`, `case-study`, `tool-or-template`, `evaluation-or-review`, `dataset`, `expert-input`, `internal-document`, `presentation`.

### 4.5 Facet: Evidence type (controlled — adopted from Analyst skill) **[Observed]**
`conceptual-argument`, `methodological-design`, `expert-judgment`, `participant-self-assessment`, `monitoring-data`, `independently-validated-outcome`, `comparative-evidence`, `portfolio-level-evidence`.

> This is the single most valuable facet for the Analyst. It is what allows evidence strength to be assessed *later* without re-reading the source, and what prevents "a methodology says X" from being mistaken for "X is validated."

### 4.6 Facet: Methodology family (controlled, extensible)
`ipsr`, `scaling-scan`, `aiccra-scaling-framework`, `genderup`, `responsible-scaling`, `kohl-systems-approach`, `paass`, `link-methodology`, `general`, `none`.

### 4.7 Facet: S4I Area of Work (controlled) **[Observed — from project instructions]**
`aow1`, `aow2`, `aow3`, `aow4`. Respect boundary rules: a card may be *tagged* with an AoW it informs, but tagging does not assert delivery responsibility.

### 4.8 Facets: Geography / Sector (open but normalized)
Geography uses ISO 3166 codes or a short region controlled list (`ssa`, `south-asia`, `latam`, `global`). Sector uses a short controlled list, extensible by governance.

---

## 5. Cross-linking standards

**[Interpretation]** Links are where a document archive becomes a *knowledge system*. Untyped links ("see also") do not support synthesis; typed, directional links do.

### 5.1 Link record format
Every entry in `related:` is an object:
```yaml
related:
  - target: CP-0007
    type: describes
    note: "Source is a primary reference for the Scaling Readiness concept."
```

### 5.2 Controlled relation types
| Type | Meaning | Typical direction |
|---|---|---|
| `derived_from` | This object was built from that source | Layer B → KC |
| `describes` | KC is a primary source for a concept/heuristic | KC → CP/HP |
| `supports` | Provides evidence for the target proposition | KC/ER → HP/CP |
| `contradicts` | Provides evidence against the target | KC/ER → HP/CP |
| `refines` | Qualifies / adds boundary conditions to target | any |
| `relates_to` | Associative, non-committal (use sparingly) | any |
| `part_of` | Component of a larger work already in repo | KC → KC |
| `supersedes` / `superseded_by` | Version replacement | KC → KC |
| `applies_to_capability` | Links to a Capability Definition | any → CD |
| `applies_to_stage` | Links to a stage | any → stage |
| `cites` | The source cites another source in the repo | KC → KC |

### 5.3 Bidirectional integrity
**[Recommendation]** Links are declared once, on the *asserting* object, but the reciprocal must be materialized on the target (`describes` ↔ `described_by`). Maintaining reciprocals is a **Librarian duty** and a QA-gate check. **[Recommendation]** Generate a link-graph index (`/_index/links.json`) so dangling links (pointing at a non-existent or deprecated ID) are detected automatically.

### 5.4 Inline references
In body prose, reference other objects by ID in double brackets: `[[KC-0001]]`, `[[CP-0007]]`. A renderer/index resolves these to titles. IDs, never titles, are the anchor — titles change, IDs never do.

---

## 6. Citation & provenance standards

**[Observed]** Core Librarian mandate: *"the original source is authoritative"* and *"provenance is never lost."* These rules operationalize it.

### 6.1 Preserve the original, immutably
1. Every ingested source is archived **verbatim** in `/sources/` — the exact file received, unmodified.
2. The archived filename embeds the KC ID: `/sources/KC-0001__<slug>.<ext>` (§7).
3. The source file is **read-only / append-only**. It is never edited, reformatted, or "cleaned." Derived/cleaned text lives elsewhere and links back.
4. If the source is a URL with no downloadable artifact, archive a captured snapshot (PDF/HTML) *and* record the live URL. **[Recommendation]** Never rely on a live URL as the sole provenance — link rot is guaranteed at scale.

### 6.2 Integrity hash
`integrity_hash` in `source_locator` stores a SHA-256 of the archived file. This proves the object still describes the exact bytes it was curated from, and detects silent substitution. **[Recommendation]** Compute at ingestion; re-verify during freshness reviews.

### 6.3 Claim-level source locators
Every claim in body §3 and every term in §4 carries a `source_locator` fine enough to find it in the original: `p.14`, `§3.2`, `Fig.4`, `Table 2`, `00:12:30` (for media). **[Interpretation]** Without claim-level locators, verification at the thousand-object scale becomes re-reading whole PDFs — the exact failure mode this repository exists to prevent.

### 6.4 Citation format
Store structured citation in frontmatter (author/year/title/publisher/DOI) so any human-readable style (APA, Chicago) can be rendered on demand. **[Recommendation]** Do not hand-format citation strings into the body; render them from structured fields to keep them consistent across thousands of cards.

### 6.5 Secondary sources
If the ingested source is itself a summary of other work, tag `source_type: grey-literature` (or as appropriate) and set claim `claim_register` to reflect that the underlying evidence is *reported, not observed here*. Spawn an Open Question to trace primary evidence when a claim matters. **[Recommendation]** Never let a secondary source's confidence launder into the repository as if primary.

---

## 7. Naming conventions

### 7.1 Principle
**[Recommendation]** Two identifiers per object: a **stable opaque ID** (never changes, machine anchor) and a **human slug** (readable, may be corrected). Filenames combine both; all internal links use the ID only.

### 7.2 Object IDs
Format: `<TYPE>-<NNNN>` — type prefix + zero-padded sequential integer.
`KC` knowledge-card · `CP` concept-page · `HP` heuristic-page · `ER` evidence-record · `MP` methodology-profile · `CC` coaching-case · `PS` portfolio-summary · `CD` capability-definition · `IN` insight-page · `OQ` open-question.
Example: `KC-0001`. IDs are assigned once, **never reused and never renumbered**, even after deprecation. 4 digits now; widen to 5 before 10,000 objects (**[Hypothesis]** sufficient headroom for the alpha).

### 7.3 Slugs
Lowercase, hyphenated, ASCII, ≤ 60 chars, derived from title + a disambiguator (lead author + year for sources): `scaling-readiness-sartas-2020`. Slugs may be corrected without changing the ID.

### 7.4 Filenames
`<ID>__<slug>.md` for objects; `<ID>__<slug>.<ext>` for archived sources.
Double underscore separates ID from slug (single-underscore-safe within each). Example object: `KC-0001__scaling-readiness-sartas-2020.md`.

### 7.5 Folders
```
/repository
  /_standards        # this spec, controlled vocabularies, JSON schemas, templates
  /_index            # generated: link graph, facet indexes, ID registry
  /sources           # immutable primary sources (verbatim)
  /knowledge-cards   # KC
  /concepts          # CP
  /heuristics        # HP
  /evidence          # ER
  /methodologies     # MP
  /cases             # CC
  /portfolio         # PS
  /capabilities      # CD
  /insights          # IN
  /open-questions    # OQ
```
**[Recommendation]** Keep folders flat within each type (no nested sub-topics). Topic navigation is a *facet query*, not a folder path — this is what prevents the folder tree from ossifying as the repository grows.

---

## 8. Versioning

### 8.1 Card content versioning (SemVer)
`card_version: MAJOR.MINOR.PATCH`.
- **MAJOR** — meaning-changing correction: a claim was wrong, mis-attributed, or the source was re-interpreted. Anything relying on the old reading must be revisited.
- **MINOR** — additive: new claims/links/tags extracted, no existing content invalidated.
- **PATCH** — cosmetic: typos, formatting, slug fixes.

### 8.2 Schema vs. card version
`schema_version` (this standard) and `card_version` (this card's content) are independent. A standard upgrade may require a migration pass that bumps cards' `schema_version` without touching `card_version`.

### 8.3 Status lifecycle
`draft` → `in-review` → `accepted` → (`needs-refresh` ⇄ `accepted`) → `deprecated` / `superseded`.
Only `accepted` objects are treated as canonical by the Analyst. `draft`/`in-review` are visible but flagged non-authoritative. `deprecated`/`superseded` are **never deleted** (provenance is permanent) but excluded from default synthesis and marked with `superseded_by`.

### 8.4 Freshness
`review_due` sets a re-verification date. On review: re-check the integrity hash, confirm the source still says what §3 claims, refresh links. **[Recommendation]** Default horizons: methodologies/frameworks 24 months; empirical/portfolio data 12 months; foundational concepts 36 months. Tune later against real churn.

### 8.5 Change log
Body §10 mirrors, in human-readable form, each version bump: date, version, curator, one-line reason. The immutable §2 Provenance block is exempt from ordinary edits — correcting provenance is always a MAJOR bump with an explicit log entry.

---

## 9. Quality-assurance acceptance gate

A card is `accepted` only when **every** check passes. This is the gate that protects the repository at scale.

### 9.1 Structural
- [ ] Frontmatter validates against `kc.schema.json`; all `M` fields present.
- [ ] `id` unique and correctly formatted; filename matches `<id>__<slug>.md`.
- [ ] All ten body sections present (empty ones carry `None recorded`).
- [ ] `schema_version` matches the current ratified standard.

### 9.2 Provenance & fidelity (Librarian sign-off)
- [ ] Source archived verbatim in `/sources`; `integrity_hash` recorded and verified.
- [ ] Full structured citation present.
- [ ] Every §3 claim and §4 term has a source_locator.
- [ ] Source firewall intact: §1–6 contain no interpretation, comparison, or confidence.
- [ ] No claim overstates the source (spot-check locators against the original).

### 9.3 Synthesis integrity (Analyst sign-off)
- [ ] Each claim tagged with a valid `evidence_type`; methodology claims not dressed as outcome evidence.
- [ ] ≥1 capability and ≥1 stage tagged, each with a rationale in §7.
- [ ] Cross-links use controlled relation types and resolve to existing objects.
- [ ] Boundary conditions (§6) stated or explicitly `None recorded`.
- [ ] Curator interpretation confined to §9; open questions logged as OQ objects where material.

### 9.4 Governance
- [ ] No new capability/stage/methodology value introduced without a paired update to the controlled vocabulary and `Capabilities.md`.
- [ ] Reciprocal links materialized on targets; link index has no new dangling references.
- [ ] `status` set; `review_due` set.

**[Recommendation]** Require **dual sign-off**: Librarian attests fidelity (§9.2), Analyst attests synthesis integrity (§9.3). Record both in §10. **[Interpretation]** Splitting the sign-off is what keeps the two roles honest against each other — the Librarian catches over-claiming, the Analyst catches un-usable-for-synthesis cards.

---

## 10. Surfaced disagreements (for your adjudication)

Per the team charter, we preserve rather than paper over disagreements.

### 10.1 Card granularity — one card per *source* vs one card per *claim/concept*
- **Analyst's position:** synthesis is easiest when the atomic unit is a claim or concept, so cards should be fine-grained.
- **Librarian's position:** provenance is only clean when one object maps to one source; claim-level cards multiply provenance surfaces and invite drift from the original.
- **Resolution reached (proposed):** the two-layer model (§1). KCs are **one-per-source** (Librarian wins on the atomic unit); claim/concept-level synthesis lives in Layer B objects that *link back* to KC claims via `source_locator` (Analyst gets fine-grained synthesis without sacrificing provenance). **We believe this resolves the dispute; confirm.**

### 10.2 Confidence ratings on Knowledge Cards
- **Analyst's position:** confidence levels are core to the skill and should travel with knowledge.
- **Librarian's position:** confidence is a *cross-source synthesis judgment*, not a property of a single source; putting it on a KC misrepresents an assertion as an assessment.
- **Resolution reached (proposed):** KCs carry `evidence_type` (a factual property of the source) but **not** `confidence`. Confidence lives on Layer B objects (ER/HP/CP/IN), which is where cross-source judgment legitimately happens. **Unresolved if you want at-a-glance confidence on sources — flag it.**

### 10.3 Freshness horizons
Both roles agree freshness matters; the specific horizons in §8.4 are **[Hypothesis]**, not evidence-based. Flagged as tunable, not settled.

---

## 11. Worked example (illustrative — fictional source, for format only)

```markdown
---
id: KC-0001
schema_version: "0.9"
title: "Scaling Readiness: concept, methodology, and application"
object_type: knowledge-card
status: accepted
card_version: 1.0.0
created: 2026-07-13
updated: 2026-07-13
curator: scaling-librarian
source_type: peer-reviewed
authors: ["Sartas, M.", "et al."]
publication_year: 2020
publisher: "Agricultural Systems"
source_locator:
  url: "https://example.org/scaling-readiness"
  doi: "10.0000/example.2020"
  archived_path: "/sources/KC-0001__scaling-readiness-sartas-2020.pdf"
  access_date: 2026-07-13
  integrity_hash: "sha256:PLACEHOLDER_AT_INGESTION"
capabilities: ["scaling-readiness", "innovation-characterization", "scaling-strategy"]
stages: ["cross-stage"]
methodology_family: ["general"]
evidence_types: ["conceptual-argument", "methodological-design", "case-study" ]
geography: ["ssa", "global"]
sector: ["agriculture"]
aow: ["aow2"]
tags: ["readiness", "innovation-packages", "bottlenecks"]
related:
  - target: CD-0002
    type: applies_to_capability
    note: "Primary reference for the Scaling Readiness capability definition."
review_due: 2028-07-13
---

# Scaling Readiness: concept, methodology, and application

## 1. Source Summary
Introduces "scaling readiness" as a diagnostic combining an innovation's maturity
with its use, applied to innovation packages rather than single technologies. [p.1–2]

## 2. Provenance
Sartas, M. et al. (2020). *Scaling Readiness*... DOI 10.0000/example.2020.
Archived: /sources/KC-0001__scaling-readiness-sartas-2020.pdf.
Accessed 2026-07-13. SHA-256: <hash>.  [IMMUTABLE]

## 3. Key Claims
1. Scaling readiness = innovation readiness × innovation use.
   [evidence_type: conceptual-argument] [loc: p.4] [register: Interpretation-by-author]
2. Scaling requires characterizing the innovation *package*, not the core technology alone.
   [evidence_type: conceptual-argument] [loc: p.5] [register: Observed]
...

## 4. Definitions & Key Terms
- Innovation readiness — demonstrated maturity of an innovation. [loc: p.4]
- Innovation use — extent of use by intended users. [loc: p.4]

## 5. Methods & Evidence Base
Conceptual synthesis plus illustrative application cases; no controlled outcome study. [p.6–9]

## 6. Scope & Boundary Conditions
Framed for agricultural R&D in CGIAR-type systems; transferability beyond stated. [p.10]

## 7. Relationship to Capabilities & Stages
- scaling-readiness — source is a foundational reference. 
- cross-stage — readiness is assessed at every stage.

## 8. Cross-References
- describes → CD-0002 (Scaling Readiness capability)

## 9. Curator Notes & Open Questions
Analyst note: claims are conceptual/methodological, not outcome-validated — do not cite as
evidence that scaling readiness *improves* outcomes. OQ-0001 spawned to seek such evidence.

## 10. Change Log
- 2026-07-13 · 1.0.0 · scaling-librarian · Initial ingestion. Librarian ✓ / Analyst ✓.
```

---

## 12. Decisions we need from you

1. **Ratify the two-layer object model** (§1), or keep everything as one card type?
2. **Confidence on KCs** (§10.2): accept "no confidence on KCs," or require an at-a-glance confidence field?
3. **Machine validation** (§3, §9): commit to JSON-schema validation + a link index, or start manual and add tooling later?
4. **Folder architecture** (§7.5): adopt as proposed?
5. **Freshness horizons** (§8.4): accept the proposed defaults as provisional?
6. Any **house citation style** or existing card format we must conform to?

On your ratification, we will (a) finalize this as `/_standards/KNOWLEDGE_STANDARD.md v1.0`, (b) generate `kc.schema.json` and the controlled-vocabulary files, and (c) proceed to the first ingestion against the ratified standard. *(Reminder: I have read-only access to the repository, so "finalize" means I produce the files for you to commit.)*

---

## 13. Deferred (stubs for follow-up passes)
Layer B schemas — Concept Page, Heuristic Page, Evidence Record, Methodology Profile, Coaching Case, Portfolio Summary, Capability Definition, Insight Page, Open Question — inherit all shared conventions (§3–§9) and add type-specific body sections (e.g., HP: the rule, conditions, supporting/contradicting evidence, confidence; ER: proposition, evidence for/against, independence, confidence, what-would-change-it). Specified after the KC standard is ratified so the first ingestion is not blocked.

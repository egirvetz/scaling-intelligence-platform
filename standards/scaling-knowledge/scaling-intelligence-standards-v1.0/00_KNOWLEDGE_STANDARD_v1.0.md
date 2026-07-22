# Scaling Intelligence — Knowledge Standard

**Document:** Canonical Knowledge Standard for the Scaling Intelligence Graph
**Version:** 1.0-rc1 (Release Candidate — decisions 1–7 ratified; awaiting final ratification)
**Status:** Release Candidate for review by Evan / human reviewer
**Authors:** Scaling Librarian + Scaling Analyst (Knowledge Development Team)
**Applies to:** Every object (node) and relationship (edge) in the Scaling Intelligence Graph
**Supersedes:** Knowledge Card Specification v0.9 (DRAFT); Knowledge Standard v1.0 (draft)

> **Governance note.** On final ratification this becomes `/_standards/KNOWLEDGE_STANDARD.md` (tagged `v1.0`). `schema_version` in nodes tracks the ratified line (`"1.0"`); this document is `v1.0-rc1` until ratified. Claude has read-only access to the repository; "finalize" means the team hands you validated files to commit.
>
> **Decisions ratified (this RC).** (1) Practical Implications required, with a permitted no-implication phrase and interpretation labeling (§4.4); (2) entity nodes architecturally reserved but **not mandatory** during initial ingestion (§9); (3) graph-first architecture kept; (4) Source vs Evidence Confidence kept (§7); (5) ontology governed-but-evolving kept (§5); (6) provenance firewall + validation kept; (7) AI-ready architecture kept (§8.2).

---

## 0. What changed from v0.9 → v1.0

This version keeps every ratified v0.9 decision (two-layer architecture, provenance-first, controlled taxonomy, QA gate, machine validation, dual sign-off) and incorporates seven strategic refinements you directed:

1. **Mental model shifted from *repository* to *graph*** (§1). Nodes and edges are now the primitives; cards are nodes.
2. **Capabilities and the wider ontology are now *governed but evolving*** (§5), with a discovery-and-promotion lifecycle.
3. **Source Confidence is split from Evidence Confidence** (§7). Source Confidence lives on the Knowledge Card; Evidence Confidence stays in Layer B.
4. **A required *Practical Implications* ("So what?") section** is added to every Knowledge Card (§4.4).
5. **AI-readiness metadata** is reserved now so it is cheap to populate later (§8).
6. **Future first-class entity node types** (People, Organizations, Solution Tracks, etc.) are architected for (§9).
7. **A long-term Operating System vision** is stated as the standing evaluation lens for every design decision (§12).

---

## 1. The Scaling Intelligence Graph (mental model)

**[Recommendation — ratified in principle]** We are not building a document repository. We are building a **Scaling Intelligence Graph**: a connected, evolving system in which knowledge and the entities scaling acts upon are all first-class **nodes**, joined by typed, directional **edges**.

- A **node** is any addressable object with a stable ID: a Knowledge Card, a Concept, an Evidence Record, a Heuristic, and — in future versions — a Person, Organization, Project, Country, Technology, Innovation Package, Solution Track, Scaling Partnership (§9).
- An **edge** is a typed relationship between two nodes (`supports`, `contradicts`, `derived_from`, `works_on`, `operates_in` …), carrying its own attributes (§6).
- The **Markdown files are the serialization** of the graph, not the graph itself. The graph is materialized in `/_index/graph/` from node frontmatter + edges, and is what powers retrieval, synthesis, and (later) AI reasoning.

**[Interpretation]** Every downstream design choice in this document is justified by one test: *does it make the graph richer, more traversable, and more trustworthy over time?* Provenance keeps nodes trustworthy; typed edges make the graph traversable; the evolving ontology (§5) lets it grow richer without losing control.

**Two classes of node** — worth naming now because they behave differently:

| Class | Examples | Anchored to | Carries |
|---|---|---|---|
| **Knowledge nodes** | Knowledge Card, Concept, Heuristic, Evidence Record, Insight, Open Question, Methodology Profile, Coaching Case, Portfolio Summary | a source or a synthesis | provenance and/or confidence |
| **Entity nodes** (future, §9) | Person, Organization, Project, Country, Program, Technology, Innovation Package, Solution Track, Scaling Partnership | the real world | identity attributes, not claims |

The Knowledge Card is the first node type fully specified here because it is what the first ingestion needs. All other node types inherit the shared conventions (§6–§11).

---

## 2. Two-layer knowledge architecture (retained from v0.9)

**Layer A — Source-anchored nodes (one source ↔ one node).** Preserve fidelity to a single primary source; provenance is simple and permanent.
- **Knowledge Card (KC)** — the atomic knowledge node; a structured representation of one source.

**Layer B — Synthesis-derived nodes (many sources → one node).** Built by reading *across* Layer A; carry Evidence Confidence.
- **Concept Page (CP)**, **Heuristic Page (HP)**, **Evidence Record (ER)**, **Methodology Profile (MP)**, **Coaching Case (CC)**, **Portfolio Summary (PS)**, **Capability Definition (CD)**, **Insight Page (IN)**, **Open Question (OQ)**.

**[Interpretation]** In graph terms: Layer A nodes are grounded to the world through sources; Layer B nodes are grounded to Layer A through edges. This is what lets synthesis be fine-grained *and* fully traceable — the Analyst's fine-grained claim is always one edge away from the exact page in the exact source the Librarian archived.

---

## 3. Knowledge Card — anatomy (two zones)

A Knowledge Card is a UTF-8 Markdown file: **YAML frontmatter** (§8) plus a **structured body** organized into two explicitly separated zones.

### Zone A — Source Fidelity (the source firewall)
May contain **only what the source says**. No interpretation, no cross-source comparison, no repository judgment. Immutable in spirit; the Provenance block is immutable in fact (§10).

### Zone B — Curated Intelligence (clearly labeled interpretation)
Everything the team *adds*: practical implications, curator notes, the rationale on each edge. All Zone B content is understood to be interpretation and is quarantined from Zone A.

> **[Interpretation]** The two-zone body is the structural expression of the whole project's founding tension — *preserve the source* (Zone A, Librarian) vs *extract usable intelligence* (Zone B, Analyst). We do not resolve the tension by choosing a side; we resolve it by giving each side its own zone and a hard wall between them, checked at the QA gate.

### 3.1 Required body sections (in order)

```
# <Title>

—— ZONE A: SOURCE FIDELITY (only what the source says) ——

## 1. Source Summary
## 2. Provenance                         [IMMUTABLE after acceptance]
## 3. Key Claims                         [each: evidence_type, source_locator, register]
## 4. Definitions & Key Terms
## 5. Methods & Evidence Base
## 6. Scope & Boundary Conditions

—— ZONE B: CURATED INTELLIGENCE (clearly-labeled interpretation) ——

## 7. Practical Implications ("So what?")   [NEW in v1.0 — required, see §4.4]
## 8. Relationship to Capabilities & Stages
## 9. Graph Edges (Cross-References)
## 10. Curator Notes & Open Questions
## 11. Change Log
```

Every section is required. An empty section carries the literal token `None recorded` so absence is auditable.

---

## 4. Section rules of note

### 4.1 Key Claims (§3 of body)
A numbered list of atomic assertions. Each claim carries `evidence_type` (§5.5 vocab), `source_locator` (§ page/figure), and `register` ∈ {Observed, Interpretation-by-author, Hypothesis-by-author}. **Claims record what the source asserts — never the repository's judgment.**

### 4.2 Methods & Evidence Base (§5 of body)
How the source generated its claims (design, data, n, geography, timeframe). This is what lets the Analyst assess Evidence Confidence *later, in a Layer B node,* without re-reading the source.

### 4.3 Source firewall enforcement
Zone A sections (body §1–6) must contain no interpretation. This is a hard QA check (§11). Violations are the single most common way provenance quietly degrades at scale.

### 4.4 Practical Implications — the required "So what?" (NEW)
**[Recommendation]** Every Knowledge Card must state how the source *could* inform scaling decisions. This is Zone B (interpretation), clearly labeled, and never mixed into Zone A. It is structured by decision context so the graph can route a card to the right use:

```
## 7. Practical Implications ("So what?")
Register: Interpretation by curator — NOT source content.

- Coaching:              how could this inform coaching conversations?
- Stage-gating:          does it bear on entry/exit evidence at a stage?
- Portfolio management:  implications for portfolio-level decisions?
- Scaling strategy:      what does it imply for strategy design?
- Innovation packaging:  implications for defining the innovation package?
- Decision support:      what decision could this improve, and for whom?
```

**Never invent relevance (RATIFIED).** Curators must not manufacture an implication a source does not defensibly support. Where no defensible implication can be established from the source, the **only** permitted entry — per decision — is the exact phrase:

> `No practical implication established from this source alone.`

This phrase is legitimate and carries no penalty at the QA gate; a confabulated implication is a QA **failure**. Per-context "None identified" is retired in favor of this single, auditable no-implication phrase. The whole section is hard-labeled *Interpretation by curator — not source evidence*, keeping it firmly in Zone B and outside the provenance firewall.

**[Interpretation]** This section is what turns an archive into decision support — the operational face of the Manifesto's "Value first" — while the mandatory-honest-phrase rule protects the firewall's credibility. **[Hypothesis]** It will also become a prime input to AI-assisted coaching: a well-written Practical Implications block is effectively a retrieval target for "what does the repository know that helps *this* decision?"

> **Disagreement resolved (was §13.1).** The Librarian's concern (a required interpretation field pressures confabulation) and the Analyst's concern (without a forced "So what?" the graph fills with inert nodes) are both met by the ratified rule: the section is required, but the honest no-implication phrase is always available and confabulation fails QA. The Librarian's requested spot-check — that any stated implication be traceable to a Zone-A claim — is **adopted** as a QA check (§11).

### 4.5 Curator Notes (§10 of body)
The curator's doubts, caveats, and interpretations — explicitly Zone B. Material open questions are spawned as `OQ` nodes and linked.

---

## 5. Ontology governance — *governed but evolving* (REVISED)

**[Recommendation]** The taxonomy is a controlled vocabulary **and** an extensible ontology. Governance prevents uncontrolled growth; it does **not** freeze the ontology. The repository must be able to *discover* new capabilities, heuristics, patterns, and mechanisms and promote them under control.

### 5.1 Term lifecycle
Every controlled-vocabulary term (capability, methodology family, sector, edge type, even node type) has a status:

`candidate` → `provisional` → `endorsed` → `deprecated`

- **candidate** — proposed (by a human or by the Analyst from a recurring signal), not yet usable for mandatory classification.
- **provisional** — usable, flagged as new; under observation.
- **endorsed** — canonical; the default vocabulary.
- **deprecated** — retired; retained for historical nodes, excluded from new classification, mapped to a successor.

### 5.2 Discovery mechanism
**[Recommendation]** The Analyst may open a **Candidate Concept / Candidate Capability / Candidate Heuristic** proposal when a pattern recurs across independent sources (e.g., a mechanism appearing in ≥3 independent source families). The proposal is an `OQ`- or `IN`-class node describing the signal, the supporting nodes, and the recommended vocabulary change. Promotion `candidate → provisional → endorsed` is a **governed act** requiring human or dual-role sign-off, and it updates the vocabulary file **and** `Capabilities.md` in lockstep.

### 5.3 Why capabilities are not frozen
**[Interpretation]** A frozen capability list would force every new source into ten pre-set boxes and make the graph blind to genuinely new scaling mechanisms — the opposite of an intelligence system that learns. The lifecycle lets the ontology grow *from evidence* while governance keeps it from sprawling. **[Observed]** This also matches the Manifesto ("Learning before reporting") and the Roadmap's intent to mature over versions.

### 5.4 What stays controlled vs. free
- **Controlled (governed lifecycle):** node types, edge types, capabilities, stages, source types, evidence types, methodology families, source-confidence levels, AoW.
- **Free (ungoverned):** `tags` and `ai.semantic_tags` — discovery aids only, never a basis for mandatory classification or synthesis claims. Recurrent free tags are a *signal* the Analyst mines to propose new controlled terms.

### 5.5 Controlled facets (endorsed set at v1.0)
Full enumerations live in `03_CONTROLLED_VOCABULARIES.md`; summarized here:
- **Capabilities** — anchored to `Capabilities.md` (pathway / intelligence / cross-cutting).
- **Stages** — `proof-of-concept`, `transition-to-scale`, `scaling`, `cross-stage`.
- **Source types** — peer-reviewed, grey-literature, framework-or-methodology, case-study, tool-or-template, evaluation-or-review, dataset, expert-input, internal-document, presentation, workshop-output, unpublished.
- **Evidence types** — conceptual-argument, methodological-design, expert-judgment, participant-self-assessment, monitoring-data, independently-validated-outcome, comparative-evidence, portfolio-level-evidence.
- **Methodology families** — ipsr, scaling-scan, aiccra-scaling-framework, genderup, responsible-scaling, kohl-systems-approach, paass, link-methodology, general, none.
- **S4I Areas of Work** — aow1, aow2, aow3, aow4.

---

## 6. Edges (cross-linking / graph relationships)

Edges are first-class. Declaring them well is how the repository becomes a graph rather than a pile.

### 6.1 Edge record format (in node frontmatter)
```yaml
edges:
  - target: CP-0007
    type: describes
    note: "Primary source for the Scaling Readiness concept."
    register: interpretation      # observed | interpretation
```

### 6.2 Endorsed edge types (v1.0)
| Type | Meaning | Typical direction |
|---|---|---|
| `derived_from` | Node built from that source/node | Layer B → KC |
| `describes` | Source is a primary reference for a concept/heuristic | KC → CP/HP |
| `supports` | Evidence for the target proposition | KC/ER → HP/CP |
| `contradicts` | Evidence against the target | KC/ER → HP/CP |
| `refines` | Qualifies / adds boundary conditions | any |
| `relates_to` | Associative (use sparingly) | any |
| `part_of` | Component of a larger work/entity | any |
| `supersedes` / `superseded_by` | Version replacement | KC → KC |
| `cites` | Source cites another node's source | KC → KC |
| `applies_to_capability` / `applies_to_stage` | Classification edges | any → CD/stage |

**Reserved for entity nodes (provisional, §9):** `authored_by`, `affiliated_with`, `works_on`, `operates_in`, `funded_by`, `partners_with`, `deploys`, `part_of_package`.

### 6.3 Bidirectional integrity
Edges are declared once on the asserting node; the reciprocal is materialized on the target (`describes` ↔ `described_by`). Reciprocal maintenance and dangling-edge detection are **Librarian duties**, automated via `/_index/graph`. IDs — never titles — are the anchor. Inline references use `[[KC-0001]]`.

---

## 7. Confidence — Source vs Evidence (REVISED)

**[Recommendation]** There are two distinct constructs, and conflating them was the flaw in both v0.9 positions. v1.0 separates them cleanly.

### 7.1 Source Confidence — a property of the source (ON the Knowledge Card)
*How trustworthy is the source itself, as an artifact?* This is a characteristic of the source, assessable at ingestion without cross-source synthesis, so it legitimately lives on the KC.

Controlled scale (`source_confidence`):

| Level | Meaning | Typical source types |
|---|---|---|
| `authoritative` | Peer-reviewed or independently validated; recognized authority | peer-reviewed; independently-validated evaluation |
| `established` | Formal, attributable, methodologically transparent | framework-or-methodology; official evaluation-or-review; reputable grey-literature |
| `provisional` | Attributable but limited review or transparency | internal-document; working paper; expert-input with traceable basis |
| `informal` | Limited traceability or single-voice | presentation; workshop-output |
| `unverified` | Unpublished / anonymous / unattributable | unpublished; informal note |

Defaults map from `source_type`; the curator may adjust with a one-line rationale in Curator Notes. Source Confidence says **nothing** about whether the source's claims are *true* — only how much weight the artifact itself warrants.

### 7.2 Evidence Confidence — a synthesis judgment (NOT on the Knowledge Card)
*How strong is the evidence for a particular proposition, across sources?* This depends on corroboration, independence, evidence type, and transferability — none knowable from one source. It therefore lives **only** on Layer B nodes (ER, HP, CP, IN), using the Analyst scale: **well-supported, moderately-supported, emerging, speculative, insufficient-evidence.**

### 7.3 The rule
- KC carries `source_confidence` **and** per-claim `evidence_type`. It carries **no** Evidence Confidence.
- ER/HP/CP/IN carry `evidence_confidence`, computed across the KCs they cite.

**[Interpretation]** This gives you the at-a-glance trust signal on cards you wanted, without letting a single trustworthy-looking source launder its claims into the repository as if they were validated evidence. A peer-reviewed paper is `authoritative` as a *source* even when the *evidence* for one of its conceptual claims is only `emerging`.

> Both roles now agree on §7. The Librarian's provenance concern is met (source trust is a factual artifact property); the Analyst's synthesis concern is met (evidence judgment stays where cross-source reasoning happens). This resolves v0.9 §10.2.

---

## 8. Metadata (YAML frontmatter) + AI-readiness

`M` mandatory · `R` recommended · `O` optional. Full schema: `02_kc.schema.json`.

### 8.1 Core fields
| Field | Req | Notes |
|---|---|---|
| `id` | M | Immutable node ID, `KC-0001` (§ naming). Never reused/renumbered. |
| `schema_version` | M | Version of this standard, `"1.0"`. |
| `title` | M | Descriptive. |
| `node_type` | M | `knowledge-card` (registry §9.2). Replaces v0.9 `object_type`. |
| `layer` | M | `A` for KC. |
| `status` | M | Lifecycle state (§10.3). |
| `card_version` | M | SemVer of content (§10.1). |
| `created` / `updated` | M | ISO 8601. |
| `curator` | M | Person or agent role. |
| `source_type` | M | Controlled (§5.5). |
| `source_confidence` | M | Controlled (§7.1). |
| `authors` | M | List. |
| `publication_year` / `publisher` | R | |
| `source_locator` | M | `{url, doi, archived_path, access_date, integrity_hash}` (§ provenance). |
| `capabilities` | M | ≥1, controlled + lifecycle status. |
| `stages` | M | ≥1, controlled. |
| `methodology_family` | R | Controlled; `general`/`none` allowed. |
| `evidence_types` | M | Distinct types present in the source. |
| `geography` / `sector` | R | Normalized. |
| `aow` | R | Controlled; tagging ≠ delivery responsibility. |
| `tags` | O | Free discovery keywords. |
| `edges` | R | Typed graph edges (§6). |
| `supersedes` / `superseded_by` | O | Version chain. |
| `review_due` | R | Freshness trigger (§10.4). |

### 8.2 AI-readiness block (RESERVED — NEW)
**[Recommendation]** Reserve an `ai:` block now so future embedding/graph tooling is a data migration, not a schema break. All fields optional and default-empty at v1.0; nothing needs to be populated today.

```yaml
ai:
  machine_summary: ""        # short abstractive summary for retrieval/RAG
  semantic_tags: []          # model-suggested tags; NEVER used for mandatory classification (§5.4)
  embedding_status: none     # none | pending | embedded | stale
  embedding_model: ""        # model + version used, for reproducibility
  vector_id: ""              # id/handle in the vector store
  graph_synced: false        # whether node+edges are materialized in /_index/graph
  last_ai_processed: ""      # ISO date of last AI enrichment
```

**[Interpretation]** Keeping `semantic_tags` (model-suggested, free) firmly separate from controlled `capabilities`/`stages` protects the governed ontology from silent drift as AI enrichment scales — the model can *propose*, but promotion still runs through §5.2 governance.

---

## 9. Designing for future first-class object types (NEW)

**[Recommendation — RATIFIED: reserve now, implement incrementally]** The architecture must expand from documents to the **entities scaling acts upon**. Per decision, entity node types are **architecturally reserved now** — their IDs, folders, edge types, and a schema *slot* are fixed so early data never needs re-keying — but they are **not mandatory during initial ingestion**. A Knowledge Card may cite an author or organization in prose today without a `PER`/`ORG` node existing; entity nodes are created, and their schemas matured, **progressively** as the repository grows and each type's schema stabilizes (see the activation ladder in §9.4).

### 9.1 Entity node types (reserved)
People (`PER`), Organizations (`ORG`), Projects (`PRJ`), Programs (`PRG`), Countries (`CTY`), Technologies (`TEC`), Innovation Packages (`INP`), Solution Tracks (`SLT`), Scaling Partnerships (`SPN`).

### 9.2 Node-type registry (ID prefixes)
*Knowledge nodes:* `KC` knowledge-card · `CP` concept-page · `HP` heuristic-page · `ER` evidence-record · `MP` methodology-profile · `CC` coaching-case · `PS` portfolio-summary · `CD` capability-definition · `IN` insight-page · `OQ` open-question.
*Entity nodes (reserved):* `PER` `ORG` `PRJ` `PRG` `CTY` `TEC` `INP` `SLT` `SPN`.

### 9.3 How the architecture absorbs entities without rework
1. **Same ID/naming scheme** (§ naming) — an Organization is `ORG-0001__cgiar.md`.
2. **Same frontmatter spine** (`id`, `node_type`, `status`, `edges`, `ai`) — entity nodes just swap Zone-A/B knowledge sections for identity attributes.
3. **Edges already carry the load** — a Knowledge Card can be `authored_by → PER-0004`, a Project `operates_in → CTY-0231`, a Technology `part_of_package → INP-0007`. These edge types are reserved provisional now (§6.2).
4. **Provenance still applies** — entity attributes cite the KCs that assert them, so an Organization's stated mandate is traceable to a source, not folklore.

**[Interpretation]** Once entity nodes exist, the graph answers questions no document repository can: *which organizations have delivery-system evidence in transition-to-scale in East Africa, and who are the people connecting them?* That query is a graph traversal over edges we are reserving today.

### 9.4 Activation ladder (incremental implementation — RATIFIED)
Entity types activate on demand, not all at once. Each type moves through the same gate before it becomes usable for mandatory linking:

`reserved` (ID/folder/edges fixed; no nodes) → `piloted` (a handful of nodes created against a draft schema during real use) → `active` (schema stabilized and ratified; nodes may be required by relevant edges).

**[Recommendation]** Likely activation order, driven by need: **Organizations** and **People** first (they attach to almost every source via `authored_by`/`affiliated_with`), then **Countries** (cheap, closed vocabulary), then **Projects/Programs**, then **Technologies/Innovation Packages** (align with AICCRA eCatalogue / TAAT — §11-review), then **Solution Tracks** and **Scaling Partnerships** (mature last, once real Solution Track applications exist). No entity attribute is ever unsourced — every attribute cites a KC.

> **Disagreement resolved (was §13.2).** The Analyst wanted entities soon (portfolio intelligence); the Librarian wanted provenance discipline first. The ratified reserve-now/implement-incrementally decision + the "no unsourced entity attribute" rule satisfies both: entities arrive when a real need pulls them, each with cited provenance, none blocking initial ingestion.

---

## 10. Provenance, naming, versioning (retained + graph-aware)

### 10.1 Provenance (Librarian core mandate)
- Every source archived **verbatim** in `/sources/`, read-only, filename embeds the node ID.
- `integrity_hash` = SHA-256 of the archived file; verified at ingestion and at each freshness review.
- Claim- and term-level `source_locator`s (page/§/figure/timestamp) on every Zone-A claim.
- Structured citation in frontmatter; human styles rendered on demand.
- Live URLs are never the sole provenance — capture a snapshot.
- Provenance block (body §2) is **immutable**; correcting it is always a MAJOR version bump with a log entry.

### 10.2 Naming
- **Stable opaque ID** `<TYPE>-<NNNN>` (never reused/renumbered) + **human slug** (correctable).
- Filenames: `<ID>__<slug>.md` for nodes; `<ID>__<slug>.<ext>` for sources.
- 4 digits now; widen before 10,000 nodes.

### 10.3 Status lifecycle
`draft → in-review → accepted → (needs-refresh ⇄ accepted) → deprecated/superseded`.
Only `accepted` nodes are canonical for synthesis. Nothing is ever deleted; superseded nodes are excluded from default synthesis and carry `superseded_by`.

### 10.4 Versioning
- `card_version` SemVer: **MAJOR** meaning-changing correction · **MINOR** additive · **PATCH** cosmetic.
- `schema_version` (this standard) is independent; a standard upgrade may trigger a migration pass.
- Body Change Log mirrors each bump with date, version, curator, reason, and dual sign-off marks.
- `review_due` freshness horizons (provisional): frameworks/methodologies 24 mo; empirical/portfolio 12 mo; foundational concepts 36 mo.

---

## 11. Quality-assurance acceptance gate (graph-aware, dual sign-off)

A node is `accepted` only when **all** checks pass.

**Structural** — frontmatter validates against `kc.schema.json`; `id` unique & well-formed; filename matches; all 11 body sections present; `schema_version` current.

**Provenance & fidelity (Librarian sign-off)** — source archived verbatim; `integrity_hash` verified; structured citation complete; every Zone-A claim/term has a locator; **source firewall intact** (Zone A free of interpretation); no claim overstates the source; `source_confidence` set with rationale if non-default.

**Synthesis integrity (Analyst sign-off)** — each claim has a valid `evidence_type`; methodology claims not dressed as outcome evidence; ≥1 capability and ≥1 stage with rationale; **Practical Implications completed honestly** — every stated implication is traceable to a Zone-A claim (the Librarian's adopted spot-check), and any context lacking a defensible implication uses the exact permitted phrase `No practical implication established from this source alone.`; a confabulated implication is a failure; edges use controlled types, resolve to existing nodes, and have reciprocals; boundary conditions stated or `None recorded`; curator interpretation confined to Zone B.

**Governance** — no new controlled term introduced without a paired lifecycle proposal (§5.2) and `Capabilities.md` update; link index has no new dangling edges; `status` and `review_due` set; `ai` block present (may be empty).

**Dual sign-off recorded in the Change Log:** Librarian ✓ (fidelity) + Analyst ✓ (synthesis).

---

## 12. Long-term vision — the standing evaluation lens (NEW)

**[Recommendation]** Every design decision, now and future, is evaluated against the Scaling Intelligence Operating System this graph is meant to become. The OS must ultimately support: knowledge management, evidence synthesis, scaling intelligence, portfolio intelligence, coaching support, stage-gating, strategic planning, adaptive learning, and AI-assisted decision support.

Traceability of each v1.0 decision to that vision:

| OS capability | Served by (this standard) |
|---|---|
| Knowledge management | Layer A nodes, provenance, naming, versioning |
| Evidence synthesis | Layer B nodes, Evidence Confidence, evidence-type facet |
| Scaling intelligence | Practical Implications, capability/stage facets |
| Portfolio intelligence | Entity nodes (§9), portfolio-summary node type |
| Coaching support | Practical Implications → coaching; Coaching Case nodes |
| Stage-gating | stage facet; Practical Implications → stage-gating |
| Strategic planning | Heuristics, Concepts, methodology profiles |
| Adaptive learning | Evolving ontology (§5), Open Questions, freshness reviews |
| AI-assisted decision support | AI-readiness block (§8.2), graph index, machine summaries |

**[Interpretation]** The single most important architectural bet is that a *governed graph with clean provenance and forced "so what"* is the right substrate for all nine — because each capability is ultimately a different traversal or synthesis over the same nodes and edges.

---

## 13. Disagreement ledger (preserved, per your standing request)

The team was asked not to converge prematurely. The three v1.0 tensions are now **resolved by decision**; new tensions surfaced during the architectural review remain **live** and are tracked in `05_ARCHITECTURAL_REVIEW.md` §7.

### 13.1 A *required* Practical Implications section — RESOLVED
Required section retained; the exact phrase `No practical implication established from this source alone.` is always permitted; confabulation fails QA; every stated implication must be traceable to a Zone-A claim (Librarian spot-check adopted, §11). Both positions met.

### 13.2 How fast to introduce entity nodes — RESOLVED
Reserve now, implement incrementally via the §9.4 activation ladder; no unsourced entity attribute. Both positions met.

### 13.3 Whether Source Confidence risks anchoring — RESOLVED
`source_confidence` stays on the card (factual property of the artifact); any claim of register `Hypothesis-by-author` carries its own low register regardless of source confidence, preventing a trustworthy *source* from lending false weight to a weak *claim*.

### 13.4 New live tensions (from the architectural review)
Three genuine tensions emerged while stress-testing the architecture for the OS: **(a)** how many frontmatter fields are truly mandatory at alpha (Analyst: trim to a minimum-viable card; Librarian: keep provenance fields mandatory); **(b)** whether dual sign-off is workable with a one-person-plus-AI team at alpha; **(c)** whether edges should remain inline or become first-class nodes to carry time-validity and provenance. Each is documented with both positions and a proposed path in `05_ARCHITECTURAL_REVIEW.md` §7. **These are the disagreements now requiring your attention.**

---

## 14. Ratification status

Decisions 1–7 are **ratified** and reflected throughout this RC (see the header decision log). The graph model, two-layer architecture, Source/Evidence Confidence split, evolving ontology, provenance firewall, validation mechanisms, AI-ready architecture, and required-but-honest Practical Implications are all locked.

**Remaining before final `v1.0`:** the three live tensions in §13.4 (mandatory-field scope, sign-off model at alpha, inline vs first-class edges) plus the review-driven additions in `05_ARCHITECTURAL_REVIEW.md` (notably rights/licensing metadata and `external_ids` for integration). These are consolidated for you in `07_FILE_MANIFEST.md` → "Remaining decisions." On their resolution the package is retagged `v1.0` and the first real ingestion proceeds.

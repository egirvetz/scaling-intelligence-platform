# Scaling Intelligence — Ingestion Workflow (Source → Synthesis)

**Companion to:** Knowledge Standard v1.0 · **Status:** proposed for ratification

How new knowledge enters the Scaling Intelligence Graph, from a raw source to synthesized intelligence. Nine stages, three phases. Roles: **L** = Librarian, **A** = Analyst, **H** = Human reviewer, **AI** = automated tooling.

```
   PHASE 1: CAPTURE (Layer A)         PHASE 2: CURATE (Layer A)        PHASE 3: SYNTHESIZE (Layer B)
  ┌──────────────────────────┐      ┌───────────────────────────┐   ┌────────────────────────────┐
  │ 1 Intake                 │      │ 4 Draft Knowledge Card    │   │ 7 Cross-node synthesis     │
  │ 2 Archive + hash source  │ ───▶ │ 5 Classify + edges        │──▶│ 8 Ontology discovery       │
  │ 3 Assign ID              │      │ 6 QA gate + dual sign-off │   │ 9 Publish + schedule review│
  └──────────────────────────┘      └───────────────────────────┘   └────────────────────────────┘
```

---

## PHASE 1 — CAPTURE

### Stage 1 · Intake (L, H)
Receive the source (file, URL, or pasted text). Record: what it is, why it's being ingested, who supplied it. Decide it is in scope (contributes to knowledge / capabilities / frameworks / heuristics / methods / decision support / coaching / learning / portfolio intelligence). If out of scope, log and stop.

### Stage 2 · Archive + integrity hash (L, AI)
Save the source **verbatim** to `/sources/` (read-only). Compute `sha256`. For URLs, capture a snapshot AND record the live URL — never rely on the live URL alone. **Provenance is fixed here and never changes.**

### Stage 3 · Assign ID (L, AI)
Claim the next `KC-NNNN` from `_index/id_registry.json`. Rename the archived source to `KC-NNNN__<slug>.<ext>`. IDs are immutable and never reused.

---

## PHASE 2 — CURATE (produces a Knowledge Card, Layer A)

### Stage 4 · Draft the Knowledge Card (L, A)
Copy the template. Fill **Zone A** (source fidelity) first: Source Summary, Provenance, Key Claims (each with `evidence_type`, `source_locator`, `register`), Definitions, Methods & Evidence Base, Scope. **Discipline:** nothing interpretive enters Zone A.

### Stage 5 · Classify, assess source, draw edges (L, A)
- Tag controlled facets: `capabilities` (≥1), `stages` (≥1), `evidence_types`, `source_type`, `methodology_family`, `aow`, geography, sector.
- Set `source_confidence` (default from `source_type`; adjust with rationale in Curator Notes).
- Write **Zone B**: Practical Implications ("So what?" — every context answered or "None identified"), Capability/Stage rationale, and **graph edges** to existing nodes (`describes`, `supports`, `contradicts`, `cites`, `authored_by`…).
- Spawn `OQ` nodes for material open questions.
- If a term you need doesn't exist, do **not** invent a tag — open a candidate-term proposal (Stage 8) and use the nearest endorsed term meanwhile.

### Stage 6 · QA acceptance gate + dual sign-off (L, A, H)
Run the §11 checklist. **AI** validates frontmatter against `kc.schema.json` and checks edges resolve with reciprocals. **L** attests provenance & firewall; **A** attests synthesis integrity & Practical Implications. Both marks recorded in the Change Log. Set `status: accepted`, `card_version: 1.0.0`, `review_due`. Materialize the node + edges into `_index/graph/`.

> A card that fails any check stays `in-review`. Nothing partial is accepted.

---

## PHASE 3 — SYNTHESIZE (produces Layer B intelligence)

### Stage 7 · Cross-node synthesis (A)
Once ≥1 accepted KC touches a concept/proposition, the Analyst builds or updates Layer B nodes:
- **Concept Page (CP)** — definition + current understanding, `describes`-linked from KCs.
- **Evidence Record (ER)** — evidence for/against one proposition, with **Evidence Confidence** computed across the supporting/contradicting KCs (independence-aware; source families not double-counted).
- **Heuristic Page (HP)** — a decision rule, its conditions, and the evidence balance.
- **Insight Page (IN)** — reusable cross-source finding.

Every Layer B claim links back to specific KC claims via edges + `source_locator`, so synthesis is always one hop from the archived source. Evidence Confidence lives here — never on the KC.

### Stage 8 · Ontology discovery & governance (A, H)
When a mechanism/pattern recurs across independent source families, open a **candidate capability / concept / heuristic** proposal (an OQ/IN node citing the signal). Promotion `candidate → provisional → endorsed` is a governed act (standard §5.2): on approval, update `CONTROLLED_VOCABULARIES.yaml` and `Capabilities.md` in lockstep. This is how the ontology learns without sprawling.

### Stage 9 · Publish, index, schedule review (L, AI)
Rebuild `_index/` (graph, facets, validation report). Node is queryable. `review_due` schedules re-verification: re-check `integrity_hash`, confirm claims still match the source, refresh edges, bump versions as needed.

---

## Guarantees this workflow enforces
- **Provenance never lost** — fixed at Stage 2, immutable thereafter.
- **Firewall preserved** — interpretation cannot enter Zone A (Stage 4 + Stage 6 check).
- **Synthesis always traceable** — every Layer B claim is one edge from a source locator (Stage 7).
- **Ontology governed but evolving** — new terms only via Stage 8 governance.
- **Two roles kept honest** — dual sign-off at Stage 6; disagreements documented, not dissolved.

## Roles at a glance
| Stage | L | A | H | AI |
|---|---|---|---|---|
| 1 Intake | ● | | ○ | |
| 2 Archive+hash | ● | | | ● |
| 3 Assign ID | ● | | | ● |
| 4 Draft KC | ● | ● | | |
| 5 Classify/edges | ● | ● | | |
| 6 QA + sign-off | ● | ● | ○ | ● |
| 7 Synthesis | | ● | | |
| 8 Ontology governance | ○ | ● | ● | |
| 9 Publish/index | ● | | | ● |

● lead · ○ consulted

# Scaling Knowledge — Version 0.1 Implementation Plan

**From:** Scaling Knowledge Team (Librarian + Analyst), in product-developer mode
**Goal:** the smallest *complete, usable* knowledge system that can support real Solution Track work — then validate it by using it, not by expanding it.
**Governing rule for v0.1:** build a folder, template, or file only when the *first real artifact* needs it. Everything else waits.

> **Product stance.** A Knowledge Card with clean provenance and an honest "so what?" is the smallest unit that delivers value. Synthesis (Concepts, Heuristics, Evidence) only pays off once several cards exist. So v0.1 optimizes for **one thing: getting real, trustworthy Knowledge Cards flowing**, then producing the *first* synthesis object that a Solution Track can actually use.

---

## 1. Files that should immediately exist under the Scaling Knowledge Standard

The **operating kit** — five files. These are what a curator touches to do the work:

| File | Why it's essential now |
|---|---|
| `KNOWLEDGE_STANDARD.md` | The single governing standard (already drafted, v1.0-rc1). |
| `KNOWLEDGE_CARD_TEMPLATE.md` | You cannot make a card without it. |
| `kc.schema.json` | Turns "did we fill it right?" into an automatic check. |
| `CONTROLLED_VOCABULARIES.yaml` | The tag lists the card must draw from (trim to what v0.1 uses — see §5). |
| `INGESTION_WORKFLOW.md` | The five-step path from source to accepted card (§6). |

Plus one lightweight governance note, **`GOVERNANCE.md` (½ page)**: who mints IDs, who signs off, how a new tag gets added. At a 1–2 person alpha this is three sentences, but write it down.

**Reference (keep, but not "operating") :** `ARCHITECTURAL_REVIEW.md`, `ARCHITECTURAL_ASSESSMENT.md`, the manifest. They inform decisions; a curator doesn't open them to ingest a source.

---

## 2. Templates essential for Version 0.1

**One: the Knowledge Card template.** That's it.

Defer the Concept / Heuristic / Evidence templates until the moment you write the first one — and write that first Layer-B template *by hand from the standard* when a real synthesis need appears (target: after ~5 cards). Building four templates before any card exists is exactly the premature richness we're trying to avoid.

---

## 3. Example artifacts to create first

- **Keep `EXAMPLE_KC-0001.md`** as the gold-standard *reference* card (it's illustrative, clearly labeled).
- **First real artifact to create = the first real Knowledge Card (`KC-0001`)** from an actual source tied to an active Solution Track. This is the product's first true test.
- Defer the CP/ER/HP examples as *operational* artifacts; the existing illustrative ones are enough reference until real Layer-B nodes are written.

**Recommendation:** pick the first real source from a Solution Track that is live *now*, so the card immediately earns its keep.

---

## 4. Repository folders necessary today vs. later

**Create today (three, plus one cheap extra):**
```
/repository
├── _standards/         # the operating kit (§1)
├── sources/            # verbatim archived originals
└── knowledge-cards/    # KC nodes
   (+ open-questions/   # optional but cheap; captures "we need X" from day one)
```

**Create just-in-time (when the first file for it exists):**
`concepts/`, `heuristics/`, `evidence/` — at first synthesis (~after 5 cards).
`capabilities/`, `insights/`, `methodologies/`, `cases/`, `portfolio/` — when first needed.

**Defer to Version 2:**
`_index/` (build when the generator exists, ~30–50 cards), `entities/*` (activation ladder), `crosswalks/` (at first external-system integration).

> Product principle: an empty folder is a promise you haven't kept. Don't scaffold the whole tree; grow it.

---

## 5. What to defer until Version 2

Reserve in the architecture (so it's not a rewrite later), but **do not build or operate now:**

1. **Materialized graph index & facet indexes** — answer queries with search/scripts until card count justifies a generator.
2. **`id_registry.json` automation** — track IDs in a plain running list (or a one-line-per-ID text file) at alpha.
3. **Reciprocal-edge automation** — declare each edge *once*, on the asserting card; generate inverses in v2.
4. **Full controlled-vocabulary lifecycle governance** — keep the `status` fields, but promote terms by a quick curator+review, not a formal process.
5. **Entity nodes (all types)** — reserved only; activate via the §9.4 ladder when a real need pulls them.
6. **Layer-B JSON schemas (CP/HP/ER)** — write the first ones as prose-validated templates; formalize schemas once their shape stabilizes.
7. **AI embedding/vector population** — fields stay reserved and empty.
8. **PRMS / IPSR / eCatalogue / TAAT crosswalks** — at first integration, not now.
9. **GitHub CI enforcement** — high-value, but v0.2; for v0.1, run the schema check locally by hand.
10. **Long-form (time-bounded, provenanced) edges** — reserve the shape in the schema; use only simple inline edges in v0.1.

**Two live tensions resolved in product-default form for v0.1:** adopt the **Minimum Viable Card** (§7 field core) and the **curator + AI second-pass** sign-off. Both are "Lite profile" settings, reversible by governance, not schema changes.

---

## 6. Minimum workflow to ingest the first real source

Five steps (the full nine collapse to this at alpha):

1. **Intake** — confirm the source is in scope and tied to a real Solution Track need. One sentence on *why*.
2. **Archive + hash** — save the original verbatim to `/sources/`, compute SHA-256, record it. *(Non-negotiable — provenance can't be added later.)*
3. **Assign ID** — take the next `KC-NNNN`; add it to the running ID list; rename the archived source to match.
4. **Draft the card** — Zone A first (summary, provenance, claims with locators, methods, scope), then Zone B (Practical Implications — honest, using the permitted phrase where nothing applies; capability/stage tags; any simple edges).
5. **QA + accept** — run §7; on pass, set `status: accepted`, `card_version: 1.0.0`, record sign-off in the Change Log.

**Skipped at alpha:** index rebuild (none yet), reciprocal-edge materialization, synthesis (that starts only once several cards exist).

---

## 7. Quality assurance before a Knowledge Card is accepted

A **one-screen checklist**, run by the curator with an AI second-pass (dual *human* sign-off deferred to v2):

**Minimum Viable Card — mandatory fields (must all be present):**
`id` · `source_locator{archived_path, access_date, integrity_hash}` · `rights` (license/confidentiality — add this field even in v0.1) · `source_type` · `source_confidence` · ≥1 `capability` · ≥1 `stage`. Everything else is recommended and can be enriched later.

**Checks:**
- [ ] Frontmatter validates against `kc.schema.json`.
- [ ] Source archived verbatim + hash recorded.
- [ ] Every Zone-A claim has a source locator.
- [ ] **Firewall intact** — no interpretation in Zone A.
- [ ] Practical Implications honest — every stated implication traces to a Zone-A claim; unsupported contexts use `No practical implication established from this source alone.`
- [ ] `source_confidence` set (with a one-line reason if non-default).
- [ ] Sign-off recorded (curator ✓ / AI-review ✓).

If any check fails, the card stays `in-review`. Nothing partial is accepted. That single rule is what keeps the repository trustworthy from card #1.

---

## 8. Version 0.1 implementation roadmap (before large-scale ingestion)

Five short phases. The point of each is to *learn from use*, not to produce volume.

**Phase 0 — Bootstrap (½ day).**
Create the three folders + `open-questions/`; commit the operating kit (§1); trim the vocab to v0.1 terms; add the `rights` field to schema + template; seed the ID list. *Done when a curator could ingest a source without asking where anything goes.*

**Phase 1 — First real card (the real test).**
Ingest one real source tied to a live Solution Track through the §6 workflow → `KC-0001`. *Done when it passes QA and a colleague can read it and find the source.*

**Phase 2 — First cohort (~5 cards, ≥2 capabilities).**
Ingest 4–5 more real sources spanning at least two capabilities and two source types. *Purpose: stress the vocabulary, the template, and the workflow with variety.* Log every friction as an Open Question.

**Phase 3 — First synthesis (the value proof).**
From the cohort, write **one Concept Page or Heuristic Page** that a Scaling Strategy coach could actually use on a current Solution Track. *This is the moment the system proves it supports real work, not just storage.*

**Phase 4 — Retrospective & standard tune (½ day).**
Review the Open Questions from Phases 1–3. Amend the standard where real use exposed friction (this is the "validate through use" you asked for). Decide what graduates from `experimental` to `stable`.

**Gate to large-scale ingestion:** ≥5 accepted cards + 1 usable synthesis object + retrospective complete + no unresolved firewall/provenance failures. Only then scale up — and only then build the v2 machinery (indexer, CI, entities) that the volume will justify.

---

## 9. One-line summary
Ship three folders, five standard files, one template, one real card — then five cards, one synthesis object, and a retro. That is the whole of v0.1. Everything else is reserved, not built.

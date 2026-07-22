# Scaling Intelligence Knowledge Discipline — Architectural Review

**For:** v1.0-rc1, before large-scale ingestion
**By:** Scaling Librarian + Scaling Analyst
**Lens:** building the long-term Scaling Intelligence Operating System (SI-OS)
**Method:** each component rated on Simplicity / Scalability / Maintainability / Extensibility (H/M/L), with the single most important risk called out. Ratings are **[Interpretation]** unless marked.

> Bottom line up front: the architecture is **sound and unusually well-factored for an alpha**, but it is **over-specified relative to the tooling and team that exist today**, and it is **missing three things that are painful to backfill** (rights/licensing, external identifiers, and an explicit dedup/merge policy). The right move is to *keep the architecture, ship a "Lite" operating profile for the first ~50 cards, and add the three missing fields now while they are cheap.*

---

## 1. Component-by-component review

| Component | S | Sc | M | Ex | Most important risk |
|---|---|---|---|---|---|
| Two-layer model (Layer A / B) | H | H | H | H | None material — this is the load-bearing wall and it's well placed. |
| Graph-first model (nodes + edges) | M | H | H | H | Edges are inline; time-varying/provenanced edges will strain the model (§6, §7c). |
| Node ID scheme (`TYPE-NNNN`) | H | H | H | M | Immutable prefixes are a one-way door (§6) — but the chosen set is right. |
| Markdown + YAML frontmatter as source of truth | H | M | H | H | Free-text bodies aren't machine-checkable; only frontmatter is. Acceptable. |
| JSON-schema validation | H | H | H | M | `schema_version: const "1.0"` blocks multi-version validation (§4, easy fix). |
| Controlled vocab + lifecycle | M | H | H | H | Lifecycle governance is heavier than a 1-curator alpha needs (§2). |
| Provenance firewall (Zone A/B) | H | H | H | H | Enforced only by human QA until a linter exists; risk of quiet erosion. |
| Source vs Evidence Confidence | H | H | H | H | Conceptually clean; keep. |
| Practical Implications (required) | H | M | H | H | Now well-guarded by the honest-phrase + traceability rule. |
| Dual sign-off QA gate | M | M | M | H | Assumes two independent reviewers; alpha team may be one person + AI (§7b). |
| Frontmatter field set | M | H | M | H | ~18 mandatory/recommended fields is a lot to hand-fill per card (§2, §7a). |
| AI-readiness block | H | H | H | H | Correctly reserved and inert; no cost today. Keep. |
| `_index/` (graph, facets, id_registry) | L | H | M | H | **Over-engineered now:** hand-maintaining generated artifacts before tooling exists (§2). |
| Reciprocal-edge materialization | L | H | M | H | **Over-engineered now:** manual reciprocals will drift without a script (§2). |
| Entity nodes (reserved) | H | H | H | H | Correctly deferred via the §9.4 ladder. Keep. |
| Freshness `review_due` | H | M | H | H | Horizons are guesses; low cost to carry. Keep. |
| Versioning (SemVer for cards + standard) | H | H | H | H | Sound; add a standard-level CHANGELOG (§5). |

**[Observed]** The example Knowledge Card validates against the JSON schema, and all vocab/schema files parse — so the machine-checkable core is real, not aspirational.

---

## 2. Over-engineered for the current stage

Nothing here is *wrong* for the OS; it is simply **early**. Recommend deferring the machinery, not the architecture.

1. **Hand-maintained `_index/` artifacts.** `nodes.json`, `edges.json`, `facets/`, `id_registry.json` are *generated* outputs. Until a build script exists, maintaining them by hand is pure overhead and a source of drift. **Recommendation:** mark `_index/` "generated-only; do not author"; for the first cohort, derive answers on demand (grep/scripts) and build the index generator when card count crosses ~30–50.
2. **Manual reciprocal edges.** Declaring an edge on both nodes by hand doesn't scale and will desync. **Recommendation:** declare edges **once** on the asserting node now; generate inverses when the indexer lands. (The standard already says inverses are generated — make it explicit that humans never hand-write them.)
3. **Full controlled-vocabulary lifecycle at 1 curator.** `candidate→provisional→endorsed→deprecated` with governed promotion is right for a multi-team platform, heavy for the alpha. **Recommendation:** keep the *statuses* (they cost nothing) but run a **lightweight promotion** at alpha (curator + one async review), reserving formal governance for when multiple contributors exist.
4. **Dual sign-off as a hard gate.** Valuable, but presupposes two people. **Recommendation:** allow **one human curator + AI-assisted second-pass** to satisfy the gate at alpha, recording both marks; escalate to two-human sign-off when the team grows. (See live tension §7b.)
5. **~18 fields per card.** Rich metadata is why the graph will be powerful, but filling it all by hand for every source is a friction that will quietly reduce ingestion throughput. **Recommendation:** define a **Minimum Viable Card** (§3, gap G1 fix) — a small mandatory core, everything else recommended — so nothing blocks capture.

> **[Interpretation]** The meta-risk of an alpha is not under-specification; it is *specifying so much that ingestion never starts*. Every deferral above protects throughput without discarding a single architectural commitment.

---

## 3. Missing / important gaps

Ordered by how expensive they are to add later (most expensive first).

- **G1 — Rights / licensing / confidentiality (CRITICAL, add now).** There is no field for copyright, license, embargo, or confidentiality. In a CGIAR context this is unavoidable: third-party copyrighted PDFs, embargoed datasets, internal-only documents. Backfilling rights across hundreds of archived sources is painful and legally risky. **Recommendation:** add `rights` block: `{license, holder, confidentiality: public|internal|restricted, embargo_until, redistribution_allowed}`. Gate `sources/` archival on it.
- **G2 — External identifiers (add now).** Only `doi`/`url` exist. Integration with PRMS, AICCRA eCatalogue, TAAT, CGSpace, IPSR requires stable cross-system keys. **Recommendation:** add an `external_ids` map: `{cgspace_handle, prms_result_id, ecatalogue_id, taat_id, ipsr_id, orcid}`. Cheap now, join-enabling later (§6 integration).
- **G3 — Duplicate / merge policy (add now, low cost).** The original Librarian mandate includes "identify duplicate or overlapping knowledge," but the standard has no dedup or node-merge procedure. Two cards for the same source, or two concepts that should be one, will happen. **Recommendation:** define a `merge`/`duplicate_of` relation + a merge procedure that preserves both IDs (never delete) and redirects edges.
- **G4 — Language / translation.** No `language` field; multilingual sources (FR/ES/PT common in CGIAR geographies) can't be filtered or paired. **Recommendation:** add `language` (+ optional `translation_of` edge).
- **G5 — Card-level curation audit.** `curator` exists, but not *who reviewed*, *when signed off*, or the card's own provenance. **Recommendation:** capture sign-off actors/dates in the Change Log as structured entries (feeds later audit/API).
- **G6 — Crosswalk artifacts.** Capability/stage/evidence facets are internal; external systems have their own taxonomies. Hardcoding mappings into the schema would be brittle. **Recommendation:** a versioned `crosswalks/` folder holding mapping tables (SI↔PRMS, SI↔IPSR stages, SI↔eCatalogue, SI↔TAAT) as data.
- **G7 — Visibility/access classification for derived nodes.** Tied to G1: a public Concept Page must not quote a restricted source verbatim. **Recommendation:** propagate a visibility flag from source rights to any node quoting it.
- **G8 — Edge provenance/attributes.** An edge like `contradicts` or (future) `partners_with 2020–2023` may itself need a source and a time window. Inline edges can't carry this well. **Recommendation:** reserve an optional long-form edge object (`{target, type, note, register, source, valid_from, valid_to}`) now (schema already allows extra edge keys to be added) — see one-way-door §6.
- **G9 — Empty-state / bootstrap.** The repo has foundational docs but the standard assumes indices and registries that don't exist yet. **Recommendation:** an explicit bootstrap checklist (create folders, seed `id_registry`, place standard) — folded into the ingestion workflow's Stage 0.

---

## 4. Simplifications that don't cost long-term capability

1. **Ship a "Lite" operating profile** for the first ~50 cards: MVC field core (G1 fix), single-curator+AI sign-off, edges declared once, `_index` generated-only. Graduate to "Full" when tooling + team exist. *One standard, two operating profiles* — no architectural fork.
2. **Drop `schema_version: const "1.0"`** in the JSON schema; accept a pattern (`^1\.`) so minor standard revisions don't invalidate every card.
3. **Collapse near-duplicate facets where safe.** `geography` regions + ISO codes are two systems; pick codes as canonical and treat regions as a derived rollup, not a parallel vocabulary.
4. **Let free `tags` do early discovery work**; only promote to controlled vocabulary when a tag recurs. (Already the intent — make it the explicit alpha default so curators don't agonize over facets.)
5. **Version lives inside the document + git tag, not in filenames.** Rename `00_KNOWLEDGE_STANDARD_v1.0.md` → `KNOWLEDGE_STANDARD.md`; stop renaming files per version (avoids churn and broken links).

---

## 5. Repository organization, naming, governance, versioning — recommendations

- **Organization:** keep the flat-by-type layout; add `crosswalks/` (G6) and `_standards/CHANGELOG.md`. Keep `_index/` generated-only.
- **Naming:** IDs and slugs as specified are good. **Change:** drop version suffixes from standard/spec filenames; version via the document header + git tags (`standard-v1.0`). Keep `<ID>__<slug>` for nodes/sources.
- **Governance:** define a tiny RACI now — who mints IDs, who promotes vocab terms, who signs off. At alpha this can be "curator proposes, reviewer confirms." Put it in a one-page `GOVERNANCE.md`. Escalate formality with team size, not before.
- **Versioning:** adopt SemVer for the **standard itself** with a CHANGELOG and short migration notes per bump; `schema_version` in cards tracks the standard's MAJOR.MINOR. Card `card_version` stays independent. This is what lets you evolve the standard without orphaning old cards.

---

## 6. Architectural decisions that will be hard to change later (one-way doors)

Ranked by reversibility cost. Walk through the cheap-to-keep ones deliberately; put a hinge on the expensive ones.

1. **ID scheme + node-type prefixes.** Changing later means re-keying every node and every edge. **Verdict:** lock now — the set is right. (Good door to close.)
2. **Two-layer split (source vs synthesis).** Reversing it would mean re-curating everything. **Verdict:** keep; it's the best decision in the package.
3. **Markdown+frontmatter as canonical store (vs database).** Migrating to a DB later is *feasible* precisely because frontmatter is structured and files are in git — but the free-text bodies would need parsing. **Verdict:** fine to keep; the generated `_index` is the migration bridge to any DB/API. Don't put machine-critical data in prose bodies.
4. **Inline edges vs edges-as-first-class-nodes.** *The subtlest and most expensive door.* If edges later must carry their own provenance, confidence, or time-validity (entities will demand this: partnerships, employment, deployments have dates and sources), retrofitting inline edges into edge-nodes touches every file. **Verdict:** reserve the **long-form edge object** now (G8) so the upgrade is additive, not a migration. This is the one place to spend design effort today. *(Live tension §7c.)*
5. **Flat capability enum vs hierarchical capability graph.** If capabilities need parent/child or relationships, the enum is limiting. **Verdict:** keep the enum for *tagging*, but let `CD` (Capability Definition) nodes carry structure via edges — so hierarchy lives in the graph, not the enum. Door stays open.
6. **`schema_version` as `const`.** Minor but real: hard-coding one version makes multi-version validation awkward. **Verdict:** fix now (§4.2) before any cards exist.

---

## 7. Live architectural tensions (Librarian ⇄ Analyst — preserved, need your call)

Per your standing request, these did not converge.

**7a — Minimum Viable Card vs full metadata at ingestion.**
- *Analyst:* trim mandatory fields to a small core so ingestion is fast and the graph fills; recommended fields can be enriched later (including by AI).
- *Librarian:* provenance-critical fields (source, hash, locators, rights) must be mandatory from the first card, or the archive is compromised and can't be fixed retroactively.
- *Proposed path:* MVC = mandatory **provenance + rights + classification minimum** (id, source_locator, integrity_hash, rights, source_type, source_confidence, ≥1 capability, ≥1 stage); everything else recommended and enrichable. This gives the Analyst speed on synthesis fields and the Librarian non-negotiable provenance. **Your ruling requested.**

**7b — Sign-off model at alpha.**
- *Analyst:* one curator + AI second-pass is enough to start; two-human sign-off will bottleneck a tiny team.
- *Librarian:* the dual sign-off is what keeps fidelity and synthesis honest against each other; weakening it invites drift.
- *Proposed path:* "Lite" profile permits curator + AI-review (both marks recorded); "Full" profile requires two humans; the switch is a governance setting, not a schema change. **Your ruling requested.**

**7c — Inline edges vs first-class edge nodes.**
- *Analyst:* keep edges inline and lightweight now; most knowledge-layer edges never need attributes.
- *Librarian:* entity relationships (partnerships, employment, deployment) inherently have time and provenance; without reserving the long-form edge now we buy a painful migration later (door §6.4).
- *Proposed path:* keep inline edges as default; **reserve** the optional long-form edge object in the schema now (additive, no cost to simple edges). **Your ruling requested.**

---

## 8. Integration outlook (SI, Scaling Strategy, IPSR, PRMS, eCatalogue, TAAT, GitHub, APIs, web)

- **Scaling Intelligence (internal):** the graph *is* the SI substrate; Analyst/Coach skills read curated nodes. Boundary already right — Coach consumes, Librarian/Analyst produce.
- **Scaling Strategy discipline (interpretive):** consumes Heuristics/Concepts, not raw sources; the firewall is exactly what lets Strategy pull *curated* intelligence. Strategy outputs (coaching cases) become nodes flagged interpretive. Keep the disciplines separate; connect via the graph.
- **IPSR:** IPSR stages ↔ Three Stages via a crosswalk (G6); IPSR outputs become Coaching Case / Solution Track entity nodes as those types activate (§9.4). Reserve `external_ids.ipsr_id`.
- **PRMS:** reporting system → add `external_ids.prms_result_id`; PRMS results can be *sources* (KC) or link to *entities* (projects/innovations). Never hardcode PRMS taxonomy — crosswalk it.
- **AICCRA eCatalogue / TAAT Clearinghouse:** innovation catalogues → map to **Technology / Innovation Package** entity nodes with `external_ids`; catalogue records ingest as KCs (consider a `catalogue-entry` source type when activated). These two systems are the strongest early reason to activate Technology/Innovation-Package entities.
- **GitHub:** repo-as-truth aligns natively with git. **Recommendation now (cheap, high value):** put `/repository` under git, add CI that runs schema validation + link/dangling-edge checks on every PR, a PR template embedding the QA gate, and `CODEOWNERS` for `_standards/`. This turns the QA gate from a checklist into enforced automation and is the single highest-leverage integration to start immediately.
- **APIs / web apps:** the generated `_index/graph/*.json` is the API surface; clean frontmatter + `external_ids` make read APIs and a web explorer straightforward. Design the indexer output *as* the API contract so the web app and API share one shape.

**[Recommendation]** Sequence: (1) GitHub + CI validation now; (2) add G1/G2/G6 fields now; (3) build the `_index` generator at ~30–50 cards; (4) stand up a read API/web explorer over the generated index; (5) activate Technology/Innovation-Package entities when eCatalogue/TAAT ingestion begins.

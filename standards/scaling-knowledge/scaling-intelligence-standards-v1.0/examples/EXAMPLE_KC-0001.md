---
# ⚠️ ILLUSTRATIVE EXAMPLE — demonstrates the v1.0 Knowledge Card format only.
# Source citation and claims are fabricated placeholders; do NOT treat as real evidence.
id: KC-0001
schema_version: "1.0"
title: "Scaling Readiness: concept, methodology, and application (ILLUSTRATIVE)"
node_type: knowledge-card
layer: A
status: accepted
card_version: 1.0.0
created: 2026-07-13
updated: 2026-07-13
curator: scaling-librarian
source_type: peer-reviewed
source_confidence: authoritative
authors: ["[Author A]", "[Author B]"]
publication_year: 2020
publisher: "[Journal name] (placeholder)"
source_locator:
  url: "https://example.org/illustrative-scaling-readiness"
  doi: "10.0000/illustrative.2020"
  archived_path: "/sources/KC-0001__scaling-readiness-illustrative-2020.pdf"
  access_date: 2026-07-13
  integrity_hash: "sha256:0000000000000000000000000000000000000000000000000000000000000000"
capabilities: ["scaling-readiness", "innovation-characterization", "scaling-strategy"]
stages: ["cross-stage"]
methodology_family: ["general"]
evidence_types: ["conceptual-argument", "methodological-design"]
geography: ["ssa", "global"]
sector: ["agriculture"]
aow: ["aow2"]
tags: ["readiness", "innovation-packages", "bottleneck-analysis"]
edges:
  - target: CP-0001
    type: describes
    note: "Primary reference for the Scaling Readiness concept."
    register: interpretation
  - target: CD-0002
    type: applies_to_capability
    note: "Foundational to the Scaling Readiness capability."
    register: interpretation
supersedes: ""
superseded_by: ""
review_due: 2028-07-13
ai:
  machine_summary: ""
  semantic_tags: []
  embedding_status: none
  embedding_model: ""
  vector_id: ""
  graph_synced: true
  last_ai_processed: ""
---

# Scaling Readiness: concept, methodology, and application (ILLUSTRATIVE)

<!-- ================= ZONE A: SOURCE FIDELITY ================= -->

## 1. Source Summary
The source introduces "scaling readiness" as a diagnostic that combines an innovation's
demonstrated maturity with the extent of its use, and applies it to innovation *packages*
rather than single technologies. It proposes a stepwise method to identify and act on the
binding bottleneck to scaling. *(Illustrative summary.)*

## 2. Provenance
[Author A] & [Author B] (2020). *Scaling Readiness: concept, methodology, and application.*
[Journal] (placeholder). DOI 10.0000/illustrative.2020.
Archived: `/sources/KC-0001__scaling-readiness-illustrative-2020.pdf`. Accessed 2026-07-13.
SHA-256: `0000…0000` (placeholder). **[IMMUTABLE]**

## 3. Key Claims
1. Scaling readiness = innovation readiness × innovation use.
   `[evidence_type: conceptual-argument] [loc: p.4] [register: Interpretation-by-author]`
2. Scaling requires characterizing the innovation *package*, not the core technology alone.
   `[evidence_type: conceptual-argument] [loc: p.5] [register: Observed]`
3. Progress is constrained by the least-ready component (a weakest-link logic).
   `[evidence_type: conceptual-argument] [loc: p.6] [register: Hypothesis-by-author]`

## 4. Definitions & Key Terms
- **Innovation readiness** — demonstrated maturity of an innovation, on a staged scale. `[loc: p.4]`
- **Innovation use** — extent of use by intended users beyond the originating team. `[loc: p.4]`

## 5. Methods & Evidence Base
Conceptual synthesis plus illustrative application cases. No controlled or independently
validated outcome study is reported. `[loc: p.6–9]`

## 6. Scope & Boundary Conditions
Framed for agricultural R&D in CGIAR-type systems. Transferability beyond that context is
asserted but not tested. `[loc: p.10]`

<!-- ================= ZONE B: CURATED INTELLIGENCE ================= -->

## 7. Practical Implications ("So what?")
**Register: Interpretation by curator — NOT source content.**

- **Coaching:** Gives coaches a shared vocabulary (readiness × use) to locate where a team is stuck.
- **Stage-gating:** Readiness levels can inform, but do not by themselves justify, gate decisions — evidence of *use* is also required.
- **Portfolio management:** Enables comparing innovations on a common readiness/use grid.
- **Scaling strategy:** Points strategy at the binding bottleneck rather than the whole system at once.
- **Innovation packaging:** Directly supports defining the package (Claim 2).
- **Decision support:** Improves "what must be true before we invest in scaling this?" decisions.

## 8. Relationship to Capabilities & Stages
- `scaling-readiness` — the source is a foundational reference for this capability.
- `innovation-characterization` — package framing (Claim 2) informs characterization.
- `cross-stage` — readiness/use is assessed at every stage, not one.

## 9. Graph Edges (Cross-References)
- `describes` → [[CP-0001]] (Scaling Readiness concept)
- `applies_to_capability` → [[CD-0002]]
- Claim 3 is assessed as a proposition in [[ER-0001]] and underlies heuristic [[HP-0001]].

## 10. Curator Notes & Open Questions
Analyst note: Claims 1 and 3 are conceptual/hypothetical (`register` reflects this) — do **not**
cite this card as evidence that scaling readiness *improves outcomes*. `source_confidence:
authoritative` reflects the *source artifact* (peer-reviewed), not the strength of evidence for
any single claim. Spawned [[OQ-0001]]: seek independently-validated outcome evidence for the
weakest-link proposition.

## 11. Change Log
- 2026-07-13 · 1.0.0 · scaling-librarian · Initial ingestion (illustrative). Librarian ✓ / Analyst ✓.

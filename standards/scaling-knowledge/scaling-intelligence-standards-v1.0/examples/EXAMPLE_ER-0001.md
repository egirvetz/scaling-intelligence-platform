---
# ⚠️ ILLUSTRATIVE EXAMPLE — demonstrates the v1.0 Evidence Record (Layer B) format.
id: ER-0001
schema_version: "1.0"
title: "Proposition: the least-ready package component binds scaling progress (weakest-link)"
node_type: evidence-record
layer: B
status: accepted
card_version: 1.0.0
created: 2026-07-13
updated: 2026-07-13
curator: scaling-analyst
capabilities: ["scaling-readiness", "scaling-strategy"]
stages: ["cross-stage"]
evidence_confidence: speculative
methodology_family: ["general", "kohl-systems-approach"]
tags: ["weakest-link", "bottleneck", "critical-assumptions"]
edges:
  - target: KC-0001
    type: derived_from
    note: "Source of the weakest-link claim (Claim 3)."
    register: interpretation
  - target: HP-0001
    type: supports
    note: "Evidence base for the weakest-link heuristic."
    register: interpretation
  - target: OQ-0001
    type: relates_to
    note: "Open question on outcome evidence."
    register: interpretation
review_due: 2028-01-13
ai: { machine_summary: "", semantic_tags: [], embedding_status: none, embedding_model: "", vector_id: "", graph_synced: true, last_ai_processed: "" }
---

# Evidence Record — Weakest-link proposition

## 1. Proposition (stated precisely)
"In an innovation package, scaling progress is constrained by the least-ready component; raising
the readiness of that component yields more scaling gain than improving already-ready components."

## 2. Evidence FOR
| Source | What it offers | Evidence type | Independent? |
|---|---|---|---|
| [[KC-0001]] | Conceptual argument for weakest-link logic (Claim 3) | conceptual-argument | — (single source) |

## 3. Evidence AGAINST / competing accounts
None recorded yet. (Absence of counter-evidence is **not** confirmation.)

## 4. Independence assessment
Currently **one source, one family**. No independent corroboration; no empirical or comparative test.

## 5. Methodology vs. outcome
The supporting evidence is a **methodological/conceptual argument**, not validated outcome
evidence. The proposition has not been tested against monitoring or comparative data.

## 6. Scope & transferability
Asserted for agricultural innovation packages in CGIAR-type systems; transferability untested.

## 7. Evidence Confidence
**Speculative.** Basis: a single conceptual source, no independence, no outcome test.

## 8. What would change this assessment
- One study with monitoring/comparative data linking component readiness to scaling gains → *emerging*.
- Independent corroboration from a second family (e.g., Kohl systems analysis) → *moderately-supported*.

## 9. Change Log
- 2026-07-13 · 1.0.0 · scaling-analyst · Evidence record created (illustrative). Librarian ✓ / Analyst ✓.

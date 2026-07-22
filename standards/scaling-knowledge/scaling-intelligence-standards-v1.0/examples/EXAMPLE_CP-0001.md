---
# ⚠️ ILLUSTRATIVE EXAMPLE — demonstrates the v1.0 Concept Page (Layer B) format.
# Content is a format demonstration, not validated repository knowledge.
id: CP-0001
schema_version: "1.0"
title: "Scaling Readiness (concept)"
node_type: concept-page
layer: B
status: accepted
card_version: 1.0.0
created: 2026-07-13
updated: 2026-07-13
curator: scaling-analyst
capabilities: ["scaling-readiness", "innovation-characterization"]
stages: ["cross-stage"]
evidence_confidence: emerging          # Layer B carries Evidence Confidence (NOT source_confidence)
methodology_family: ["general"]
tags: ["readiness", "innovation-use", "maturity"]
edges:
  - target: KC-0001
    type: derived_from
    note: "Primary source describing the concept."
    register: interpretation
  - target: HP-0001
    type: relates_to
    note: "Weakest-link heuristic operationalizes this concept."
    register: interpretation
review_due: 2029-07-13
ai: { machine_summary: "", semantic_tags: [], embedding_status: none, embedding_model: "", vector_id: "", graph_synced: true, last_ai_processed: "" }
---

# Scaling Readiness (concept)

## 1. Definition (current repository understanding)
Scaling readiness is the joint assessment of an innovation's **maturity** (how proven it is)
and its **use** (how widely it is used beyond its originators), applied to an innovation
*package* rather than a single technology. *(Synthesized; illustrative.)*

## 2. Sources & evidence base
| Source | Contribution | Evidence type | Source confidence |
|---|---|---|---|
| [[KC-0001]] | Origin of the readiness × use formulation | conceptual-argument | authoritative |

**Independence note:** currently 1 source (single family). Concept is **not** corroborated across
independent families — hence `evidence_confidence: emerging`.

## 3. Key distinctions
- Readiness ≠ use: a mature innovation with no uptake is not "scaling-ready."
- Package ≠ technology: readiness is a property of the whole package.

## 4. Relationship to other concepts
- Operationalized by the weakest-link heuristic [[HP-0001]].
- The proposition that the *least-ready component* binds progress is assessed in [[ER-0001]].

## 5. Open questions
- [[OQ-0001]] Does higher measured scaling readiness predict better scaling outcomes? (No validated evidence yet.)

## 6. Confidence statement
**Evidence Confidence: Emerging.** Basis: conceptually well-articulated in one authoritative
source, but no independent corroboration and no validated outcome evidence. Would upgrade to
*moderately-supported* with ≥2 independent source families or one validated-outcome study.

## 7. Change Log
- 2026-07-13 · 1.0.0 · scaling-analyst · Concept page created from KC-0001 (illustrative). Librarian ✓ / Analyst ✓.

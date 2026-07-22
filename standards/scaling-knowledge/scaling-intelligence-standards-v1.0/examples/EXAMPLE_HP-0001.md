---
# ⚠️ ILLUSTRATIVE EXAMPLE — demonstrates the v1.0 Heuristic Page (Layer B) format.
id: HP-0001
schema_version: "1.0"
title: "Fix the weakest link first"
node_type: heuristic-page
layer: B
status: accepted
card_version: 1.0.0
created: 2026-07-13
updated: 2026-07-13
curator: scaling-analyst
capabilities: ["scaling-strategy", "scaling-readiness"]
stages: ["transition-to-scale", "scaling"]
evidence_confidence: emerging
methodology_family: ["kohl-systems-approach", "general"]
tags: ["weakest-link", "prioritization", "bottleneck"]
edges:
  - target: ER-0001
    type: derived_from
    note: "Evidence record assessing the underlying proposition."
    register: interpretation
  - target: CP-0001
    type: relates_to
    note: "Operationalizes the Scaling Readiness concept."
    register: interpretation
review_due: 2028-01-13
ai: { machine_summary: "", semantic_tags: [], embedding_status: none, embedding_model: "", vector_id: "", graph_synced: true, last_ai_processed: "" }
---

# Heuristic — Fix the weakest link first

## 1. The rule
When designing a scaling strategy for an innovation package, identify the least-ready
component and prioritize raising *its* readiness before investing in already-ready components.

## 2. When it applies (conditions)
- The innovation is a **package** of interdependent components (not a standalone technology).
- Components are genuinely interdependent (progress needs all of them).
- You can assess relative readiness across components.

## 3. When it may NOT apply (boundary conditions)
- Components are substitutable or independent (no binding link).
- The "weakest" component is intractable within scope — reroute rather than force it.
- Political/market timing outweighs technical readiness.

## 4. Evidence balance
- **Supporting:** [[ER-0001]] (conceptual argument, [[KC-0001]]).
- **Contradicting:** none recorded.
- **Independence:** single source family; no outcome test.

## 5. Confidence
**Emerging.** Intuitive and conceptually grounded, but not empirically validated. Use as a
*prompt for analysis*, not a guarantee. Pair with critical-assumptions checking.

## 6. Practical use
- **Coaching:** ask a team "what is your weakest link, and what would it take to move it?"
- **Stage-gating:** a persistently unaddressed weakest link is a reason to hold at a gate.
- **Scaling strategy:** sequences investment toward the binding constraint.

## 7. Change Log
- 2026-07-13 · 1.0.0 · scaling-analyst · Heuristic created (illustrative). Librarian ✓ / Analyst ✓.

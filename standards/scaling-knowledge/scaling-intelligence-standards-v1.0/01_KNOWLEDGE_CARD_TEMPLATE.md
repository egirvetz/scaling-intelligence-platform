---
# ============================================================
# SCALING INTELLIGENCE — KNOWLEDGE CARD TEMPLATE
# Copy this file, rename to <ID>__<slug>.md, fill every field.
# Delete these comment lines before acceptance. Compliant with Knowledge Standard v1.0.
# ============================================================
id: KC-XXXX                       # immutable, assigned from the ID registry
schema_version: "1.0"
title: ""                         # descriptive human-readable title
node_type: knowledge-card
layer: A
status: draft                     # draft | in-review | accepted | needs-refresh | deprecated | superseded
card_version: 0.1.0               # SemVer; 1.0.0 at acceptance
created: YYYY-MM-DD
updated: YYYY-MM-DD
curator: ""                       # person or agent role

# --- Source identity ---
source_type: ""                   # see controlled vocab: source_type
source_confidence: ""             # authoritative | established | provisional | informal | unverified
authors: []
publication_year:                 # integer or blank
publisher: ""
source_locator:
  url: ""
  doi: ""
  archived_path: ""               # /sources/KC-XXXX__<slug>.<ext>
  access_date: YYYY-MM-DD
  integrity_hash: ""              # sha256:<hash> of archived source

# --- Classification (controlled facets; see 03_CONTROLLED_VOCABULARIES.md) ---
capabilities: []                  # >=1 required
stages: []                        # >=1 required
methodology_family: []            # general/none allowed
evidence_types: []                # >=1; distinct types present in the source
geography: []
sector: []
aow: []                           # aow1..aow4; tagging != delivery responsibility
tags: []                          # free discovery keywords only

# --- Graph edges ---
edges: []                         # list of {target, type, note, register}

# --- Version chain ---
supersedes: ""
superseded_by: ""
review_due: YYYY-MM-DD

# --- AI-readiness (reserved; optional at v1.0) ---
ai:
  machine_summary: ""
  semantic_tags: []
  embedding_status: none          # none | pending | embedded | stale
  embedding_model: ""
  vector_id: ""
  graph_synced: false
  last_ai_processed: ""
---

# <Title>

<!-- ================= ZONE A: SOURCE FIDELITY ================= -->
<!-- Only what the source says. No interpretation. -->

## 1. Source Summary
<!-- 2–5 neutral sentences: what the source is and what it claims to do. -->
None recorded

## 2. Provenance
<!-- IMMUTABLE after acceptance. Full citation, archived path, access date, hash. -->
None recorded

## 3. Key Claims
<!-- Numbered atomic claims. Each: [evidence_type: ...] [loc: p./§/fig] [register: Observed | Interpretation-by-author | Hypothesis-by-author] -->
None recorded

## 4. Definitions & Key Terms
<!-- Terms the source introduces/uses distinctively, with source_locator. -->
None recorded

## 5. Methods & Evidence Base
<!-- How the source generated its claims: design, data, n, geography, timeframe. -->
None recorded

## 6. Scope & Boundary Conditions
<!-- Where the source's claims do / do not apply. -->
None recorded

<!-- ================= ZONE B: CURATED INTELLIGENCE ================= -->
<!-- Clearly-labeled interpretation. Never mix into Zone A. -->

## 7. Practical Implications ("So what?")
**Register: Interpretation by curator — NOT source content.**
<!-- NEVER invent relevance. Where no defensible implication exists, use the EXACT phrase:
     "No practical implication established from this source alone."
     Every stated implication must be traceable to a Zone-A claim (QA spot-check). -->

- **Coaching:** No practical implication established from this source alone.
- **Stage-gating:** No practical implication established from this source alone.
- **Portfolio management:** No practical implication established from this source alone.
- **Scaling strategy:** No practical implication established from this source alone.
- **Innovation packaging:** No practical implication established from this source alone.
- **Decision support:** No practical implication established from this source alone.

## 8. Relationship to Capabilities & Stages
<!-- One-line rationale per capability and per stage tagged above. -->
None recorded

## 9. Graph Edges (Cross-References)
<!-- Human-readable mirror of frontmatter `edges`, with rationale. Use [[IDs]]. -->
None recorded

## 10. Curator Notes & Open Questions
<!-- Zone B. Doubts, caveats, source_confidence rationale if non-default. Spawn OQ nodes for material questions. -->
None recorded

## 11. Change Log
<!-- Reverse-chronological. date · version · curator · reason · sign-off. -->
- YYYY-MM-DD · 0.1.0 · <curator> · Draft created. Librarian ☐ / Analyst ☐.

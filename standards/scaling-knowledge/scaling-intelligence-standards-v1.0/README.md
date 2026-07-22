# Scaling Intelligence — Foundational Standards (v1.0-rc1)

Produced by the Knowledge Development Team (Scaling Librarian + Scaling Analyst).
**Status:** Release Candidate. Decisions 1–7 ratified; architectural review complete; awaiting
final ratification of the items in `07_FILE_MANIFEST.md` → "Remaining decisions." Claude has
read-only repo access, so these files are handed to you to commit (target paths in the manifest).

## Package contents

| # | Deliverable | File |
|---|---|---|
| 1 | Knowledge Standard (canonical, v1.0-rc1) | `00_KNOWLEDGE_STANDARD_v1.0.md` |
| 2 | Knowledge Card template | `01_KNOWLEDGE_CARD_TEMPLATE.md` |
| 3 | JSON schema (machine validation) | `02_kc.schema.json` |
| 4 | Controlled vocabularies | `03_CONTROLLED_VOCABULARIES.yaml` |
| 5 | Repository / graph folder standards | `04_REPOSITORY_FOLDER_STANDARDS.md` |
| 6 | **Architectural review** (NEW) | `05_ARCHITECTURAL_REVIEW.md` |
| 7 | **Architectural assessment — 3 questions** (NEW) | `06_ARCHITECTURAL_ASSESSMENT.md` |
| 8 | **File manifest + remaining decisions** (NEW) | `07_FILE_MANIFEST.md` |
| 9 | Ingestion workflow (source → synthesis) | `09_INGESTION_WORKFLOW.md` |
| 10 | Example Knowledge Card | `examples/EXAMPLE_KC-0001.md` |
| 11 | Example Concept Page | `examples/EXAMPLE_CP-0001.md` |
| 12 | Example Evidence Record | `examples/EXAMPLE_ER-0001.md` |
| 13 | Example Heuristic Page | `examples/EXAMPLE_HP-0001.md` |

**Read order for review:** `07_FILE_MANIFEST.md` (what's here + what to decide) → `06_ARCHITECTURAL_ASSESSMENT.md` (the short verdict) → `05_ARCHITECTURAL_REVIEW.md` (the detail) → `00` (the standard itself).

## How the pieces fit
`00` is the authority. `01`–`04` operationalize it (fill-in template, validator, vocabularies,
folder layout). `06`–`09` are one connected, **illustrative** example graph showing the two
layers and the edges between them:

```
KC-0001 (source)  --describes-->  CP-0001 (concept)
   |                                   |
   | derived_from                      | relates_to
   v                                   v
ER-0001 (evidence) --supports--> HP-0001 (heuristic)
```

`10` is the process that produces all of the above, source to synthesis.

## Validation status
- `02_kc.schema.json` is a valid JSON Schema (2020-12) and `EXAMPLE_KC-0001` validates against it
  (dates JSON-normalized, as real ingestion tooling does).
- All YAML files parse.

## Ratified in this RC (decisions 1–7)
Practical Implications required + honest no-implication phrase · entity nodes reserved-now/
implemented-incrementally (§9.4 ladder) · graph-first architecture · Source vs Evidence Confidence ·
governed-but-evolving ontology · provenance firewall + validation · AI-ready architecture.

## Remaining decisions before final v1.0 (full list in `07_FILE_MANIFEST.md` §D)
Live trade-offs needing your ruling: Minimum Viable Card scope · alpha sign-off model ·
inline vs reserved long-form edges. Recommended-yes additions: rights/licensing · `external_ids` ·
dedup/merge policy · `language` · drop schema `const` · GitHub CI · CHANGELOG + GOVERNANCE.

## Live disagreements deliberately preserved (`00` §13.4 / review §7)
1. Minimum Viable Card vs full metadata at ingestion.
2. Dual sign-off vs curator+AI at alpha.
3. Inline edges vs reserved first-class edge nodes (the main one-way door).

## ⚠️ Note on the examples
All four example nodes are **illustrative format demonstrations**. Their sources, citations,
and claims are fabricated placeholders and must not be treated as real repository evidence.

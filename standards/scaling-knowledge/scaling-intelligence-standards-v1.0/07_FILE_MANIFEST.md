# v1.0-rc1 — Package Manifest & Remaining Decisions

**Package:** Scaling Intelligence Knowledge Discipline · **Version:** 1.0-rc1
**Generated:** 2026-07-13 · Claude has read-only repo access — these files are handed to you to commit.

## A. Manifest — every file and its intended repository location

Working files live in this package folder (`scaling-intelligence-standards-v1.0/`). The **Intended repository location** is where each should be committed under `/repository`. Note the recommended rename that drops version suffixes from filenames (review §5): version lives in the document header + git tag, not the filename.

| # | Working file | Intended repository location | Role |
|---|---|---|---|
| — | `README.md` | `/repository/_standards/README.md` | Package index |
| 1 | `00_KNOWLEDGE_STANDARD_v1.0.md` | `/repository/_standards/KNOWLEDGE_STANDARD.md` | **Canonical standard** (authority) |
| 2 | `01_KNOWLEDGE_CARD_TEMPLATE.md` | `/repository/_standards/templates/KNOWLEDGE_CARD_TEMPLATE.md` | Fill-in card template |
| 3 | `02_kc.schema.json` | `/repository/_standards/schemas/kc.schema.json` | Machine validation schema |
| 4 | `03_CONTROLLED_VOCABULARIES.yaml` | `/repository/_standards/CONTROLLED_VOCABULARIES.yaml` | Controlled vocab + lifecycle |
| 5 | `04_REPOSITORY_FOLDER_STANDARDS.md` | `/repository/_standards/FOLDER_STANDARDS.md` | Folder / graph layout |
| 6 | `05_ARCHITECTURAL_REVIEW.md` | `/repository/_standards/architecture/ARCHITECTURAL_REVIEW.md` | Review (this RC) |
| 7 | `06_ARCHITECTURAL_ASSESSMENT.md` | `/repository/_standards/architecture/ARCHITECTURAL_ASSESSMENT.md` | 3-question assessment |
| 8 | `07_FILE_MANIFEST.md` | `/repository/_standards/architecture/MANIFEST_v1.0-rc1.md` | This manifest |
| 9 | `09_INGESTION_WORKFLOW.md` | `/repository/_standards/INGESTION_WORKFLOW.md` | Source→synthesis process |
| 10 | `examples/EXAMPLE_KC-0001.md` | `/repository/_standards/examples/EXAMPLE_KC-0001.md` | Example Knowledge Card |
| 11 | `examples/EXAMPLE_CP-0001.md` | `/repository/_standards/examples/EXAMPLE_CP-0001.md` | Example Concept Page |
| 12 | `examples/EXAMPLE_ER-0001.md` | `/repository/_standards/examples/EXAMPLE_ER-0001.md` | Example Evidence Record |
| 13 | `examples/EXAMPLE_HP-0001.md` | `/repository/_standards/examples/EXAMPLE_HP-0001.md` | Example Heuristic Page |

**Not yet created (to be added on the decisions below), intended locations:**
- `/repository/_standards/CHANGELOG.md` — standard version history (review §5).
- `/repository/_standards/GOVERNANCE.md` — one-page RACI (review §5).
- `/repository/crosswalks/` — SI↔PRMS, SI↔IPSR, SI↔eCatalogue, SI↔TAAT mapping tables (review G6, §8).
- `/repository/_standards/schemas/{cp,hp,er}.schema.json` — Layer B schemas (deferred until KC standard is in use).
- `.github/workflows/validate.yml`, `.github/PULL_REQUEST_TEMPLATE.md`, `CODEOWNERS` — GitHub CI + QA-gate enforcement (review §8).

## B. What changed in this RC (vs the v1.0 draft)
- Version → **v1.0-rc1**; decisions 1–7 marked ratified (header + §14).
- **Practical Implications** (§4.4): permitted no-implication phrase locked; "None identified" retired; traceability spot-check adopted into the QA gate (§11); template defaults updated.
- **Entity nodes** (§9): reserve-now / implement-incrementally ratified; added the §9.4 **activation ladder** and the "no unsourced entity attribute" rule.
- **Disagreement ledger** (§13): prior three tensions marked resolved; three new review-driven tensions logged as live (§13.4).
- Added **architectural review** (05), **assessment** (06), and this **manifest** (07).

## C. Validation status
- `kc.schema.json` is a valid JSON Schema (2020-12); `EXAMPLE_KC-0001` validates against it.
- All YAML/JSON files parse. (Fixed during review: `case-study` removed from `evidence_types` in the example — it is a source type, not an evidence type.)

## D. Remaining decisions before final ratification (consolidated)

**From the live tensions (review §7 / standard §13.4):**
1. **Minimum Viable Card** — adopt the small mandatory core (provenance + rights + minimal classification), everything else recommended? *(§7a)*
2. **Sign-off model at alpha** — permit one curator + AI second-pass in a "Lite" profile, escalating to two-human "Full" later? *(§7b)*
3. **Edges** — keep inline as default but **reserve** the optional long-form (attributed, time-bounded) edge object now? *(§7c — the main one-way door)*

**From the identified gaps (review §3) — recommend "yes, add now" for all four:**
4. **Rights/licensing/confidentiality** block on sources? *(G1 — critical)*
5. **`external_ids`** map for PRMS / eCatalogue / TAAT / CGSpace / IPSR / ORCID? *(G2)*
6. **Duplicate/merge policy** + `duplicate_of` relation? *(G3)*
7. **`language`** field (+ `translation_of`)? *(G4)*

**From simplifications (review §4/§5) — low-risk housekeeping:**
8. Drop `schema_version: const` → pattern `^1\.`? *(review §4.2)*
9. Adopt **GitHub + CI validation** as the operating home now? *(review §8 — highest-leverage integration)*
10. Add `CHANGELOG.md` + one-page `GOVERNANCE.md`, and drop version suffixes from standard filenames? *(review §5)*

**Recommended default:** approve 4–10 (they are cheap now, expensive later, and non-controversial), and give explicit rulings on 1–3 (the genuine trade-offs). On those rulings the team will fold the changes in and retag the package **v1.0**.

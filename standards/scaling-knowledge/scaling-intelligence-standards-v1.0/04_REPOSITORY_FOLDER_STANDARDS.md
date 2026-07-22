# Scaling Intelligence — Repository & Graph Folder Standards

**Companion to:** Knowledge Standard v1.0 · **Status:** proposed for ratification

The files on disk are the **serialization** of the Scaling Intelligence Graph. This document fixes where each node type lives, how sources are preserved, and how the graph is materialized. The principle throughout: **flat folders by node type; navigation by facet query, not by folder path.**

## 1. Top-level layout

```
/repository
├── _standards/                 # governance: never synthesis content
│   ├── KNOWLEDGE_STANDARD.md            # the ratified standard (v1.0)
│   ├── KNOWLEDGE_CARD_TEMPLATE.md
│   ├── kc.schema.json                   # + cp/hp/er schemas as added
│   ├── CONTROLLED_VOCABULARIES.yaml
│   ├── FOLDER_STANDARDS.md              # this document
│   └── INGESTION_WORKFLOW.md
│
├── _index/                     # GENERATED — never hand-edited
│   ├── id_registry.json                 # every assigned ID + status (prevents reuse)
│   ├── graph/                           # materialized nodes + edges
│   │   ├── nodes.json
│   │   └── edges.json
│   ├── facets/                          # inverted indexes per facet (capability, stage, …)
│   └── validation_report.json           # last QA/schema run
│
├── sources/                    # IMMUTABLE primary sources, verbatim
│   └── KC-0001__scaling-readiness-sartas-2020.pdf
│
├── knowledge-cards/            # KC  (Layer A)
├── concepts/                   # CP  (Layer B)
├── heuristics/                 # HP  (Layer B)
├── evidence/                   # ER  (Layer B)
├── methodologies/              # MP  (Layer B)
├── cases/                      # CC  (Layer B)
├── portfolio/                  # PS  (Layer B)
├── capabilities/               # CD  (Layer B; canonical capability definitions)
├── insights/                   # IN  (Layer B)
├── open-questions/             # OQ
│
└── entities/                   # RESERVED — future entity nodes (§9 of the standard)
    ├── people/                 # PER
    ├── organizations/          # ORG
    ├── projects/               # PRJ
    ├── programs/               # PRG
    ├── countries/              # CTY
    ├── technologies/           # TEC
    ├── innovation-packages/    # INP
    ├── solution-tracks/        # SLT
    └── scaling-partnerships/   # SPN
```

## 2. Rules

**2.1 One node, one file, one folder.** A node lives in exactly the folder for its `node_type`. Its facets (capability, stage, geography…) are metadata, never folders. Adding a new topic never means adding a folder.

**2.2 Flat within a type.** No nested sub-topic folders inside `knowledge-cards/` etc. Sub-topic browsing is a facet query against `_index/facets/`. This is what stops the tree ossifying at scale.

**2.3 `sources/` is sacred.** Verbatim, read-only, filename embeds the node ID. Never edited, reformatted, or cleaned. One archived source per Knowledge Card.

**2.4 `_index/` is generated, never authored.** Rebuilt from node frontmatter by tooling. Hand-editing it desynchronizes the graph from its source of truth (the files).

**2.5 `_standards/` is governed.** Changes are versioned governance acts, not routine edits.

**2.6 Entity folders are reserved but empty at v1.0.** Present so entity nodes drop in without a re-org; schemas deferred per standard §9/§13.2.

## 3. The ID registry (`_index/id_registry.json`)
Single source of truth for allocated IDs. Guarantees IDs are never reused or renumbered even after deprecation. Every new node claims its next ID here first. Shape:

```json
{ "KC": { "next": 2, "assigned": { "KC-0001": {"status":"accepted","slug":"scaling-readiness-sartas-2020"} } } }
```

## 4. Graph materialization
`_index/graph/nodes.json` + `edges.json` are the queryable graph. On each accepted change the tooling: (a) validates frontmatter against the schema, (b) upserts the node, (c) writes declared edges **and their reciprocals**, (d) flags dangling edges (targets that don't exist or are deprecated), (e) refreshes facet indexes. This is where "repository" becomes "graph."

## 5. Naming (recap from standard §10.2)
- Nodes: `<ID>__<slug>.md` — e.g. `CP-0001__scaling-readiness.md`
- Sources: `<KC-ID>__<slug>.<ext>` — e.g. `KC-0001__scaling-readiness-sartas-2020.pdf`
- IDs: `<TYPE>-<NNNN>`, immutable; slugs correctable.

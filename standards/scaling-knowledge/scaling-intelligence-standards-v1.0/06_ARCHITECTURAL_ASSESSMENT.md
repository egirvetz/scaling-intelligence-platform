# Architectural Assessment — Three Questions

**Companion to:** `05_ARCHITECTURAL_REVIEW.md` · A short, opinionated read for v1.0-rc1.

---

## Q1 — If we were beginning this platform again today, what would we design differently?

Five things — none of them the core architecture, all of them sequencing and a few reserved fields.

1. **Start on GitHub with CI validation from line one.** Treat the standard as code: schema validation, link/dangling-edge checks, and the QA gate enforced on every pull request. We arrived at this after designing the standard; it should have been the first commit, because it makes every later rule self-enforcing.
2. **Design the Minimum Viable Card first, then grow it.** We specified a rich card and are now trimming back to a mandatory core. Starting from "what is the smallest card that preserves provenance and is still useful?" and adding fields only as real sources prove they're needed would have avoided premature richness.
3. **Reserve the long-form (attributed, time-bounded) edge from the start.** Inline edges are fine for knowledge links but wrong for entity relationships, which have dates and sources. This is the one genuine one-way door; we'd have built the hinge in on day one rather than retrofitting it (we're reserving it now — review §6.4/§7c).
4. **Add rights/licensing, visibility, external IDs, and language on the very first card.** These are cheap up front and expensive to backfill across a populated archive — especially rights in a CGIAR context. We'd never let a source be archived without them.
5. **Keep generated artifacts generated from the start.** We described `_index` and reciprocal edges as if they'd be maintained; we'd have written the tiny generator first and forbidden hand-editing, rather than specifying machinery ahead of the tool that produces it.

**[Interpretation]** Notably, we would *not* change the two-layer model, the provenance firewall, the graph-first framing, or the Source/Evidence Confidence split. The redesigns are about *when* and *how much*, not *what*.

---

## Q2 — What parts are likely to remain stable for many years?

These are the load-bearing walls. We would build the OS expecting them not to move:

- **The two-layer architecture** — source-anchored nodes vs synthesis-derived nodes. This distinction is fundamental, not stylistic; it will outlive every schema detail.
- **The provenance firewall and immutable sources** — verbatim archival, integrity hashing, claim-level locators, Zone A/B separation. This is the trust foundation; weakening it would undermine everything downstream.
- **The node-ID scheme and node-type registry** — stable opaque IDs, never reused. Once chosen, these are effectively permanent, and the chosen set is right.
- **The graph-first mental model** — nodes and edges as primitives, files as serialization, a generated index as the query/API surface.
- **Source Confidence (on cards) vs Evidence Confidence (on synthesis)** — a clean, durable conceptual distinction.
- **Governed-but-evolving ontology as a principle** — the *specific* capabilities will change; the principle that the ontology is controlled yet extensible will not.

**[Interpretation]** If these six hold, the platform can absorb almost any change elsewhere — new node types, new tooling, new integrations — without a foundational rewrite.

---

## Q3 — What should intentionally remain experimental until we have completed multiple real Solution Track applications?

Deliberately *not* frozen — these need contact with real coaching and real Solution Tracks before we can trust their shape:

- **Entity node schemas** (People, Organizations, Projects, Programs, Technologies, Innovation Packages, Solution Tracks, Partnerships). Reserve IDs/edges/folders (done); let the *fields* stabilize through the §9.4 activation ladder against real data. Solution Track and Partnership schemas should mature **last**.
- **The Practical Implications taxonomy** — the six decision contexts (coaching, stage-gating, portfolio, strategy, packaging, decision support) are a hypothesis about how knowledge routes to decisions. Real coaching will reshape them.
- **Evidence Confidence calibration** — the thresholds separating well-supported / moderately-supported / emerging / speculative are uncalibrated until we've rated evidence across many real propositions.
- **Heuristic Page structure** — heuristics only prove their format when coaches actually apply them to live Solution Tracks; expect the template to change.
- **Portfolio Summary schema** — meaningful only once there's a portfolio; defer hard commitments.
- **Freshness horizons** — the 12/24/36-month defaults are guesses; tune against observed churn.
- **Capability taxonomy specifics** — expect the discovery mechanism (§5.2) to add and retire capabilities as evidence accumulates.

**[Recommendation]** Mark each of the above `experimental` in the standard's status metadata so downstream consumers know not to build hard dependencies on them yet. Promote to `stable` only after **≥3 real Solution Track applications** have exercised them — the same evidence bar we apply to knowledge should apply to our own schemas.

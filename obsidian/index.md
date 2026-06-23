---
phase: 9
type: knowledge-layer-entry
codebase: itsdangerous
graph_commit: 672971d66a2ef9f85151e53283113f33d642dabd
---

# Knowledge Layer — `itsdangerous`

This is the entry point for the Obsidian-style knowledge layer of Assignment 4.
The goal of this layer is **not** to repeat the analysis, but to make it
*navigable*: each note is a small concept, and the wiki-links between notes let a
reader walk from a graph output to an architectural conclusion and back to its
evidence.

## How to read this vault

We treat the codebase as a **graph-based knowledge system**. Graphify turned the
8 source files of `itsdangerous` into a graph of **135 nodes / 334 edges / 7
communities**, and every edge is treated as a *claim* about a relationship with
an evidence level (EXTRACTED / INFERRED / AMBIGUOUS). The notes here connect that
graph to the modules it describes and to the documents that justify each claim.

## Map of notes

- [[architecture_map]] — the big picture: layers, hubs, bridges, and how the
  modules sit relative to each other.
- [[serializer]] — the serialization layer and the system's central hub.
- [[signer]] — the signing engine the rest of the system is built on.
- [[encoding_and_exceptions]] — the two cross-cutting layers (`encoding.py`
  helpers and the `exc.py` hierarchy).
- [[communities_and_bridges]] — the 7 detected communities and the nodes that
  bridge them.
- [[verification_notes]] — what is still unverified and must be checked by hand.

## Source artifacts behind this layer

- Graph data: `graph/itsdangerous/graph.json`, `graph/itsdangerous/GRAPH_REPORT.md`
- Written analysis: `docs/architecture_analysis.md`
- Evidence ratings: `docs/evidence_log.md`
- Selection & setup rationale: `docs/codebase_selection.md`,
  `docs/environment_and_inventory.md`, `docs/graph_generation_log.md`

## Evidence legend (used in every note)

- **[EXTRACTED]** — read directly from the graph/report (counted node, AST edge,
  printed number). Highest confidence.
- **[INFERRED]** — reasoned from the graph, not read off it (what a hub *means*).
  Medium confidence.
- **[AMBIGUOUS]** — the artifacts disagree or can be read more than one way. Must
  be verified before trusting. See [[verification_notes]].

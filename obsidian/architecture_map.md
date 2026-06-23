---
phase: 9
type: knowledge-layer-note
topic: architecture-overview
---

# Architecture Map

This note is the high-level map of `itsdangerous` as seen through the graph.
Start here, then follow the links into the per-subsystem notes.

## The layered picture [INFERRED, well supported]

Reading the graph top-down, the system looks like a **layered design with a
clear core**:

```
encoding helpers  →  Signer + algorithms  →  Serializer  →  timed / URL-safe variants
        (bottom)            (middle)            (top)             (specializations)
```

Cutting across all layers are the **exception hierarchy** (`exc.py`) and the
**public façade** (`__init__.py`, via 6 EXTRACTED `re_exports` edges).

- The layering itself is **[INFERRED]**, but it rests on **[EXTRACTED]** node
  counts and import edges (see [[verification_notes]] for which parts are solid).
- See [[serializer]], [[signer]], and [[encoding_and_exceptions]] for each layer.

## Modules and roles

| Module | Nodes | Role | Note |
|---|---|---|---|
| `serializer.py` | 33 | serialization layer / central hub | [[serializer]] |
| `signer.py` | 34 | signing engine + algorithms | [[signer]] |
| `timed.py` | 20 | time-aware variants | [[communities_and_bridges]] |
| `url_safe.py` | 9 | URL-safe variants | [[communities_and_bridges]] |
| `encoding.py` | 8 | shared utility helpers | [[encoding_and_exceptions]] |
| `exc.py` | 19 | exception hierarchy (cross-cutting) | [[encoding_and_exceptions]] |
| `_json.py` | 5 | JSON compaction wrapper | [[communities_and_bridges]] |
| `__init__.py` | 1 | public API surface | — |

Node counts are **[EXTRACTED]** from `graph.json`; the role labels are
**[INFERRED]** from file/symbol names.

## Hubs and bridges at a glance [EXTRACTED metrics]

- **`Serializer`** — top degree (26) *and* top betweenness (0.215): the
  architectural center and strongest bridge. → [[serializer]]
- **`Signer`** — degree 21, betweenness 0.156: the engine others build on. →
  [[signer]]
- **`want_bytes()`** — degree 21 in an 8-node module: a shared-utility hotspot. →
  [[encoding_and_exceptions]]
- **`BadSignature`** — degree 19, betweenness 0.123: a passive, cross-cutting
  hub. → [[encoding_and_exceptions]]

## Key healthy signal [EXTRACTED]

The Graphify report detected **no import cycles**. The architectural risk here is
*concentration of responsibility* in a few hubs, not circular dependency. The
risky-to-change nodes are tracked in [[verification_notes]].

## Traceability

Every claim in this map can be traced: graph output
(`graph/itsdangerous/GRAPH_REPORT.md`) → analysis
(`docs/architecture_analysis.md` §1–§7) → evidence
(`docs/evidence_log.md`). See [[communities_and_bridges]] and
[[verification_notes]] to follow the chain.

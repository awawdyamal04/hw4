---
phase: 9
type: knowledge-layer-note
topic: communities-bridges-variants
---

# Communities and Bridges

This note covers how the graph splits into **communities** (subsystems), which
nodes act as **bridges** between them, and where the **timed** and **URL-safe**
variants fit.

## The 7 communities [EXTRACTED detection → INFERRED themes]

Graphify detected **7 communities** (6 shown, 1 thin omitted). Mapping each to
its dominant file:

| Community | Dominant file(s) | Theme [INFERRED] |
|---|---|---|
| 0 | serializer.py | Serializer internals / dumps-loads |
| 1 | exc.py + encoding.py | Exceptions + encoding helpers |
| 2 | signer.py | Signing engine |
| 3 | url_safe.py + timed.py + serializer.py | URL-safe & timed serializer variants |
| 4 | signer.py | Signing algorithms (HMAC / None) |
| 5 | timed.py | Timestamp signing |
| 6 | _json.py | JSON compaction wrapper (thin/omitted) |

The communities line up reasonably well with the file structure [INFERRED],
which is a sign the clustering is meaningful rather than noise. Cohesion scores
are all low (≤0.22), suggesting the modules are tightly inter-dependent.

> **[AMBIGUOUS]:** community node-counts differ between `graph.json` and
> `GRAPH_REPORT.md` (the report came from a separate `cluster-only` re-run). Any
> *per-community* claim is held back until confirmed → [[verification_notes]].

## The bridges [EXTRACTED betweenness]

**121 of 334 edges (~36%) cross community boundaries** [EXTRACTED]. The three
bridge nodes the report names:

- **`Serializer`** (0.215) — connects community 3 ↔ 0, 1, 2, 5. See [[serializer]].
- **`Signer`** (0.156) — connects community 2 ↔ 0, 1, 3, 4, 5. See [[signer]].
- **`BadSignature`** (0.123) — connects community 1 ↔ all others. See
  [[encoding_and_exceptions]].

These bridges are *why* the layered map in [[architecture_map]] holds together:
the central hubs are also the nodes that stitch the subsystems into one system.

## Timed and URL-safe variants

- **Timed variants** (`timed.py`, communities 3 & 5): `TimestampSigner` and
  `TimedSerializer` add time-of-signing behaviour. Their module imports of
  [[signer]] and [[serializer]] are **[EXTRACTED]**, but the *subclass* links are
  only **[INFERRED]** `uses` edges — see the inheritance gap in
  [[verification_notes]].
- **URL-safe variants** (`url_safe.py`, community 3): explicitly import from both
  [[serializer]] and `timed.py`, and from `base64_encode/decode` in
  [[encoding_and_exceptions]] (all **[EXTRACTED]**). This supports reading them as
  specializations (compression + base64) layered on top of the serializer.

## Evidence pointers

- `docs/architecture_analysis.md` §4–§5; `graph/itsdangerous/GRAPH_REPORT.md`
  "Communities" and "Suggested Questions"; `docs/evidence_log.md` §4 (url_safe and
  timed rows).

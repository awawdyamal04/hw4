---
phase: 9
type: knowledge-layer-note
module: serializer.py
---

# Serializer

`serializer.py` is the **top layer** of the system and the home of its central
abstraction, `Serializer`. It is the object a user normally instantiates: it
takes Python data, serializes it, and signs it by wrapping a [[signer]].

## Why it is the center [EXTRACTED metrics → INFERRED role]

- **Highest degree of any code node: 26 edges** [EXTRACTED]. Top of the report's
  "God Nodes" list.
- **Highest betweenness: 0.215** [EXTRACTED]. The report explicitly calls it a
  *cross-community bridge*, connecting community 3 to communities 0, 1, 2 and 5.
- Putting these together, `Serializer` is **the architectural center and
  strongest bridge** [INFERRED]. It is also the top single-point-of-failure
  candidate: if its contract changes, both the serialization layer and everything
  bridging through it is affected.

## How it relates to the rest

- **`Serializer` → [[signer]]**: the module `imports` `Signer` [EXTRACTED], and
  `Serializer` builds a signer via `make_signer`. The "wraps a Signer" wording is
  supported by EXTRACTED import/type edges; the behavioural
  `Serializer --uses--> Signer` edge itself is **[INFERRED]**.
- **`Serializer` → [[encoding_and_exceptions]]**: imports from `encoding.py`
  [EXTRACTED]; several `--uses--> BadSignature` links are **[INFERRED]** and
  flagged in the report's "Surprising Connections".
- **Variants build on it**: `TimedSerializer` and the URL-safe serializer are
  specializations layered on top — see [[communities_and_bridges]]. Note that
  `TimedSerializer`'s tie to `Serializer` is only an **[INFERRED]** `uses` edge,
  not an EXTRACTED `inherits` edge (a real extraction gap, see
  [[verification_notes]]).

## Evidence pointers

- Hub/bridge metrics: `docs/architecture_analysis.md` §3–§4;
  `graph/itsdangerous/GRAPH_REPORT.md` "God Nodes" and "Suggested Questions".
- Edge ratings: `docs/evidence_log.md` §3 (node row) and §4 (Serializer↔Signer,
  exc.py rows).
- Items to confirm: [[verification_notes]] (the `uses` edges, the inheritance
  gap).

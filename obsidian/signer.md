---
phase: 9
type: knowledge-layer-note
module: signer.py
---

# Signer

`signer.py` is the **middle layer** — the signing engine that the rest of the
system is built on. It holds the `Signer` class plus the algorithm classes
(`HMACAlgorithm`, `NoneAlgorithm`) and the key-derivation logic.

## Role in the graph [EXTRACTED metrics → INFERRED role]

- **`Signer`: degree 21, betweenness 0.156** [EXTRACTED]. Second core hub and
  second-strongest bridge, connecting community 2 to communities 0, 1, 3, 4 and 5.
- **[INFERRED]** it is the engine that [[serializer]] and the timed variants sit
  on top of. It is the second single-point-of-failure candidate after
  `Serializer`.
- `signer.py` is the largest module by node count (**34 nodes** [EXTRACTED]),
  which matches its role as the core algorithmic component.

## How it relates to the rest

- **[[serializer]] depends on `Signer`**: the dependency is **[EXTRACTED]**
  (module import + type edges); the runtime `uses` link is [INFERRED]. See
  [[serializer]] for the same edge read from the other side.
- **`TimestampSigner` → `Signer`**: in `timed.py`, but the class-to-class link is
  only an **[INFERRED]** `uses` edge — no `inherits` edge was extracted, even
  though the real library defines `TimestampSigner(Signer)`. This gap is tracked
  in [[verification_notes]] and [[communities_and_bridges]].
- **Algorithms → [[encoding_and_exceptions]]**: `HMACAlgorithm` and
  `NoneAlgorithm` show **[INFERRED]** `--uses--> BadSignature` edges; the module
  import of `exc` and `encoding` is [EXTRACTED].

## Communities it spans

The signing logic is split across two communities — the **signing engine**
(community 2) and the **signing algorithms** (community 4). This split, and why
`Signer` bridges them, is discussed in [[communities_and_bridges]].

## Evidence pointers

- Metrics and bridge role: `docs/architecture_analysis.md` §3–§4.
- Edge ratings: `docs/evidence_log.md` §3 (Signer row) and §4
  (TimestampSigner↔Signer row).
- Items to confirm: [[verification_notes]].

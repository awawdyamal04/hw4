---
phase: 9
type: knowledge-layer-note
modules: [encoding.py, exc.py]
---

# Encoding and Exceptions

These are the two **cross-cutting layers** of `itsdangerous`. Neither is a "top"
or "core" module, but almost everything depends on them, so they shape the whole
graph. They are grouped here because both show the same pattern: small or passive
modules with very high connectivity.

## `encoding.py` — the shared utility layer

- Only **8 nodes** [EXTRACTED], yet its helpers are among the most connected in
  the graph: `want_bytes()` (degree 21), `base64_decode()` (11),
  `base64_encode()` (10) [EXTRACTED].
- **Small file, large fan-in → classic shared-utility shape** [INFERRED].
- **[[serializer]], [[signer]], `timed.py` and `url_safe.py` all import from
  `encoding.py`** [EXTRACTED]. `url_safe.py` imports `base64_encode/decode`
  explicitly, which supports the URL-safe variants doing base64 work — see
  [[communities_and_bridges]].
- `want_bytes()` is a **bottleneck candidate** [INFERRED], but partly on **6
  [INFERRED]** `uses` edges (e.g. inside `derive_key()` / `get_signature()`).
  Confirm callers before calling it a single point of failure →
  [[verification_notes]].

## `exc.py` — the exception hierarchy (passive cross-cutting hub)

- **19 nodes** [EXTRACTED] defining `BadData`, `BadSignature`, `BadPayload`,
  `BadHeader`, `BadTimeSignature`, etc.
- **`BadSignature`: degree 19, betweenness 0.123** [EXTRACTED]. It bridges
  community 1 to every other community.
- **[INFERRED]** these are *passive* hubs: their connectivity comes from being
  raised/referenced everywhere, not from calling other code. Renaming or
  restructuring the exception contract would touch the whole codebase — a
  *coupling* point rather than a runtime failure point.
- **Important caveat:** that every module *imports* `exc` is **[EXTRACTED]**, but
  the eye-catching `Serializer / Signer / HMACAlgorithm / NoneAlgorithm /
  _PDataSerializer --uses--> BadSignature` links are all **[INFERRED]**
  ("Surprising Connections"). The coupling is real; the specific raise
  relationships need source confirmation → [[verification_notes]].

## Why these two belong together

Both are **dependencies that flow upward** through the layers in
[[architecture_map]]: encoding feeds the signer/serializer with byte handling,
and exceptions feed every layer with a shared error contract. Together they
explain a large share of the 36% cross-community edges noted in
[[communities_and_bridges]].

## Evidence pointers

- `docs/architecture_analysis.md` §2, §3, §6; `docs/evidence_log.md` §3–§4
  (encoding helpers row, exc.py row).

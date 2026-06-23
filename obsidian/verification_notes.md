---
phase: 9
type: knowledge-layer-note
topic: open-verification
---

# Verification Notes

This note collects the claims that are **not yet safe to assert as proven**. It
exists to keep the knowledge layer honest: the PRD requires that no inferred edge
is presented as fact and that every uncertainty is labelled (PRD §9, NFR4). Each
item below should be checked against the real source under
`external_projects/itsdangerous/src/itsdangerous`.

## Extracted vs. inferred — what is solid

- **Solid backbone [EXTRACTED]:** module imports
  (`serializer.py → signer.py`, `url_safe.py → serializer.py/timed.py`), the
  spread of `encoding.py` and `exc.py` imports, and the existence + degree of the
  hub nodes. The layered conclusion in [[architecture_map]] rests mainly on these.
- **Uncertain layer [INFERRED]:** the behavioural and "is-a" relationships. Of
  334 edges, **38 are INFERRED** (avg confidence 0.57), and they are *only*
  `uses` (29) and `calls` (9) edges. That is where to be careful.

## Open items to verify

1. **The inheritance gap (highest priority).** `TimedSerializer` and
   `TimestampSigner` are real subclasses of [[serializer]] and [[signer]], but the
   graph records them only as **[INFERRED]** `uses` edges — no `inherits` edge was
   extracted. Confirm `class TimedSerializer(Serializer)` and
   `class TimestampSigner(Signer)` in `timed.py`. Asserting inheritance "because
   the graph shows it" would be overclaiming.

2. **The `--uses--> BadSignature` "Surprising Connections."** Five INFERRED edges
   from `_PDataSerializer / Serializer / HMACAlgorithm / NoneAlgorithm / Signer`
   inflate `BadSignature`'s degree (see [[encoding_and_exceptions]]). Verify which
   classes actually raise/catch `BadSignature`.

3. **`want_bytes()` as a bottleneck.** Its high degree partly rests on 6 INFERRED
   edges. Confirm the real callers (`derive_key()`, `get_signature()`) before
   treating it as a single point of failure. See [[encoding_and_exceptions]].

4. **Community-size discrepancy [AMBIGUOUS].** `graph.json` and `GRAPH_REPORT.md`
   assign different node counts to communities; the report came from a separate
   `cluster-only` re-run. Decide which clustering to trust before making any
   per-community claim. See [[communities_and_bridges]].

5. **The "thin omitted" community.** The report omits one community (<3 nodes),
   but `graph.json` shows community 6 (`_json.py`) has 5 nodes. Confirm the
   omission criterion and which community was dropped.

6. **Hub list filtering.** "God Nodes" excludes structural nodes (`Any`, file
   nodes); raw degree reorders the list. The top hubs (`Serializer`, `Signer`,
   `want_bytes()`, `BadSignature`) are stable across both views, but confirm the
   filtering is intentional and don't over-read the lower ranks.

## How this supports traceability

This note closes the loop required by the PRD (FR6, SC5): a reader can start from
a graph output, follow it through [[architecture_map]] into a subsystem note
([[serializer]], [[signer]], [[encoding_and_exceptions]],
[[communities_and_bridges]]), and arrive here to see exactly how confident the
claim is and what remains to be checked. The strong (EXTRACTED) claims can be
trusted; the weak (INFERRED / AMBIGUOUS) ones are routed here for manual
verification rather than asserted as proof.

## Evidence pointers

- `docs/architecture_analysis.md` §8–§9 (evidence table + manual-verification
  list); `docs/evidence_log.md` §5 (ambiguous/risky claims).

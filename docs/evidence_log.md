# Evidence Log — `itsdangerous`

**Course phase:** Phase 8 — Evidence log
**Assignment:** Assignment 4
**Codebase analyzed:** `external_projects/itsdangerous/src/itsdangerous`
**Graph built from commit:** `672971d66a2ef9f85151e53283113f33d642dabd` (`2.1.x-60-g672971d`)
**Source artifacts referenced:** `graph/itsdangerous/graph.json`, `graph/itsdangerous/GRAPH_REPORT.md`, `docs/architecture_analysis.md`
**Status:** Evidence log only. No Graphify re-run, no graph files modified, no architecture analysis modified, no Obsidian notes created, `README.md` untouched.

---

## 1. Purpose of This Phase

This phase records the **evidence** behind the most important architectural claims
we made in `docs/architecture_analysis.md`. The PRD treats every edge in the graph
as a *claim about a relationship* (PRD §9, FR5), so before we let a claim support a
conclusion, we should be able to say where it came from and how much we trust it.

The goal here is **not** to repeat the whole analysis or to list all 135 nodes and
334 edges. It is to take the handful of nodes and relationships that the analysis
actually leans on, and to write down, for each one:

* its evidence level (EXTRACTED / INFERRED / AMBIGUOUS),
* which artifact the evidence comes from,
* why we have that level of confidence,
* what still needs to be checked by hand against the real source code.

In short, this log is the "show your work" companion to the architecture analysis.
It keeps us honest about the difference between what the graph *shows* and what we
*reasoned*, and it gives an evaluator a single place to audit our confidence.

---

## 2. Evidence Levels

We use the same three levels as the PRD (§9) and the architecture analysis, applied
here at the level of individual nodes and edges:

* **EXTRACTED** — the fact comes straight out of the graph data or the report: a
  counted node, an AST-extracted edge (an explicit `import`, `inherits`, `method`,
  `contains`, etc.), or a number printed in `GRAPH_REPORT.md`. These edges carry
  `"confidence": "EXTRACTED"` and `confidence_score: 1.0` in `graph.json`. Highest
  confidence.
* **INFERRED** — the relationship was reasoned by the extractor (or by us) rather
  than read directly from a syntactic construct. In `graph.json` these are the
  `uses` and some `calls` edges marked `"confidence": "INFERRED"` with
  `confidence_score: 0.5`. They are plausible but **not proven**, and should be
  treated as lower confidence.
* **AMBIGUOUS** — the artifacts disagree, are incomplete, or can be read more than
  one way. Graphify reported **0% AMBIGUOUS** edges, so nothing is labelled
  ambiguous *inside the data*; we use this level for claims where the artifacts
  themselves are inconsistent (for example, the community-size mismatch noted in
  the analysis), and these must be verified before being trusted.

A reminder we hold ourselves to throughout: **an INFERRED edge is not a proven
relationship.** It is a hint that still needs to be checked against the source.

---

## 3. Important Nodes

These are the nodes the analysis relies on as hubs, utilities, or cross-cutting
points. Degree values are the "God Nodes" counts in `GRAPH_REPORT.md`, which agree
with the node entries in `graph.json`. The *existence and degree* of each node is
EXTRACTED; the *architectural role* we attach to it (hub, utility, etc.) is
INFERRED and is documented in the analysis, not here.

| Node | File | Degree (report) | Evidence level | Source artifact | Reason for confidence | Still needs manual verification |
|---|---|---|---|---|---|---|
| `Serializer` | serializer.py | 26 | EXTRACTED (node + degree); INFERRED (role) | GRAPH_REPORT.md "God Nodes"; graph.json | Node exists in `graph.json` (`serializer_serializer`) and tops the report's connected-node list. Degree is a direct count. | Whether all 26 edges are real responsibility vs. AST verbosity; the "central hub" reading is interpretation. |
| `Signer` | signer.py | 21 | EXTRACTED (node + degree); INFERRED (role) | GRAPH_REPORT.md; graph.json | Node `signer_signer` present; degree counted. Imported by serializer, timed, url_safe (all EXTRACTED). | The "engine that others build on" framing is reasoned, not read off the graph. |
| `want_bytes()` | encoding.py | 21 | EXTRACTED (node + degree); INFERRED (role) | GRAPH_REPORT.md; graph.json | Node `encoding_want_bytes` present; high degree for an 8-node module. | Several of its edges are INFERRED `uses` (report flags 6); the "bottleneck/high fan-in" reading depends on those being real. |
| `BadSignature` | exc.py | 19 | EXTRACTED (node + degree); INFERRED (role) | GRAPH_REPORT.md; graph.json | Node `exc_badsignature` present; high degree. Part of an EXTRACTED `inherits` chain in `exc.py`. | Much of its high degree comes from INFERRED `--uses--> BadSignature` edges ("Surprising Connections"); the "passive/cross-cutting hub" reading needs source confirmation. |
| `TimedSerializer` | timed.py | 15 | EXTRACTED (node + degree); INFERRED (role) | GRAPH_REPORT.md; graph.json | Node `timed_timedserializer` present; degree counted. | Its relationship *to* `Serializer` is only INFERRED in the graph (see §4) — verify the real subclass relationship. |
| `TimestampSigner` | timed.py | 14 | EXTRACTED (node + degree); INFERRED (role) | GRAPH_REPORT.md; graph.json | Node `timed_timestampsigner` present; degree counted. | Same caveat: its tie to `Signer` is an INFERRED `uses` edge, not an EXTRACTED inherits edge. |
| `base64_encode()` | encoding.py | 10 | EXTRACTED (node + degree) | GRAPH_REPORT.md; graph.json | Node `encoding_base64_encode` present; imported explicitly by `url_safe.py` (EXTRACTED). | Low risk; mainly confirm callers match the import sites. |
| `base64_decode()` | encoding.py | 11 | EXTRACTED (node + degree) | GRAPH_REPORT.md; graph.json | Node `encoding_base64_decode` present; imported explicitly by `url_safe.py` (EXTRACTED). | Low risk; same as above. |

**Note on degree counts.** The analysis already flags that a raw degree count over
*all* `graph.json` nodes (including the `Any` type and the file nodes) reorders this
list, and that the report filtered structural nodes out of "God Nodes". We treat the
filtered report list as EXTRACTED but acknowledge the filtering decision is itself
something to confirm (carried as item 6 in the analysis's manual-verification list).

---

## 4. Important Relationships / Edges

These are the relationships the analysis uses to argue the layered structure and the
risky change-points. The important subtlety — and the main reason this log exists —
is that several of these relationships appear in the graph at **two different
levels**: a **module-level import** (EXTRACTED) and a **class-level `uses`**
(INFERRED). We record both, because mixing them up is exactly how an inferred edge
could be mistaken for proof.

| Relationship (as claimed) | How it appears in the graph | Evidence level | Source artifact | Reason for confidence | Still needs manual verification |
|---|---|---|---|---|---|
| **Serializer related to Signer** | `serializer` module `imports` `signer_signer` (EXTRACTED); `Serializer.__init__` / `make_signer` type edges to `signer_signer` (EXTRACTED); plus `serializer_serializer --uses--> signer_signer` (INFERRED, 0.5) | **EXTRACTED** at module + type level; INFERRED at the behavioural `uses` level | graph.json; architecture_analysis.md §3–§4 | The import and the type-annotation edges are explicit AST facts, so the *dependency* is well grounded. The "Serializer wraps a Signer" wording is supported but the runtime `uses` link itself is inferred. | Confirm in `serializer.py` that `Serializer` actually instantiates/holds a `Signer` (it does via `make_signer`), so the relationship rests on EXTRACTED edges, not the INFERRED one. |
| **TimedSerializer related to Serializer** | `timed` module `imports` `serializer_serializer` (EXTRACTED); but the class link `timed_timedserializer --uses--> serializer_serializer` is **INFERRED (0.5)**. No `inherits` edge was extracted. | **INFERRED** at the class level (module import is EXTRACTED) | graph.json | The module clearly imports `Serializer`. However, the actual subclass relationship is **not** captured as an EXTRACTED `inherits` edge — only as an inferred `uses`. So we should not present "TimedSerializer is-a Serializer" as proven from the graph. | Check `timed.py`: confirm `class TimedSerializer(Serializer)`. If so, the *real* relationship is inheritance even though the graph only inferred a `uses` edge. This gap is a genuine limitation of the extraction. |
| **TimestampSigner related to Signer** | `timed` module `imports` `signer_signer` (EXTRACTED); class link `timed_timestampsigner --uses--> signer_signer` is **INFERRED (0.5)**. No `inherits` edge extracted. | **INFERRED** at the class level (module import is EXTRACTED) | graph.json | Same shape as the row above: the import is solid, but the class-to-class relationship is inferred, not extracted. | Check `timed.py` for `class TimestampSigner(Signer)`. Treat the subclass claim as needing source confirmation, not as graph-proven. |
| **serializer.py related to signer.py** | `serializer --imports/imports_from--> signer_signer` | **EXTRACTED** | graph.json (`imports_from`, context `import`, confidence EXTRACTED); architecture_analysis.md §2 | This is a direct, AST-read import edge with `confidence_score: 1.0`. Module-to-module dependency is about as solid as the graph gets. | Minimal; optionally confirm the import line in `serializer.py`. |
| **url_safe.py related to serializer.py / timed.py** | `url_safe --imports--> serializer`, `url_safe --imports--> serializer_serializer`, `url_safe --imports--> timed`, `url_safe --imports--> timed_timedserializer` | **EXTRACTED** | graph.json (all four import edges, confidence EXTRACTED, score 1.0) | `url_safe.py` explicitly imports from both `serializer.py` and `timed.py`; all edges are AST-extracted imports. This supports treating url-safe variants as specializations layered on top. | Low risk. The *interpretation* (mixin/specialization layer) is reasoned in the analysis and could be confirmed by reading the class definitions. |
| **exc.py exceptions used across modules** | Module imports are EXTRACTED: `serializer --> exc`, `signer --> exc`, `timed --> exc`, `url_safe --> exc`, `encoding --> exc_baddata`. The class-level `... --uses--> BadSignature` links are **INFERRED**. | **EXTRACTED** for the module-level dependency; **INFERRED** for the specific "raises/uses BadSignature" links | graph.json; GRAPH_REPORT.md "Surprising Connections"; architecture_analysis.md §4, §6 | That nearly every module *imports* `exc` is an extracted fact, which supports the "cross-cutting concern" claim. But the eye-catching `Serializer/Signer/HMACAlgorithm/... --uses--> BadSignature` edges are model-reasoned (INFERRED) and the report itself marks them `[INFERRED]`. | Verify in the source that those classes actually raise/catch `BadSignature`. Until then the *coupling via imports* is solid but the specific raise relationships are not proven. |
| **encoding.py helpers used across modules** | EXTRACTED imports: `serializer --> encoding`, `signer --> encoding`, `timed --> encoding`, `url_safe --> encoding` (and `url_safe --> base64_encode/base64_decode`). | **EXTRACTED** | graph.json (`imports_from` / `import`, confidence EXTRACTED) | Multiple modules explicitly import from `encoding.py`; these are direct AST import edges. This is the strongest evidence behind the "shared utility layer" reading. | The specific *call sites* of `want_bytes()` inside `derive_key()` / `get_signature()` are INFERRED `uses` edges and should be confirmed before calling `want_bytes()` a true bottleneck. |

---

## 5. Ambiguous or Risky Claims

These are the claims where we are least comfortable, and where over-reading the
graph would be a mistake. None of them should be presented as proven.

1. **`TimedSerializer`/`TimestampSigner` inheritance is not captured as EXTRACTED.**
   In the real library these are subclasses (`TimedSerializer(Serializer)`,
   `TimestampSigner(Signer)`), but the graph only records the class-to-class link as
   an **INFERRED `uses`** edge (score 0.5), not as an EXTRACTED `inherits` edge. The
   module-level imports *are* extracted, so the dependency is real, but the specific
   "is-a" relationship is, in graph terms, only inferred. **Risk:** asserting
   inheritance "because the graph shows it" would be overclaiming. Verify against
   `timed.py`.

2. **The `--uses--> BadSignature` "Surprising Connections."** All five of these
   (`_PDataSerializer`, `Serializer`, `HMACAlgorithm`, `NoneAlgorithm`, `Signer`
   → `BadSignature`) are INFERRED at avg confidence 0.57. They inflate
   `BadSignature`'s degree and feed the "cross-cutting exception hub" story. The
   story is plausible, but the individual edges are reasoned, not read. Verify which
   classes actually raise/catch `BadSignature`.

3. **`want_bytes()` as a bottleneck.** Its high degree is partly built on 6 INFERRED
   edges (the report flags this). The "single helper many call paths funnel through"
   reading is attractive but partly rests on inferred links. Confirm the real callers
   before treating it as a single point of failure.

4. **Community sizes disagree between artifacts.** `graph.json` and
   `GRAPH_REPORT.md` assign different node counts to the communities, and the report
   was produced by a separate `cluster-only` re-run. This is the clearest
   **AMBIGUOUS** item: the artifacts genuinely disagree, so any *per-community*
   claim (themes, sizes, the "thin omitted" community) is not safe until we confirm
   which clustering to trust. The analysis already flags this in §5 and §9.

5. **Hub list depends on a filtering choice.** The "God Nodes" ranking excludes
   structural nodes (`Any`, file nodes). That is a reasonable choice, but it is a
   *choice*, and the raw-degree ordering differs. The hub identities at the top
   (`Serializer`, `Signer`, `want_bytes()`, `BadSignature`) are stable across both
   views, which is reassuring, but the exact ranking below them should not be
   over-interpreted.

---

## 6. Summary — How This Log Supports the Architecture Analysis

This evidence log backs the architecture analysis by separating, claim by claim,
what is **read from the graph** from what is **reasoned about it**:

* The **structural backbone** the analysis depends on — module imports
  (`serializer.py → signer.py`, `url_safe.py → serializer.py/timed.py`), the spread
  of `encoding.py` and `exc.py` imports across modules, and the existence and degree
  of the main hub nodes — is **EXTRACTED** and high confidence. The layered-design
  conclusion rests mostly on these solid edges, which is the analysis's strongest
  footing.

* The **behavioural and "is-a" relationships** — `Serializer uses Signer`,
  `TimedSerializer`/`TimestampSigner` related to their bases, the
  `--uses--> BadSignature` links, and `want_bytes()`'s fan-in — are **INFERRED** and
  should be verified before being treated as fact. Notably, the inheritance of the
  timed classes is *not* captured as an extracted edge at all, which is a real
  limitation of the extraction worth flagging rather than hiding.

* One claim, the **community sizes**, is genuinely **AMBIGUOUS** because the two
  artifacts disagree; per-community statements are held back accordingly.

Because the analysis's central conclusions (layered architecture; `Serializer` and
`Signer` as the core; `exc.py` and `encoding.py` as cross-cutting layers) are
supported mainly by EXTRACTED edges, while the more uncertain readings are clearly
tagged INFERRED or AMBIGUOUS and routed to manual verification, this log lets a
reader trust the strong claims and audit the weak ones. That is exactly the
evidence discipline the PRD asks for (FR5, FR8, NFR4, SC3): **no inferred edge is
presented as proven, and every confidence level is traceable to its source
artifact.**

---

## File Changed

* **Created `docs/evidence_log.md`** (this file). No graph files were modified,
  Graphify was not re-run, `docs/architecture_analysis.md` was not modified, no
  Obsidian notes were created, and `README.md` was not edited.

# Reverse Engineering a Python Codebase with Graphify and an Obsidian-Style Knowledge Layer

**Assignment 4 — Graph-based reverse engineering**

> This README was written in **Phase 10**, the final phase, *after* the graph and
> all analysis artifacts already existed. It is intended to explain the finished
> project end to end so that an evaluator (or a future reader) can follow the whole
> workflow without prior knowledge of the codebase. Where a conclusion is reasoned
> rather than read directly off the graph, the language here is deliberately
> cautious — the detailed evidence ratings live in [docs/evidence_log.md](docs/evidence_log.md).

---

## 1. Assignment Goal

The goal of Assignment 4 is to **reverse engineer an unfamiliar Python codebase and
genuinely understand its system architecture** — not just to draw a picture that
"looks like" the code. The emphasis the course places on this work is on:

- following the Vibe Coding lifecycle (Idea → PRD → Plan → TODO → Verify → Execute → Push),
- working like a project manager who guides AI agents step by step rather than
  asking for the whole assignment at once,
- treating **every edge in the graph as a claim** that must be labelled
  *extracted*, *inferred*, or *ambiguous* before it is trusted,
- producing **evidence-based conclusions** instead of asserting that the graph
  "proves" something.

The full requirements are in [prd.md](prd.md); the execution strategy is in
[plan.md](plan.md); the task breakdown is in [todo.md](todo.md).

## 2. Graphify and the Obsidian-Style Knowledge Layer

**Graphify / Grphify** is a command-line tool that extracts an AST-based graph from
a source tree. It turns source files into a graph of **nodes** (modules, classes,
functions, methods, and docstring-derived "rationale" nodes) and **edges**
(imports, calls, inheritance, containment, references, and inferred "uses"
relationships). Crucially, it labels each edge with a confidence level, which is
what lets us treat the graph as evidence rather than decoration. In this project
Graphify is used as a **knowledge layer**, connecting code structure, planning
documents, rationale, dependencies, and architectural insight — not just as a
diagramming tool.

The **Obsidian-style knowledge layer** (under [obsidian/](obsidian/)) is a small
vault of cross-linked Markdown notes. Each note covers one concept (the serializer,
the signer, the cross-cutting layers, the communities, the open verification
questions) and uses `[[wiki-links]]` so a reader can walk from a graph output to an
architectural conclusion and back to the evidence that supports it. The entry point
is [obsidian/index.md](obsidian/index.md).

## 3. Selected Codebase: `itsdangerous`

The analyzed codebase is **[`itsdangerous`](https://github.com/pallets/itsdangerous)**
by the Pallets project — a small, focused library for cryptographically signing
data (used, for example, behind Flask's signed sessions).

It was chosen over `click` and `requests` because it is the strongest fit for an
honest, evidence-based graph analysis: small enough to analyze end to end, but with
real internal architecture (signing, serialization, timed and URL-safe variants,
encoding helpers, exceptions); public and reproducible; genuinely unfamiliar
internally to most developers; and graph-friendly, with relationships that are
mostly *extracted* from explicit imports, inheritance, and calls rather than buried
in dynamic behavior. The full comparison and justification is in
[docs/codebase_selection.md](docs/codebase_selection.md).

## 4. Reproducibility Information

| Item | Value |
|---|---|
| Repository URL | `https://github.com/pallets/itsdangerous` |
| Pinned commit | `672971d66a2ef9f85151e53283113f33d642dabd` |
| Git description | `2.1.x-60-g672971d` |
| Local clone path | `external_projects/itsdangerous` |
| Analyzed source path | `external_projects/itsdangerous/src/itsdangerous` |

The clone command and the verification commands used to pin the version are
recorded in [docs/codebase_reproducibility.md](docs/codebase_reproducibility.md).

**Note on `external_projects/`:** this folder is listed in `.gitignore` and is
**not committed** to this repository. Only the *reference* to the codebase — its
URL, the pinned commit hash, and the local clone path — is committed (in the docs
above). The committed graph artifacts under [graph/](graph/) were copied out of the
ignored clone so that the results travel with the repository even though the
third-party source does not.

## 5. Workflow Followed

The project followed the Vibe Coding lifecycle, one verifiable artifact and one
meaningful commit per phase:

**Idea → PRD → Plan → TODO → Verify → Execute → Push**

1. **Idea / Understanding** — aligned on *what* the assignment asks for in
   [docs/assignment_understanding.md](docs/assignment_understanding.md), based on
   [docs/course_context.md](docs/course_context.md).
2. **PRD** — defined the requirements, evidence rules, and success criteria in
   [prd.md](prd.md).
3. **Plan** — defined the execution strategy and folder structure in
   [plan.md](plan.md).
4. **TODO** — broke the plan into ordered tasks in [todo.md](todo.md).
5. **Codebase selection** — chose `itsdangerous` and justified it
   ([docs/codebase_selection.md](docs/codebase_selection.md)).
6. **Environment & setup** — cloned and pinned the codebase, inspected its
   structure, and confirmed the Graphify command was available
   ([docs/codebase_reproducibility.md](docs/codebase_reproducibility.md),
   [docs/environment_and_inventory.md](docs/environment_and_inventory.md),
   [docs/graphify_tool_check.md](docs/graphify_tool_check.md)).
7. **Graph generation** — ran Graphify and copied the outputs into the repo
   ([docs/graph_generation_log.md](docs/graph_generation_log.md)).
8. **Graph reading & analysis** — wrote the architecture analysis
   ([docs/architecture_analysis.md](docs/architecture_analysis.md)).
9. **Evidence rating** — recorded the confidence behind each key claim
   ([docs/evidence_log.md](docs/evidence_log.md)).
10. **Knowledge layer** — built the Obsidian vault ([obsidian/](obsidian/)).
11. **README (this phase)** — written last, only after results existed.
12. **Push** — committed gradually across phases to a public GitHub repository.

## 6. Graph Generation Summary

Graphify was run with:

```bash
graphify extract external_projects/itsdangerous/src/itsdangerous
graphify cluster-only external_projects/itsdangerous/src/itsdangerous
```

It scanned **8 code files** and produced a graph of:

- **135 nodes** (≈86 code nodes; ≈49 docstring-derived "rationale" nodes)
- **334 edges** (89% EXTRACTED, 11% INFERRED, 0% AMBIGUOUS; 38 inferred edges, avg confidence 0.57)
- **7 communities** (6 shown in the report, 1 thin community omitted)
- **0 import cycles detected**

The full run, including the "no LLM backend configured" note that left the
communities with placeholder names, is logged in
[docs/graph_generation_log.md](docs/graph_generation_log.md). The generated report
is committed at [graph/itsdangerous/GRAPH_REPORT.md](graph/itsdangerous/GRAPH_REPORT.md).

## 7. Main Architecture Findings

These are summarized here; each is tied to evidence and a confidence level in the
analysis and evidence log. The structural facts (node/edge counts, imports,
degrees) are **extracted**; the architectural *roles* are **inferred** from the
extracted metrics and module names and should be read as well-supported
interpretations rather than proofs.

- **`Serializer` is the central hub.** It has the highest degree of any code node
  (26 edges) and the highest betweenness (0.215), making it both the most connected
  node and the strongest cross-community bridge. It appears to be the architectural
  center of the system. *(degree/betweenness extracted; "center" inferred)*
- **`Signer` is the signing engine.** It is the second core hub (21 edges,
  betweenness 0.156), and the serializer and the timed/URL-safe variants depend on
  it. It looks like the engine the rest of the system is built on top of.
- **`encoding.py` is a shared utility layer.** A small module (≈8 nodes) whose
  helpers — especially `want_bytes()` (21 edges) and the base64 functions — are
  imported and used across the codebase: small file, large fan-in, the classic
  shape of a shared utility layer.
- **`exc.py` is a cross-cutting exception layer.** Nearly every module imports it,
  and its exception classes (`BadSignature`, `BadPayload`, `BadData`) show up as
  high-degree "passive" hubs that bridge all communities. This reads as a
  cross-cutting coupling point rather than a runtime failure point.
- **`timed.py` and `url_safe.py` are variants / specializations.** They layer
  time-aware and URL-safe behavior on top of the core serializer and signer. Note a
  real limitation: the graph captured the timed classes' relationship to their base
  classes only as **inferred `uses`** edges, not as extracted `inherits` edges, so
  the "is-a" subclass relationship is *not* graph-proven and is flagged for manual
  verification.

The strongest candidates for **bottlenecks / single points of failure** are
`Serializer`, `Signer`, `want_bytes()`, and the `exc.py` contract — the places
where a change would ripple the furthest. Full detail is in
[docs/architecture_analysis.md](docs/architecture_analysis.md).

## 8. Evidence Discipline

Following the PRD, every important relationship is treated as a claim with an
explicit confidence level. Three levels are used throughout
[docs/architecture_analysis.md](docs/architecture_analysis.md) and
[docs/evidence_log.md](docs/evidence_log.md):

- **EXTRACTED** — read directly from the graph data or report: a counted node, an
  AST-extracted edge (`import`, `inherits`, `method`, `contains`, …), or a number
  printed in `GRAPH_REPORT.md`. Highest confidence. The structural backbone of the
  analysis rests on these.
- **INFERRED** — reasoned rather than read directly: the model's `uses`/`calls`
  edges, and our interpretation of what a hub *means*. These are plausible hints,
  **not proven**, and are flagged as lower confidence (the 38 inferred edges average
  0.57 confidence).
- **AMBIGUOUS** — the artifacts disagree or can be read more than one way. Graphify
  labelled 0% of edges ambiguous, but we apply this level where the artifacts
  themselves conflict — most clearly the **community-size mismatch** between
  `graph.json` and the regenerated `GRAPH_REPORT.md`, which is held back from any
  per-community claim until verified.

The rule kept throughout: an inferred edge is never presented as proven.

## 9. What Was Verified vs. What Still Needs Manual Verification

**Verified / high confidence (extracted):** the totals (135 / 334 / 7), the
edge-confidence breakdown, the absence of import cycles, the module-to-module import
structure (`serializer.py → signer.py`, `url_safe.py → serializer.py`/`timed.py`,
the spread of `encoding.py` and `exc.py` imports), and the existence and degree of
the main hub nodes.

**Still needs manual verification against the source** (carried in
[docs/architecture_analysis.md](docs/architecture_analysis.md) §9 and
[docs/evidence_log.md](docs/evidence_log.md) §5, and summarized in
[obsidian/verification_notes.md](obsidian/verification_notes.md)):

1. The 38 inferred edges, especially the `--uses--> BadSignature` "Surprising
   Connections" — confirm which classes actually raise/catch `BadSignature`.
2. `want_bytes()`'s inferred call edges before treating it as a true bottleneck.
3. The community-size discrepancy between `graph.json` and the report.
4. The "thin omitted" community and the omission criterion.
5. The inferred theme labels for each community.
6. The "God Nodes" filtering of structural nodes (`Any`, file nodes).
7. The timed classes' inheritance (`TimedSerializer(Serializer)`,
   `TimestampSigner(Signer)`), which the graph only inferred.

## 10. Repository Structure

```
hw4/
├── README.md                         # this file (Phase 10, written last)
├── prd.md                            # Phase 2A — requirements
├── plan.md                           # Phase 2B — execution plan
├── todo.md                           # Phase 2C — task list
├── .gitignore                        # ignores external_projects/
├── docs/
│   ├── course_context.md             # course rules (given)
│   ├── assignment_understanding.md   # Phase 1 — what the assignment asks
│   ├── codebase_selection.md         # Phase 4 — why itsdangerous
│   ├── codebase_reproducibility.md   # Phase 5A — clone + pinned commit
│   ├── environment_and_inventory.md  # Phase 5B — env + file inventory
│   ├── graphify_tool_check.md        # Phase 5C — tool availability
│   ├── graph_generation_log.md       # Phase 6 — how the graph was generated
│   ├── architecture_analysis.md      # Phase 7 — the written analysis
│   └── evidence_log.md               # Phase 8 — evidence ratings
├── graph/itsdangerous/               # committed Graphify outputs
│   ├── GRAPH_REPORT.md
│   ├── graph.json
│   ├── graph.html
│   └── manifest.json
├── obsidian/                         # Phase 9 — knowledge-layer notes
│   ├── index.md
│   ├── architecture_map.md
│   ├── serializer.md
│   ├── signer.md
│   ├── encoding_and_exceptions.md
│   ├── communities_and_bridges.md
│   └── verification_notes.md
├── prompts/
│   └── prompts.md                    # prompts used to drive the work
└── external_projects/                # IGNORED by Git — local clone only
    └── itsdangerous/                 # the analyzed codebase (not committed)
```

## 11. Key Files and What Each Contains

| File | Contents |
|---|---|
| [prd.md](prd.md) | Product requirements: problem, goal, scope, FR/NFR, evidence rules, success criteria. |
| [plan.md](plan.md) | Execution strategy, folder layout, and how each later phase would be carried out. |
| [todo.md](todo.md) | Ordered task list and the SC1–SC7 verification checklist. |
| [docs/codebase_selection.md](docs/codebase_selection.md) | Candidate comparison and justification for choosing `itsdangerous`. |
| [docs/codebase_reproducibility.md](docs/codebase_reproducibility.md) | Repository URL, pinned commit hash, clone path, and verification commands. |
| [docs/environment_and_inventory.md](docs/environment_and_inventory.md) | Python/pip environment and the initial file inventory of the codebase. |
| [docs/graphify_tool_check.md](docs/graphify_tool_check.md) | Confirmation that the `graphify` command was available. |
| [docs/graph_generation_log.md](docs/graph_generation_log.md) | The exact Graphify commands, output counts, and where the artifacts were copied. |
| [docs/architecture_analysis.md](docs/architecture_analysis.md) | The full written architectural analysis, every claim tagged with a confidence level. |
| [docs/evidence_log.md](docs/evidence_log.md) | Per-node and per-edge evidence ratings — the "show your work" companion to the analysis. |
| [graph/itsdangerous/GRAPH_REPORT.md](graph/itsdangerous/GRAPH_REPORT.md) | Graphify's generated report: god nodes, surprising connections, communities, suggested questions. |
| [graph/itsdangerous/graph.json](graph/itsdangerous/graph.json) | The raw graph data (nodes, edges, confidence fields). |
| [graph/itsdangerous/graph.html](graph/itsdangerous/graph.html) | Interactive, browser-viewable rendering of the graph. |
| [obsidian/index.md](obsidian/index.md) | Entry point to the cross-linked knowledge layer. |
| [prompts/prompts.md](prompts/prompts.md) | The prompts used to guide the work across phases. |

## 12. How to View the Graph

The interactive graph is committed at
[graph/itsdangerous/graph.html](graph/itsdangerous/graph.html). To view it:

1. Clone or download this repository.
2. Open `graph/itsdangerous/graph.html` in any modern web browser
   (double-click it, or use *File → Open*). No server or build step is required.

For the textual summary (god nodes, communities, surprising connections), read
[graph/itsdangerous/GRAPH_REPORT.md](graph/itsdangerous/GRAPH_REPORT.md); the raw
data is in [graph/itsdangerous/graph.json](graph/itsdangerous/graph.json).

## 13. Conclusion

Representing `itsdangerous` as a graph moved the understanding from reading
individual files to reasoning about the whole system. The graph data supports, with
high confidence, that the library is a **small, dependency-dense, acyclic, layered
design**: encoding helpers at the bottom, the signer and its algorithms in the
middle, the serializer on top, with timed and URL-safe variants as specializations,
and an exception hierarchy and public `__init__.py` façade cutting across. The most
defensible single conclusion is that **`Serializer` is the architectural center**
(highest degree *and* highest betweenness), with `Signer`, `want_bytes()`, and the
`exc.py` contract as the other change-sensitive points.

Equally important, the project is honest about its limits: the behavioral `uses`
edges and the timed classes' inheritance are *inferred*, the community sizes are
*ambiguous*, and those items are explicitly routed to manual verification rather
than asserted as proven. That separation between what the graph *shows* and what we
*reasoned* is the core discipline the assignment asked for.

## 14. GitHub Submission

This work is submitted as a **public GitHub repository**, grown through gradual,
meaningful per-phase commits (not a single final commit):

```
https://github.com/awawdyamal04/hw4
```

The repository contains the documentation, prompts, committed graph artifacts, the
Obsidian-style knowledge layer, and this README. The analyzed third-party source is
**not** committed — `external_projects/` is gitignored — and is instead referenced
reproducibly by its URL and pinned commit hash (see §4).

---

## File Changed

- **Wrote `README.md`** (this file) — no other files were created or modified; no
  graph files were touched, Graphify was not re-run, and no code, PRD, plan, todo,
  docs, or Obsidian notes were changed.

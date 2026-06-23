# Plan — Assignment 4
Reverse Engineering a Python Codebase with Graphify / Grphify and Obsidian Knowledge Architecture

**Course phase:** Phase 2B — Plan
**Assignment:** Assignment 4
**Status:** Plan only (no codebase selected, no code, no graph outputs yet)

> This is the **Plan** step of the Vibe Coding lifecycle
> (Idea → PRD → Plan → TODO → Verify → Execute → Push). It explains *how* we will
> carry out the project defined in `prd.md`. It does **not** create tasks (that
> belongs to `todo.md`), it does **not** choose a codebase, it does **not** write
> code, and it does **not** generate any graph output. It is based only on
> `docs/course_context.md`, `docs/assignment_understanding.md`, and `prd.md`.

---

## 1. Overall Execution Strategy

Our strategy is to work in **small, ordered phases**, where each phase produces one
verifiable artifact and ends with a meaningful Git commit. This keeps us in the
project-manager mindset the course asks for: we guide the work step by step
instead of asking the AI to build the whole assignment at once.

The guiding principles for the whole project are:

- **Understand before drawing.** The goal is to understand the system
  architecture, not just to produce a picture that looks like the code (PRD §2).
- **Every edge is a claim.** No relationship is accepted as fact until we have
  classified it as extracted, inferred, or ambiguous (PRD §9).
- **Verify before asserting.** No conclusion claims the graph "proves" anything
  until it is checked against the code or planning evidence (PRD §9, NFR4).
- **Grow the repository gradually.** Each phase is its own commit; we never
  collapse the work into one final commit (PRD NFR2).
- **Defer big decisions to the right phase.** The codebase is not chosen here; the
  graph is not generated here; the final README is not written until results
  exist (PRD §5).

The high-level flow we will follow, after this plan, is:
**plan → task list (todo) → choose codebase → generate graph → read & analyze the
graph → rate evidence → verify conclusions → write analysis & knowledge layer →
write final README → final push.**

## 2. Project Folder Structure

We will keep a simple, predictable layout so an evaluator or future reader can
navigate the repository easily. The structure below is the **intended** layout;
folders are created only when the phase that needs them arrives, so nothing here
implies a codebase has already been chosen.

```
hw4/
├── README.md                     # final workflow explanation (written last)
├── prd.md                        # Phase 2A — requirements (done)
├── plan.md                       # Phase 2B — this plan
├── todo.md                       # Phase 2C — task list (later)
├── docs/
│   ├── course_context.md         # course rules (given)
│   ├── assignment_understanding.md  # Phase 1 understanding (done)
│   ├── codebase_selection.md     # later — which codebase and why
│   ├── architecture_analysis.md  # later — the written analysis
│   └── evidence_log.md           # later — edges rated extracted/inferred/ambiguous
├── prompts/                      # later — prompts used to drive the work
├── graph/                        # later — Graphify outputs (exports, data)
├── diagrams/                     # later — exported images of the graph
├── obsidian/                     # later — Obsidian-style knowledge vault / notes
├── external_projects/            # later — local clone of the selected Python codebase, ignored by Git
├── docs/codebase_selection.md     # later — repository URL, selection reason, and reproducibility notes

```

Names may be refined when we reach each phase, but the separation of concerns —
requirements, plan, tasks, docs, prompts, graph, diagrams, knowledge layer, and
the codebase itself — is fixed.

## 3. How We Will Choose a Python Codebase Later

Codebase selection is a **later phase**, not part of this plan (PRD §5, FR1). When
we reach it, we will choose **exactly one** Python codebase using these criteria:

- **Right size.** Big enough to have real architecture (multiple modules,
  dependencies, subsystems) but small enough to analyze honestly within the
  assignment. A codebase that is too large would force us to overclaim.
- **Readable and public.** Open-source and publicly available, so the work stays
  reproducible (PRD NFR3) and an evaluator can follow along.
- **Genuinely unfamiliar.** The assignment is about *reverse engineering*, so we
  prefer a codebase we did not write and do not already know well.
- **Graph-friendly.** Has clear imports, modules, and call relationships that
  Graphify can turn into meaningful nodes and edges.

When we select it, we will record the decision and its justification in
`docs/codebase_selection.md` (one codebase, with the reasoning), and commit that
as its own step. We deliberately do **not** name or lock in a codebase now, to
avoid a poor-fit choice made before the plan is ready (PRD R5).

## 4. How We Will Generate Graph Outputs Later

Graph generation is also a **later phase**. The plan for it, kept tool-neutral so
it does not assume a chosen codebase, is:

1. **Point Graphify / Grphify at the selected codebase** and run it to extract the
   structure into a graph.
2. **Produce the graph representation** of nodes (e.g., modules, classes,
   functions) and edges (e.g., imports, calls, dependencies) per PRD FR2.
3. **Type the nodes and edges** so the graph distinguishes kinds of components and
   kinds of relationships (PRD FR3).
4. **Export the outputs** into `graph/` (graph data) and `diagrams/` (images), so
   the results are stored in the repository and are reproducible.
5. **Record how the graph was generated** — the tool settings and the prompts used
   — so the process can be repeated.

We will not run Graphify or create any outputs in this phase; we are only
describing how it will be done.

## 5. How We Will Read the Graph

Once the graph exists, we will read it through the graph concepts required by the
course (PRD FR4, SC2). We will treat these as analytical lenses, not just labels:

- **Nodes** — the components of the system (modules, classes, functions). We ask
  what *type* each node is and what role it plays.
- **Edges** — the relationships between components (imports, calls, dependencies).
  Each edge is treated as a **claim** to be rated, not a given fact.
- **Hubs** — highly connected nodes; likely the most important components, and
  candidates for "if this changes, a lot changes."
- **Bridges** — edges (or nodes) that connect otherwise separate parts of the
  system; removing them would split subsystems apart.
- **Communities** — clusters of closely related nodes that likely correspond to
  subsystems or layers.
- **Centrality** — which nodes are most central to the system's connectivity, to
  confirm or challenge our intuition about what is important.
- **Bottlenecks** — points that much of the flow or many dependencies pass
  through; potential performance or coupling concerns.
- **Single points of failure** — nodes whose removal would disconnect or break a
  large part of the system; the key architectural risks.

For each lens we will write down *what the graph shows* and *what it might mean*,
keeping the two separate so observation is not confused with interpretation.

## 6. How We Will Classify Evidence

Following PRD §9, every important edge we use in the analysis is a claim that must
carry an evidence level. For each analyzed edge we will record: the node types it
connects, the edge type, the confidence level, and one of three labels:

- **Extracted** — the relationship comes directly from the code (e.g., an explicit
  import or call that Graphify read from the source). Highest confidence.
- **Inferred** — the relationship is reasoned from indirect signals (naming,
  patterns, structure) rather than read directly. Must be flagged as lower
  confidence.
- **Ambiguous** — the relationship is uncertain or could be read more than one
  way. Marked as such, never presented as fact.

These ratings will live in `docs/evidence_log.md` so that each conclusion can be
traced back to the evidence that supports it (PRD FR5, FR6, SC3).

## 7. How We Will Document Prompts

Because the assignment is about guiding AI agents as a project manager, the
prompts are part of the deliverable (PRD FR9, NFR6). We will:

- Save the meaningful prompts we use to drive the work in the `prompts/` folder.
- Keep them organized by phase, so the prompt history mirrors the project history.
- Capture enough context (what we asked and why) that the workflow is reproducible
  and an evaluator can see how decisions were guided, not just the end result.

## 8. How We Will Verify Conclusions

Verification runs throughout the project, not as a single step at the end (PRD §9,
NFR4, SC4). Before any architectural conclusion is asserted we will:

1. **Trace it to evidence.** Tie the conclusion to specific edges/nodes and their
   evidence ratings; an unrated claim is not ready to be asserted.
2. **Check it against the code or planning documents.** Confirm that extracted
   relationships are really in the source, and that inferred ones are reasonable.
3. **Cross-check with multiple lenses.** Prefer conclusions that several graph
   concepts agree on (e.g., a node that is both a hub and central).
4. **Label remaining uncertainty honestly.** Where verification is incomplete, the
   conclusion is stated with its confidence level, never as "proven."

No conclusion will claim the graph proves something until it has passed this
check.

## 9. Git Commit Strategy

We will grow the repository through gradual, meaningful commits, one per phase or
per coherent unit of work (PRD NFR2, SC6), continuing the existing
`phase N:` commit style already in the repo. Concretely:

- **One phase → at least one commit**, with a clear message describing what the
  phase produced (e.g., `phase 2b: write execution plan`).
- **No single final commit** that dumps the whole assignment at once.
- **No skipped commits** between phases.
- Commits stay scoped to the artifact of that phase (this phase, for example,
  changes only `plan.md`).
- The repository remains a **public GitHub repository** containing source code,
  prompts, diagrams, documentation, and the final README (PRD NFR3).

## 10. What Happens in Each Future Phase

This plan does not turn these into tasks (that is `todo.md`'s job). It only states,
at a high level, what each future phase will deliver:

- **Phase 2C — Task list.** Break this plan into concrete, ordered tasks in
  `todo.md`. No code or graph yet.
- **Phase 3 — Codebase selection.** Choose exactly one unfamiliar Python codebase
  using the criteria in §3; justify and record it in `docs/codebase_selection.md`.
- **Phase 4 — Graph generation.** Run Graphify / Grphify on the selected codebase,
  produce the typed node/edge graph, and export outputs to `graph/` and
  `diagrams/` (§4).
- **Phase 5 — Graph reading & analysis.** Read the graph with the required
  concepts (§5) and write the architectural analysis in
  `docs/architecture_analysis.md`.
- **Phase 6 — Evidence rating.** Classify each important edge as extracted,
  inferred, or ambiguous with a confidence level, recorded in
  `docs/evidence_log.md` (§6).
- **Phase 7 — Knowledge layer.** Build the Obsidian-style notes linking code
  structure to planning documents, rationale, and dependencies for traceability
  (§7 prompts captured alongside).
- **Phase 8 — Verification.** Verify every conclusion against the evidence rules
  before asserting it (§8).
- **Phase 9 — Final README.** Only after results exist, write `README.md`
  explaining the full workflow end to end.
- **Throughout — Push.** Commit gradually and keep the public repository up to
  date (§9).

Each phase ends with a meaningful commit, and no phase starts before the one
before it has produced its artifact.

---

## File Changed

- **Wrote `plan.md`** (this file) — no other files were created or modified.

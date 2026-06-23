# TODO — Assignment 4
Reverse Engineering a Python Codebase with Graphify and Obsidian Knowledge Architecture

**Course phase:** Phase 2C — Task list
**Assignment:** Assignment 4
**Status:** Task list only (no codebase selected, no code, no graph outputs yet)

> This is the **TODO** step of the Vibe Coding lifecycle
> (Idea → PRD → Plan → TODO → Verify → Execute → Push). It breaks `plan.md` into
> concrete, ordered, executable tasks. It does **not** choose a codebase, run
> Graphify, generate graph outputs, or edit `README.md`. It is based only on
> `docs/course_context.md`, `docs/assignment_understanding.md`, `prd.md`, and
> `plan.md`.

---

## Current status

- **Done:** Phase 0 (repo setup), Phase 1 (course context + assignment understanding),
  Phase 2 (PRD + Plan).
- **In progress:** Phase 3 — writing this `todo.md` and the verification checklist.
- **Not started:** Phase 4 onward (codebase selection, environment, graph generation,
  graph reading, evidence rating, architecture report, knowledge layer, README, final
  submission).
- **Reminder for this phase only:** do not pick the codebase, do not run Graphify, do
  not create graph outputs, and do not touch `README.md` yet.

Legend: `[x]` done · `[~]` in progress · `[ ]` not started.

---

## Phase 0 — Repository setup

- [x] Initialize the Git repository and confirm the working branch.
- [x] Confirm the repository will be public on GitHub for submission (PRD NFR3).
- [x] Establish the `phase N:` commit-message convention (plan §9).
- [x] Create the `docs/` folder for phase artifacts.

## Phase 1 — Course context and assignment understanding

- [x] Capture the course method and rules in `docs/course_context.md`.
- [x] Write `docs/assignment_understanding.md` describing *what* the assignment asks
  for, without choosing a codebase or writing code.
- [x] Commit each understanding artifact as its own phase commit.

## Phase 2 — PRD and Plan

- [x] Write `prd.md` defining problem, goal, users, scope, FR/NFR, deliverables,
  evidence rules, success criteria, and risks (Phase 2A).
- [x] Write `plan.md` defining the execution strategy, folder structure, and how each
  later phase will be carried out (Phase 2B).
- [x] Commit the PRD and Plan as separate phase commits.

## Phase 3 — TODO and verification checklist

- [~] Write `todo.md` (this file) breaking the plan into concrete, ordered tasks.
- [ ] Add a verification checklist that maps each PRD success criterion (SC1–SC7) to a
  later task that satisfies it, so nothing is dropped.
- [ ] Sanity-check that task order is executable (no task depends on a later one).
- [ ] Confirm the TODO does not select the codebase, run Graphify, or edit `README.md`.
- [ ] Commit as `phase 2c: write task list` (changes `todo.md` only).

## Phase 4 — Python codebase selection

- [ ] List 2–3 candidate unfamiliar, public Python codebases.
- [ ] Score each candidate against the plan §3 criteria: right size, readable + public,
  genuinely unfamiliar, graph-friendly (clear imports/modules/calls).
- [ ] Select **exactly one** codebase (PRD FR1).
- [ ] Record the repository URL, the selection reasoning, and reproducibility notes in
  `docs/codebase_selection.md`.
- [ ] Add `external_projects/` to `.gitignore` so the cloned codebase is not committed
  (plan §2).
- [ ] Commit as `phase 3: select python codebase`.

## Phase 5 — Environment and tool setup

- [ ] Clone the selected codebase locally into `external_projects/`.
- [ ] Pin the clone to a known commit/tag and record that commit hash for
  reproducibility.
- [ ] Install and verify Graphify / Grphify and any required dependencies.
- [ ] Do a small trial run of Graphify on a subset to confirm the toolchain works,
  without producing the final outputs yet.
- [ ] Note the exact tool version, settings, and commands so the run is repeatable
  (plan §4).
- [ ] Create the `graph/`, `diagrams/`, `prompts/`, and `obsidian/` folders when first
  needed.
- [ ] Commit as `phase 4a: environment and tooling setup`.

## Phase 6 — Graph generation

- [ ] Point Graphify at the selected codebase and run the full extraction (plan §4).
- [ ] Produce the node/edge graph: nodes for modules/classes/functions, edges for
  imports/calls/dependencies (PRD FR2).
- [ ] Assign a **type** to each node and each edge (PRD FR3).
- [ ] Export the graph data to `graph/` and the rendered images to `diagrams/`.
- [ ] Record the prompts and exact commands/settings used to generate the graph in
  `prompts/`, organized by phase (PRD FR9, plan §7).
- [ ] Spot-check that the exported graph loads/opens correctly before relying on it.
- [ ] Commit as `phase 4b: generate and export graph`.

## Phase 7 — Graph reading and evidence rating

- [ ] Read the graph through each required lens and record *what it shows* separately
  from *what it might mean* (plan §5): Nodes, Edges, Hubs, Bridges, Communities,
  Centrality, Bottlenecks, Single Points of Failure.
- [ ] Identify the key hubs and most central nodes; note candidate "if this changes, a
  lot changes" components.
- [ ] Identify communities/subsystems and the bridges that connect them.
- [ ] For each important edge used in the analysis, record in `docs/evidence_log.md`:
  node types it connects, edge type, confidence level, and an
  **extracted / inferred / ambiguous** label (PRD FR5, plan §6).
- [ ] Verify extracted relations against the actual source; flag inferred relations as
  lower confidence; mark ambiguous relations honestly (PRD §9, plan §8).
- [ ] Commit as `phase 5: graph reading and evidence log`.

## Phase 8 — Architecture report and Obsidian-style knowledge layer

- [ ] Write `docs/architecture_analysis.md` explaining the system architecture, not
  just the diagram (PRD FR7).
- [ ] Tie every architectural conclusion to specific graph evidence and its confidence
  level; cross-check with multiple lenses before asserting (PRD FR8, plan §8).
- [ ] Make sure no conclusion claims the graph "proves" anything that has not been
  verified (PRD NFR4).
- [ ] Build the Obsidian-style knowledge vault in `obsidian/` with notes that link code
  structure to planning documents, rationale, and dependencies (PRD FR6).
- [ ] Add traceability links so each conclusion can be followed back to its evidence and
  source (PRD SC5).
- [ ] Embed or reference the exported diagrams from `diagrams/` in the analysis.
- [ ] Commit as `phase 6: architecture analysis and knowledge layer`.

## Phase 9 — README and final documentation

- [ ] Confirm results exist before writing the README (PRD §5 — never write it early).
- [ ] Write `README.md` explaining the full workflow end to end: idea → PRD → plan →
  todo → codebase choice → graph → analysis → evidence → conclusions (PRD FR10).
- [ ] Link the README to the key artifacts: `prd.md`, `plan.md`, `todo.md`, `docs/`,
  `graph/`, `diagrams/`, `prompts/`, and `obsidian/`.
- [ ] Confirm all prompts and documentation are present and organized (PRD FR9).
- [ ] Commit as `phase 7: write final README`.

## Phase 10 — Final verification and GitHub submission

- [ ] Re-run the Phase 3 verification checklist and confirm SC1–SC7 are all satisfied.
- [ ] Confirm every important edge in the analysis has a node type, edge type,
  confidence level, and extracted/inferred/ambiguous label (SC3).
- [ ] Confirm the commit history shows gradual, meaningful commits (no single dump
  commit) (NFR2, SC6).
- [ ] Confirm the repository contains the source/clone reference, prompts, diagrams,
  documentation, and a final README (NFR3, SC6).
- [ ] Make the repository public and verify it is accessible without login.
- [ ] Push the final state to GitHub and confirm the remote matches local.
- [ ] Submit the public repository link.

---
## PRD Success Criteria Verification Checklist

This checklist maps the PRD success criteria to the later project tasks that will satisfy them.

* [ ] **SC1 — Whole-system understanding:** satisfied by Phase 6 graph generation and Phase 7 graph reading, where the analysis moves from individual files to a full system view.
* [ ] **SC2 — Meaningful graph concepts:** satisfied by Phase 7, where hubs, bridges, communities, centrality, dependencies, bottlenecks, and single points of failure are used as analytical lenses.
* [ ] **SC3 — Evidence-rated important edges:** satisfied by Phase 7, where every important edge used in the analysis is recorded in `docs/evidence_log.md` with node type, edge type, confidence level, and extracted/inferred/ambiguous label.
* [ ] **SC4 — Verified architectural conclusions:** satisfied by Phase 8, where conclusions in `docs/architecture_analysis.md` are checked against graph evidence and source evidence before being asserted.
* [ ] **SC5 — Obsidian-style traceability:** satisfied by Phase 8, where the `obsidian/` knowledge layer links code structure, rationale, dependencies, and evidence.
* [ ] **SC6 — Complete public GitHub repository:** satisfied by Phase 9 and Phase 10, where the repository includes documentation, prompts, diagrams, graph outputs, README, and gradual commits.
* [ ] **SC7 — PRD completed as its own artifact:** already satisfied by Phase 2A, where `prd.md` was written and committed before planning, TODO, codebase selection, or graph generation.


## Definition of Done

The assignment is **done** when all of the following hold:

- [ ] Exactly one unfamiliar, public Python codebase is selected and justified in
  `docs/codebase_selection.md` (FR1).
- [ ] A typed node/edge graph of the system has been generated with Graphify and
  exported to `graph/` and `diagrams/` (FR2, FR3).
- [ ] The required graph concepts (Hub, Bridge, Community, Centrality, Dependency,
  Bottleneck, Single Point of Failure, Traceability) are used meaningfully, not just
  named (FR4, SC2).
- [ ] Every important edge is rated in `docs/evidence_log.md` with node type, edge type,
  confidence, and an extracted/inferred/ambiguous label (FR5, SC3).
- [ ] `docs/architecture_analysis.md` presents evidence-based, verified conclusions with
  no unverified "proof" claims (FR7, FR8, SC4).
- [ ] An Obsidian-style knowledge layer in `obsidian/` traces code back to rationale,
  planning documents, and dependencies (FR6, SC5).
- [ ] Prompts and documentation used to drive the work are stored in `prompts/` (FR9).
- [ ] `README.md` explains the full workflow end to end and was written only after
  results existed (FR10).
- [ ] The work was committed gradually across phases, and the public GitHub repository
  contains the code/clone reference, prompts, diagrams, documentation, and README, and
  is submitted (NFR2, NFR3, SC6).

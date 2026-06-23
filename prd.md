# Product Requirements Document (PRD) — Assignment 4
Graphify / Grphify / graph-based analysis
**Project title:** Reverse Engineering a Python Codebase with Graphify and Obsidian Knowledge Architecture

**Course phase:** Phase 2A — PRD definition
**Assignment:** Assignment 4
**Status:** Draft (defines requirements only; no codebase selected, no code, no graph outputs yet)

> This PRD is written as part of the Vibe Coding lifecycle
> (Idea → PRD → Plan → TODO → Verify → Execute → Push). It defines *what* we
> intend to build and *how we will know it is done*, before any planning, task
> list, or implementation. It is based only on `docs/course_context.md` and
> `docs/assignment_understanding.md`.

---

## 1. Problem Statement

When we are handed an unfamiliar Python codebase, reading the source files one at
a time only gives a local view of the system. The relationships that matter most
for understanding the architecture — which components are central, how subsystems
connect, where the risky dependencies are — stay hidden inside the files and are
easy to miss or misjudge.

Without a structured way to represent the system, our understanding stays
informal and our conclusions are really just guesses about isolated files. We
need a method that turns scattered file-level reading into an analyzable,
whole-system view, and that keeps every claim about the system grounded in
evidence instead of intuition.

## 2. Project Goal

The goal of this project is to **reverse engineer an unfamiliar Python codebase**
and genuinely **understand its system architecture** using **Graphify /
graph-based analysis** together with **Obsidian-style knowledge documentation**.

Graphify is not treated as a drawing tool. It is treated as a **knowledge layer**
that connects:

- code structure,
- planning documents,
- rationale,
- dependencies,
- graph-based architectural insights.

The intended outcome is to move from *reading individual files* to
*understanding the whole system*, and to produce evidence-based architectural
conclusions rather than a picture that merely "looks like" the code.

## 3. Target User / Evaluator

The primary audience for this project is the **course professor / evaluator** of
Assignment 4.

The evaluator expects the student to act like a **project manager who guides AI
agents**, not like a passive user who asks the AI to produce everything at once.
Therefore the evaluator is looking for:

- disciplined process that follows the Vibe Coding lifecycle,
- evidence-based reasoning where conclusions are verified, not asserted,
- genuine architectural understanding of the chosen system,
- a public GitHub repository that grows through meaningful, gradual commits.

A secondary user is any **future reader/developer** who wants to understand the
selected codebase quickly through the produced graph and documentation.

## 4. Scope

This project (across all of its phases) covers:

- Selecting **one Python codebase** to analyze (the selection happens in a later
  phase, not now).
- Building a **graph-based representation** of that system using Graphify, where
  nodes and edges represent the components and their relationships.
- Applying real **graph concepts** to the analysis: Node, Edge, Hub, Bridge,
  Community, Centrality, Dependency, Bottleneck, Single Point of Failure, and
  Traceability.
- Treating **every edge as a claim** about a relationship, with an explicit
  evidence level.
- Producing an **Obsidian-style knowledge layer** that links code structure,
  planning documents, rationale, and dependencies.
- Writing a **written architectural analysis** with **evidence-based
  conclusions**.
- Capturing the **prompts and documentation** used throughout the work.
- Delivering a **final README** that explains the full workflow.
- Submitting everything through a **public GitHub repository** with gradual,
  meaningful commits.

**Scope of this PRD document specifically (Phase 2A):** define the product
requirements only. This document does not select the codebase, does not plan the
work, does not create a task list, and does not produce any graph output or code.

## 5. Out of Scope

The following are explicitly **out of scope** for this project as defined here:

- Choosing or committing to a specific Python codebase **in this PRD**
  (that decision belongs to a later phase).
- Writing any **code** or running any tooling at this stage.
- Generating any **graph outputs**, diagrams, or analysis results at this stage.
- Editing or producing `plan.md`, `todo.md`, or `README.md` as part of Phase 2A.
- Writing the **final README before results actually exist**.
- Asking the AI to **build the whole assignment at once**.
- Claiming the graph "proves" something **without verification**.
- Modifying, refactoring, or improving the analyzed codebase itself — the project
  is about *understanding* an existing system, not changing it.

## 6. Functional Requirements

The completed project (delivered through later phases) must satisfy:

- **FR1 — Codebase selection.** Exactly one Python codebase is selected and its
  selection is justified.
- **FR2 — Graph representation.** The system is represented as a graph of nodes
  and edges produced with Graphify.
- **FR3 — Node and edge typing.** Each node and edge is assigned a type, so the
  graph distinguishes between different kinds of components and relationships.
- **FR4 — Graph-concept analysis.** The analysis identifies and uses Hubs,
  Bridges, Communities, Centrality, Dependencies, Bottlenecks, and Single Points
  of Failure where they apply.
- **FR5 — Edge-as-claim evidence rating.** Every important edge used in the
  architectural analysis must be treated as a claim. For each analyzed edge, the
  report records: what type of nodes it connects, what type of edge it is, the
  confidence level, and whether the relation is **extracted, inferred, or
  ambiguous**.
- **FR6 — Knowledge layer / traceability.** The Obsidian-style documentation links
  code structure to planning documents, rationale, and dependencies so that
  conclusions are traceable back to their source.
- **FR7 — Written architectural analysis.** A written analysis explains the system
  architecture, not just the diagram.
- **FR8 — Evidence-based conclusions.** Every architectural conclusion is tied to
  graph evidence and confidence levels, and is verified before being asserted.
- **FR9 — Prompts and documentation captured.** The prompts and documentation used
  to drive the work are stored in the repository.
- **FR10 — Final README.** A final README explains the full workflow end to end,
  and is written only after results exist.

## 7. Non-Functional Requirements

- **NFR1 — Process discipline.** Work follows the Vibe Coding lifecycle in order
  (Idea → PRD → Plan → TODO → Verify → Execute → Push); phases are not skipped.
- **NFR2 — Gradual commits.** The repository grows through meaningful Git commits
  between phases, not a single final commit.
- **NFR3 — Public reproducibility.** Submission is a **public GitHub repository**
  that includes source code, prompts, diagrams, documentation, and `README.md`.
- **NFR4 — Evidence honesty.** No conclusion is stated as proven without
  verification; uncertainty is labeled honestly (extracted / inferred /
  ambiguous).
- **NFR5 — Clarity.** Documentation is clear enough that an evaluator or future
  reader can follow the workflow and understand the architecture without prior
  knowledge of the codebase.
- **NFR6 — Project-manager mindset.** The student guides the AI agents and makes
  the decisions; the AI is not asked to produce the whole assignment in one step.

## 8. Required Deliverables

By the end of the project, the repository must contain:

1. A **selected Python codebase** (chosen in a later phase).
2. A **graph-based representation** of the system.
3. A **written architectural analysis**.
4. **Evidence-based conclusions**, including node/edge types and confidence
   levels.
5. **Prompts and documentation** used during the work.
6. A **final README** explaining the full workflow.

All of the above are submitted through a **public GitHub repository**.

**Deliverable of Phase 2A specifically:** this `prd.md` file.

## 9. Evidence and Verification Requirements

Because every edge in the graph is a **claim about a relationship**, the project
must apply an evidence discipline before drawing any conclusion. For each edge,
the analysis must answer:

- **What type of node is this?**
- **What type of edge is this?**
- **What is the confidence level?**
- **Is the relation extracted, inferred, or ambiguous?**

Verification requirements:

- **Extracted** relations come directly from the code (e.g., an import or a call)
  and carry the highest confidence.
- **Inferred** relations are reasoned from indirect signals and must be flagged as
  lower confidence.
- **Ambiguous** relations are uncertain and must be marked as such rather than
  presented as fact.
- No architectural conclusion may claim the graph "proves" something **until it
  has been verified** against the code or planning evidence.

## 10. Success Criteria

The project is successful when:

- **SC1.** A graph-based representation moves the understanding from file-level
  reading to a whole-system view.
- **SC2.** Real graph concepts (Hub, Bridge, Community, Centrality, Dependency,
  Bottleneck, Single Point of Failure, Traceability) are used meaningfully, not
  just named.
- * **SC3.** Every important edge used to support an architectural conclusion
  includes a node type, an edge type, a confidence level, and an
  extracted/inferred/ambiguous label.
- **SC4.** Architectural conclusions are evidence-based and verified, with no
  unverified "proof" claims.
- **SC5.** The Obsidian-style knowledge layer traces code back to rationale,
  planning documents, and dependencies.
- **SC6.** The public GitHub repository shows gradual, meaningful commits across
  phases and includes source code, prompts, diagrams, documentation, and a final
  README.
- **SC7 (Phase 2A).** This PRD clearly defines the product requirements for the
  project and is committed as its own phase artifact.

## 11. Risks

- **R1 — Pretty-but-shallow graph.** Producing a graph that looks good but does not
  deepen architectural understanding. *Mitigation:* keep the focus on
  understanding the system, and require graph-concept analysis (FR4).
- **R2 — Overclaiming.** Asserting that the graph "proves" something without
  verification. *Mitigation:* enforce the evidence and verification requirements
  (Section 9) and label confidence levels.
- **R3 — Skipping the process.** Jumping to code or results before the PRD and Plan
  exist, or building everything at once. *Mitigation:* follow the Vibe Coding
  lifecycle and phase boundaries; Phase 2A produces only this PRD.
- **R4 — Single big commit.** Submitting the work in one final commit instead of
  gradual ones. *Mitigation:* commit meaningfully between phases (NFR2).
- **R5 — Premature codebase choice.** Locking in a Python codebase before the
  requirements and plan are ready, leading to a poor fit. *Mitigation:* defer the
  selection to a later phase, as required.
- **R6 — Weak traceability.** Conclusions that cannot be traced back to evidence or
  planning documents. *Mitigation:* maintain the Obsidian-style knowledge layer
  (FR6) and traceability links.

## 12. Vibe Coding Lifecycle Alignment

This project follows the course's Vibe Coding lifecycle:
**Idea → PRD → Plan → TODO → Verify → Execute → Push.**

- **Idea / Understanding (Phase 1).** Completed in
  `docs/assignment_understanding.md`, which aligned on *what* the assignment asks
  for, without choosing a codebase or writing code.
- **PRD (Phase 2A — this document).** Defines the product requirements: problem,
  goal, users, scope, requirements, deliverables, evidence rules, success
  criteria, and risks. It does **not** plan the work, create a task list, choose
  the codebase, or produce any output.
- **Plan (later phase).** Will turn these requirements into an implementation
  strategy (`plan.md`) — not edited here.
- **TODO (later phase).** Will break the plan into concrete tasks (`todo.md`) —
  not edited here.
- **Verify (throughout).** Every edge and conclusion will be checked against the
  evidence rules in Section 9 before being asserted.
- **Execute (later phase).** Codebase selection, graph generation, and the written
  analysis happen only after the PRD and Plan exist.
- **Push (throughout).** Work is committed gradually with meaningful messages to a
  public GitHub repository.

This PRD therefore deliberately stops at *defining requirements*, consistent with
the rule that we must not implement code before the PRD and Plan exist, must not
write the final README before results exist, and must not build the whole
assignment at once.

---

## File Changed

- **Created `prd.md`** (this file) — no other files were created or modified.

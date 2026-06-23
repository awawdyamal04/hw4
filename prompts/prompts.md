# Prompt Log — Assignment 4

This file records the main prompts used to guide the AI-agent workflow during Assignment 4.

The project followed the Vibe Coding lifecycle:

Idea -> PRD -> Plan -> TODO -> Verify -> Execute -> Push

The prompts below are the main project-management prompts that shaped the repository artifacts. They are not every message from the conversation, but they show how the AI agent was guided step by step.

---

## Phase 1 — Assignment Understanding

Prompt used:

Read docs/course_context.md first.

We are working only on Phase 1 of Assignment 4.

Your task is to create docs/assignment_understanding.md based only on docs/course_context.md.

Do not create PRD.
Do not create PLAN.
Do not create TODO.
Do not write code.
Do not choose a Python project yet.

Write a short but professional explanation of:
1. What Assignment 4 is about.
2. What the professor expects.
3. Why graph-based reverse engineering is useful.
4. What deliverables will eventually be needed.
5. Why we are splitting the work into phases.

---

## Phase 2A — PRD

Prompt used:

Read these files first:
- docs/course_context.md
- docs/assignment_understanding.md

We are working only on Phase 2A of Assignment 4.

Your task is to write prd.md only.

Do not edit plan.md.
Do not edit todo.md.
Do not edit README.md.
Do not write code.
Do not choose the Python codebase yet.
Do not create graph outputs yet.

The PRD should define the product requirements for:
Reverse Engineering a Python Codebase with Graphify and Obsidian Knowledge Architecture.

---

## Phase 2B — Plan

Prompt used:

Read these files first:
- docs/course_context.md
- docs/assignment_understanding.md
- prd.md

We are working only on Phase 2B of Assignment 4.

Your task is to write plan.md only.

Do not edit todo.md.
Do not edit README.md.
Do not write code.
Do not choose the Python codebase yet.
Do not run Graphify yet.
Do not create graph outputs yet.

The plan should explain how we will execute the project.

---

## Phase 2C — TODO

Prompt used:

Read these files first:
- docs/course_context.md
- docs/assignment_understanding.md
- prd.md
- plan.md

We are working only on Phase 2C of Assignment 4.

Your task is to write todo.md only.

Do not edit README.md.
Do not write code.
Do not choose the Python codebase yet.
Do not run Graphify yet.
Do not create graph outputs yet.

The TODO should break the plan into concrete tasks using Markdown checkboxes.

---

## Phase 4 — Codebase Selection

Prompt used:

Read these files first:
- docs/course_context.md
- docs/assignment_understanding.md
- prd.md
- plan.md
- todo.md

We are working only on Phase 4 of Assignment 4: Python codebase selection.

Your task is to create docs/codebase_selection.md only.

Evaluate these 3 candidate Python codebases:
1. itsdangerous — https://github.com/pallets/itsdangerous
2. click — https://github.com/pallets/click
3. requests — https://github.com/psf/requests

Use the selection criteria from plan.md:
- right size
- readable and public
- genuinely unfamiliar
- graph-friendly
- suitable for evidence-based graph analysis

Choose exactly one codebase.

---

## Phase 5 — Environment and Inventory

Prompt used:

Create docs/environment_and_inventory.md only.

Use the terminal outputs provided:
- python --version
- python -m pip --version
- ls external_projects/itsdangerous
- ls external_projects/itsdangerous/src/itsdangerous

The document must include:
1. Purpose of this phase
2. Python and pip environment check
3. Local codebase location
4. Top-level repository inventory
5. src/itsdangerous module inventory
6. Initial observation about why this project is graph-friendly
7. What was not done yet
8. Next step: prepare and run Graphify in a later phase

---

## Phase 6 — Graph Generation

Prompt used:

Create docs/graph_generation_log.md only.

Document the Graphify extraction that was run on:

external_projects/itsdangerous/src/itsdangerous

Include:
- command used
- graph size
- generated files
- copied output location
- what was not done yet
- next step

Graphify output:
- 135 nodes
- 334 edges
- 7 communities

---

## Phase 7 — Architecture Analysis

Prompt used:

Read:
- graph/itsdangerous/GRAPH_REPORT.md
- graph/itsdangerous/graph.json
- docs/graph_generation_log.md
- prd.md
- plan.md

Create docs/architecture_analysis.md.

Analyze the Graphify output for the itsdangerous codebase.

The report must include:
1. Overview of the graph: 135 nodes, 334 edges, 7 communities.
2. Main modules and their architectural roles.
3. Candidate hubs / central nodes.
4. Candidate bridges between subsystems.
5. Candidate communities.
6. Possible bottlenecks or single points of failure.
7. Evidence-based conclusions.
8. For every conclusion, explain whether it is extracted, inferred, or ambiguous.
9. What still needs manual verification.

Do not claim anything is proven unless the graph clearly supports it.

---

## Phase 8 — Evidence Log

Prompt used:

Read these files first:
- prd.md
- plan.md
- todo.md
- docs/architecture_analysis.md
- graph/itsdangerous/GRAPH_REPORT.md
- graph/itsdangerous/graph.json

We are working only on Phase 8 of Assignment 4: evidence log.

Your task is to create docs/evidence_log.md only.

Create an evidence log for the most important architectural claims from docs/architecture_analysis.md.

Do not claim that inferred edges are proven.
Use cautious language.
Keep the log focused on important evidence, not every edge in the graph.

---

## Phase 9 — Obsidian Knowledge Layer

Prompt used:

Read these files first:
- prd.md
- plan.md
- todo.md
- docs/architecture_analysis.md
- docs/evidence_log.md
- graph/itsdangerous/GRAPH_REPORT.md

We are working only on Phase 9 of Assignment 4: Obsidian-style knowledge layer.

Your task is to create an Obsidian-style knowledge layer in the obsidian/ folder.

Create only these files:
- obsidian/index.md
- obsidian/architecture_map.md
- obsidian/serializer.md
- obsidian/signer.md
- obsidian/encoding_and_exceptions.md
- obsidian/communities_and_bridges.md
- obsidian/verification_notes.md

Use wiki-style links.

---

## Phase 10 — Final README

Prompt used:

Read these files first:
- prd.md
- plan.md
- todo.md
- docs/architecture_analysis.md
- docs/evidence_log.md
- obsidian/index.md
- graph/itsdangerous/GRAPH_REPORT.md

We are working only on Phase 10 of Assignment 4: final README.

Your task is to write README.md only.

The README must explain the final project clearly:
- assignment goal
- selected codebase
- reproducibility information
- workflow followed
- graph generation summary
- main architecture findings
- evidence discipline
- repository structure
- how to view graph.html
- final conclusion

---

## General Agent Instructions Used Throughout

The AI agent was repeatedly instructed to:

- work on one phase at a time,
- avoid editing unrelated files,
- avoid running tools before the correct phase,
- avoid overclaiming inferred relationships,
- separate extracted evidence from inferred interpretation,
- keep the writing professional but student-like,
- summarize exactly which files changed.
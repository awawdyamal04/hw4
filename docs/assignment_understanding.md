# Assignment 4 — Understanding the Assignment

This document records our understanding of Assignment 4 based solely on
`docs/course_context.md`. It is a Phase 1 artifact: its only purpose is to align
on *what* we are being asked to do, before any PRD, plan, task list, or code.

---

## 1. What Assignment 4 Is About

Assignment 4 is about **reverse engineering an unfamiliar codebase** using
**Graphify / graph-based analysis** combined with **Obsidian-style knowledge
documentation**.

The goal is not merely to "draw the code." It is to **understand the system
architecture**. Graphify is treated as a **knowledge layer** that connects:

- code structure,
- planning documents,
- rationale,
- dependencies,
- graph-based architectural insights.

The central idea is to move from *reading individual files* to *understanding the
whole system*.

---

## 2. What the Professor Expects

The professor expects the student to work like a **project manager guiding AI
agents** — not a passive user who asks the AI to build everything at once.
Specifically:

- **Follow the Vibe Coding lifecycle:** Idea → PRD → Plan → TODO → Verify →
  Execute → Push.
- **Commit gradually:** the repository should grow through meaningful commits
  between phases, not a single final submission.
- **Use real graph concepts** in the analysis: Node, Edge, Hub, Bridge,
  Community, Centrality, Dependency, Bottleneck, Single Point of Failure, and
  Traceability.
- **Treat every edge as a claim** about a relationship. Before drawing
  conclusions, the analysis must ask: What type of node is this? What type of
  edge is this? What is the confidence level? Is the relation **extracted,
  inferred, or ambiguous**?
- **Verify before asserting:** never claim the graph "proves" something without
  verification.

In short, the emphasis is on disciplined process, evidence-based reasoning, and
genuine architectural understanding — not on producing output quickly.

---

## 3. Why Graph-Based Reverse Engineering Is Useful

Reading source files one at a time gives only a local view and hides the
relationships that matter most. Representing the system as a graph turns informal
intuition into something analyzable:

- **Hubs and centrality** show which components are most connected and most
  important.
- **Bridges and communities** reveal how subsystems are separated and where they
  join.
- **Bottlenecks and single points of failure** expose architectural risk.
- **Dependencies and traceability** link code back to rationale and planning
  documents.

Because each edge is stated as an evidence-rated claim, the graph lets us reason
about the whole system and check our conclusions, rather than guessing from
isolated files.

---

## 4. Deliverables That Will Eventually Be Needed

The final project (produced in later phases, not now) is expected to show:

1. A **selected Python codebase**.
2. A **graph-based representation** of the system.
3. A **written architectural analysis**.
4. **Evidence-based conclusions** (with node/edge types and confidence levels).
5. **Prompts and documentation**.
6. A **final README** explaining the full workflow.

Submission is through a **public GitHub repository** that includes source code,
prompts, diagrams, documentation, and a `README.md`.

---

## 5. Why We Are Splitting the Work Into Phases

We split the work into phases because the course method requires us to avoid
skipping straight to results. The rules state that we must **not**:

- implement code before the PRD and Plan exist,
- write the final README before results exist,
- ask the AI to build the whole assignment at once,
- claim the graph proves something without verification,
- skip Git commits between phases.

Phasing enforces the project-manager mindset the assignment demands: each phase
produces a verifiable artifact and a meaningful commit, decisions happen in the
right order (understand → define → plan → execute → verify → push), and every
conclusion stays grounded in evidence. This Phase 1 document therefore stops at
*understanding* — it deliberately does not choose a codebase, write a PRD, plan,
build a task list, or write any code.

---

## File Changed

- **Updated `docs/assignment_understanding.md`** (this file) — no other files were
  created or modified.

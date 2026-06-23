# Course Context for Assignment 4

## Course Method

The course follows a Vibe Coding lifecycle:
Idea -> PRD -> Plan -> TODO -> Verify -> Execute -> Push.

The professor expects the student to work like a project manager who guides AI agents, not like a passive user asking the AI to create everything at once.

The repository should be updated gradually with meaningful commits, not submitted in one final commit.

## Submission Requirements

The homework submission should be through a public GitHub repository.

The repository should include:
- source code
- prompts
- diagrams
- documentation
- README.md

## Assignment 4 Topic

Assignment 4 is about reverse engineering an unfamiliar codebase using Graphify / graph-based analysis and Obsidian-style knowledge documentation.

The goal is not only to draw code, but to understand the system architecture.

Graphify should be treated as a knowledge layer that connects:
- code structure
- planning documents
- rationale
- dependencies
- graph-based architectural insights

## Graph Concepts Required

The analysis should use graph concepts such as:
- Node
- Edge
- Hub
- Bridge
- Community
- Centrality
- Dependency
- Bottleneck
- Single Point of Failure
- Traceability

## Evidence Levels

Every edge in the graph should be treated as a claim about a relationship.

Before drawing conclusions, the analysis should ask:
- What type of node is this?
- What type of edge is this?
- What is the confidence level?
- Is the relation extracted, inferred, or ambiguous?

## Main Idea

Graphify is not just a drawing tool.
It is a way to move from reading individual files to understanding the whole system.

The final project should show:
1. A selected Python codebase.
2. A graph-based representation of the system.
3. A written architectural analysis.
4. Evidence-based conclusions.
5. Prompts and documentation.
6. A final README explaining the full workflow.

## What We Must Not Do Too Early

Do not implement code before PRD and Plan.
Do not write the final README before results exist.
Do not ask Claude to build the whole assignment at once.
Do not claim the graph proves something without verification.
Do not skip Git commits between phases.
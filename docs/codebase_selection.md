# Codebase Selection — Assignment 4

**Course phase:** Phase 4 — Python codebase selection
**Assignment:** Assignment 4
**Status:** Selection only (codebase chosen and justified; nothing cloned yet, no Graphify run, no graph outputs, `README.md` untouched)

> This is the **codebase-selection** step that the plan defers out of Phase 2
> (`plan.md` §3, PRD FR1). It chooses **exactly one** unfamiliar, public Python
> codebase to reverse engineer in the later phases, and records the reasoning and
> a reproducibility plan. It does **not** clone anything, run Graphify, generate
> graph outputs, or edit `README.md`. It is based only on `docs/course_context.md`,
> `docs/assignment_understanding.md`, `prd.md`, and `plan.md`.

---

## 1. Purpose of This Phase

The purpose of Phase 4 is to **select a single Python codebase** that we will
reverse engineer with Graphify in the later phases, and to **justify that choice**
against the selection criteria already fixed in `plan.md` §3.

This matters because the quality of the entire downstream analysis — the graph,
the architectural conclusions, and the evidence ratings — depends on choosing a
system that is the *right* subject. We want a codebase that:

* is small enough to analyze **honestly** within the assignment, so we are not
  forced to overclaim about parts we never really examined;
* is large enough to have **real architecture** worth analyzing;
* is **public and reproducible**;
* is **genuinely unfamiliar**, since the assignment is about *reverse
  engineering*, not documenting something we already know;
* is **graph-friendly**, with clear imports, modules, classes, and calls that
  Graphify can turn into meaningful nodes and edges;
* is **suitable for evidence-based graph analysis**, meaning relationships are
  mostly *extracted* from explicit code rather than buried in dynamic,
  hard-to-trace behavior.

The deliverable of this phase is this `docs/codebase_selection.md` file and the
commit that records it.

---

## 2. Candidate Comparison Table

Each candidate is a well-known, public, open-source Python project. They are
scored against the `plan.md` §3 criteria plus the PRD's evidence-suitability
requirement. Ratings are relative to *this assignment's* goals: a focused,
honest, evidence-based graph analysis.

| Criterion                                | **itsdangerous**                                                                                                     | **click**                                                                                                                     | **requests**                                                                                                                                   |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Right size**                           | Strong — small, focused library with a limited number of core modules. Analyzable end to end.                        | Medium — noticeably larger, with CLI core, decorators, parameter types, parser, terminal UI, formatting, and testing helpers. | Medium — mid-sized, with sessions, models, adapters, API helpers, auth, cookies, and hooks.                                                    |
| **Readable and public**                  | Strong — Pallets project, BSD-3-Clause licensed, clean and well-documented code.                                     | Strong — Pallets project, BSD-3-Clause licensed, widely used and documented.                                                  | Strong — PSF project, Apache-2.0 licensed, very widely used and documented.                                                                    |
| **Genuinely unfamiliar**                 | Strong — cryptographic signing is a focused area that many developers may use indirectly but rarely read internally. | Medium — CLI patterns and decorators are broadly familiar to many Python developers.                                          | Weak — `requests` is one of the most familiar Python libraries, so there is less reverse-engineering value.                                    |
| **Graph-friendly**                       | Strong — clear modules, imports, class relationships, and mostly static relationships. Edges should map cleanly.     | Strong but noisy — rich structure, but decorators and dynamic dispatch may create harder-to-classify relationships.           | Medium — clear module layout, but important behavior relies on external dependencies, so some edges leave the analyzed boundary.               |
| **Suitable for evidence-based analysis** | Strong — many relationships can be extracted directly from imports, inheritance, and calls.                          | Medium — decorator and registration patterns may create more inferred edges.                                                  | Medium — key behavior often crosses into third-party dependencies, making some important relationships harder to verify inside one repository. |
| **Overall fit**                          | **Best fit**                                                                                                         | Good, but bigger and noisier                                                                                                  | Weakest fit for this assignment                                                                                                                |

---

## 3. Final Selected Codebase

**Selected codebase: `itsdangerous` by Pallets.**

This is the one codebase we will reverse engineer in the later phases.

Repository:

```text
https://github.com/pallets/itsdangerous
```

---

## 4. Why It Was Selected

`itsdangerous` is selected because it is the strongest fit for an honest,
evidence-based graph analysis.

First, it has the **right size**. It is small enough that we can realistically
analyze the whole system, but it is not trivial. This helps avoid producing a
pretty graph without real understanding.

Second, it has **real architecture** despite being focused. The project contains
meaningful internal relationships between signing, serialization, timed variants,
URL-safe variants, encoding, and exceptions. That gives Graphify useful material
for nodes, edges, hubs, dependencies, communities, and possible bottlenecks.

Third, it is **graph-friendly**. Many of its relationships are expected to be
visible through imports, inheritance, and direct calls. This is important because
the assignment requires us to treat graph edges as evidence-rated claims:
extracted, inferred, or ambiguous.

Fourth, it is **genuinely unfamiliar enough** for reverse engineering. Many
developers may use it indirectly through Flask sessions, but fewer have read its
internal implementation. That makes it a better subject than documenting a
library we already understand.

Finally, it is **public and reproducible**. It is hosted on GitHub, belongs to the
Pallets organization, and uses a BSD-3-Clause license. This means the evaluator
can inspect the same source code and follow the analysis path.

---

## 5. Why the Other Candidates Were Not Selected

### `click` — not selected

`click` is a strong Python project and could work for graph analysis, but it is
larger and noisier for this assignment. It includes CLI core logic, decorators,
parameter types, command parsing, terminal utilities, formatting, and testing
helpers.

The main problem is not quality. The problem is scope. Because `click` is larger,
there is a higher risk that we would analyze only part of the system and then
overclaim about the rest. It also uses decorators and dynamic behavior, which may
produce more inferred or ambiguous relationships that require extra verification.

For this assignment, it is a good runner-up, but not the safest choice.

### `requests` — not selected

`requests` is also a high-quality Python project, but it is not the best fit here.

First, it is extremely familiar. Since the assignment is about reverse
engineering an unfamiliar codebase, a very famous project weakens the learning
value.

Second, important behavior in `requests` depends on external libraries such as
`urllib3`, `certifi`, and charset-related dependencies. That means some important
architectural relationships cross outside the selected repository. This makes the
analysis boundary less clean and can weaken the evidence-based traceability we
need.

For these reasons, `requests` is the weakest fit of the three candidates.

---

## 6. Repository URL

Selected codebase:

```text
https://github.com/pallets/itsdangerous
```

Candidates considered:

```text
https://github.com/pallets/click
https://github.com/psf/requests
```

---

## 7. Reproducibility Plan

The actual cloning and tool setup will happen later, not in this phase.

In the environment setup phase, we will:

1. **Clone later into `external_projects/`.**
   The selected `itsdangerous` repository will be cloned locally into
   `external_projects/` only when the environment setup phase begins.

2. **Record the commit hash.**
   We will pin the clone to a specific commit or release tag and record that exact
   commit hash in the repository documentation. This allows the analysis to be
   reproduced later.

3. **Do not commit external project code.**
   `external_projects/` is kept in `.gitignore`, so the cloned third-party source
   is **never committed** to our repository. We keep only the reference to it:
   URL, selection justification, and pinned commit hash.

4. **Record tool settings later.**
   When Graphify is eventually run, the exact tool version, settings, and commands
   will be recorded alongside the outputs so the run is repeatable.

---

## 8. Next Step After Selection

The immediate next step is to commit this selection as its own phase artifact.

Suggested commit message:

```text
phase 4: select python codebase
```

After this commit, the project proceeds to the environment and tool setup phase.
Only then will we clone `itsdangerous` into `external_projects/`, record the
commit hash, and verify the Graphify workflow.

This phase ends at **selection only**:

* no cloning,
* no Graphify,
* no graph outputs,
* no README changes.

---

## File Changed

* **Created `docs/codebase_selection.md`** — no other files were created or
  modified.

# Environment and Initial Codebase Inventory — Assignment 4

**Course phase:** Phase 5B — Environment check and initial codebase inventory
**Assignment:** Assignment 4
**Status:** Environment checked and codebase structure inspected; no Graphify run yet, no graph outputs yet.

---

## 1. Purpose of This Phase

The purpose of this phase is to confirm that the selected Python codebase exists locally, record the basic development environment, and inspect the initial file structure before running Graphify / Grphify.

This phase does not analyze the architecture yet. It only prepares a factual inventory that will help the later graph-generation and graph-reading phases.

This phase follows the project plan: after selecting the codebase and recording its reproducibility information, we first verify the environment and inspect the codebase before generating any graph outputs.

---

## 2. Python and Pip Environment Check

The following commands were run from the main Assignment 4 repository:

```bash
python --version
```

Output:

```text
Python 3.8.0
```

Command:

```bash
python -m pip --version
```

Output:

```text
pip 19.2.3 from C:\Users\U1\AppData\Local\Programs\Python\Python38\lib\site-packages\pip (python 3.8)
```

Observation:

The machine has Python 3.8 installed and pip is available. This is enough for a basic environment check, but later tool setup may require checking whether Graphify / Grphify supports this Python version or whether a newer Python version or virtual environment is needed.

---

## 3. Local Codebase Location

The selected codebase, `itsdangerous`, was cloned locally into:

```text
external_projects/itsdangerous
```

The folder `external_projects/` is ignored by Git, so the third-party source code is not committed into this Assignment 4 repository.

This is intentional. The assignment repository stores our documentation, prompts, graph outputs, analysis, and reproducibility notes, while the external project code remains referenced by URL and pinned commit hash.

---

## 4. Top-Level Repository Inventory

The following command was used to inspect the top-level structure of the selected codebase:

```bash
ls external_projects/itsdangerous
```

Output:

```text
CHANGES.rst
LICENSE.txt
README.md
docs/
pyproject.toml
src/
tests/
uv.lock
```

Initial observations:

* `README.md`, `CHANGES.rst`, and `LICENSE.txt` provide project-level documentation.
* `pyproject.toml` and `uv.lock` indicate that this is a structured Python project with dependency and packaging metadata.
* `src/` contains the main implementation code.
* `tests/` contains tests that can help verify behavior and support later evidence checking.
* `docs/` may contain additional explanations that help connect code structure to rationale.

---

## 5. `src/itsdangerous` Module Inventory

The following command was used to inspect the main Python package:

```bash
ls external_projects/itsdangerous/src/itsdangerous
```

Output:

```text
__init__.py
__main__.py
encoding.py
exc.py
py.typed
serializer.py
signer.py
timed.py
url_safe.py
```

Initial observations:

* `signer.py` appears likely to contain the core signing logic.
* `serializer.py` appears likely to connect signing with serialization.
* `timed.py` likely adds time-based behavior to signing or serialization.
* `url_safe.py` likely handles URL-safe variants.
* `encoding.py` likely contains encoding helpers used by other modules.
* `exc.py` likely defines shared exception classes.
* `__init__.py` likely exposes the public API.
* `__main__.py` may define command-line entry behavior or module execution behavior.
* `py.typed` indicates that the package provides typing information.

These files suggest that the codebase is compact but still architecturally meaningful.

---

## 6. Initial Observation: Why This Project Is Graph-Friendly

The initial inventory supports the earlier codebase-selection decision.

`itsdangerous` is graph-friendly because it has:

* a clear `src/` package structure,
* a small number of focused modules,
* likely explicit imports between modules,
* likely class/function relationships around signing, serialization, encoding, timed behavior, URL-safe behavior, and exceptions,
* tests and documentation that can support later verification.

This makes it a good candidate for graph-based reverse engineering. The graph should be able to represent modules, classes, functions, imports, calls, and dependencies without becoming too large or too noisy.

At the same time, the project is not trivial: the modules suggest meaningful relationships between core signing logic, serialization layers, timed variants, URL-safe variants, encoding helpers, and shared exceptions.

---

## 7. What Was Not Done Yet

This phase is only an environment and inventory check.

The following were not done yet:

* Graphify / Grphify was not installed or run.
* No graph outputs were generated.
* No `graph.json`, `graph.html`, or graph report was created.
* No architectural conclusions were written.
* No evidence log was created.
* No Obsidian-style knowledge layer was created.
* `README.md` was not edited.

---

## 8. Next Step

The next step is Phase 5C / Phase 6 preparation: verify the Graphify / Grphify workflow and decide how to generate the graph outputs for the selected `itsdangerous` codebase.

Only after the tool workflow is verified should we run the graph generation phase and produce graph artifacts.

---

## File Changed

* **Created `docs/environment_and_inventory.md`**.

# Graphify Tool Check — Assignment 4

**Course phase:** Phase 5C — Graphify tool availability check
**Assignment:** Assignment 4
**Status:** Graphify command verified; graph generation not run yet.

---

## Purpose of This Phase

The purpose of this phase is to confirm that the `graphify` command is available
and working before running it on the selected Python codebase.

This phase does not generate graph outputs and does not analyze the architecture
yet. It only verifies that the tool can be called from the terminal.

---

## Command Used

```bash
graphify --help
```

---

## Result

The command worked and printed the Graphify help menu.

The available commands include:

* `install`
* `uninstall`
* `purge`
* `extract <path>`
* `path "A" "B"`
* `explain "X"`
* `diagnose-multigraph`
* `clone <github-url>`
* `merge-graphs`
* `add <url>`
* `watch <path>`
* `update <path>`
* `cluster-only <path>`
* `label <path>`
* `query "question"`
* `affected "X"`
* `save-result`

This confirms that Graphify is installed and available from Git Bash.

---

## What Was Not Done Yet

The following were not done in this phase:

* Graphify was not run on `itsdangerous`.
* No graph outputs were generated.
* No `graph.json` was created yet.
* No architecture analysis was written.
* No evidence log was created.
* `README.md` was not edited.

---

## Next Step

The next step is Phase 6: run Graphify extraction on the selected codebase:

```text
external_projects/itsdangerous/src/itsdangerous
```

and inspect the generated graph outputs.

---

## File Changed

* **Created `docs/graphify_tool_check.md`**.

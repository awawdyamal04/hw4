# Codebase Reproducibility — Assignment 4

**Course phase:** Phase 5A — Codebase clone and reproducibility record
**Assignment:** Assignment 4
**Status:** Codebase cloned locally; no Graphify run yet, no graph outputs yet.

---

## Selected Codebase

**Project:** itsdangerous
**Organization:** Pallets
**Repository URL:** https://github.com/pallets/itsdangerous

This is the codebase selected in `docs/codebase_selection.md` for reverse engineering with Graphify / Grphify.

---

## Local Clone Location

The repository was cloned locally into:

```text
external_projects/itsdangerous
```

The `external_projects/` folder is ignored by Git and is not committed to this repository.

---

## Pinned Version

The analyzed codebase is pinned to the following commit:

```text
672971d66a2ef9f85151e53283113f33d642dabd
```

Git description:

```text
2.1.x-60-g672971d
```

This pin allows the analysis to be reproduced later using the exact same source version.

---

## Clone Command Used

```bash
git clone https://github.com/pallets/itsdangerous.git external_projects/itsdangerous
```

---

## Verification Commands Used

Inside `external_projects/itsdangerous`, the following commands were used:

```bash
git rev-parse HEAD
git describe --tags --always
```

Output:

```text
672971d66a2ef9f85151e53283113f33d642dabd
2.1.x-60-g672971d
```

---

## What Was Not Done Yet

This phase only cloned the selected codebase and recorded its exact version.

The following were not done yet:

* Graphify was not run.
* No graph outputs were generated.
* No architecture analysis was written.
* No evidence log was created.
* README was not edited.

---

## File Changed

* **Created `docs/codebase_reproducibility.md`**.

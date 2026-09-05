# Claude-MEMORY.md

Auditable mirror of Claude's persistent auto-memory writes concerning the
TidySweep project. Claude's actual memory store lives outside this
repository (per-user, cross-session); this file is the human-readable,
version-controlled record of what has been written there, kept current per
the operator's global governance standard.

## 2026-09-05 — Project inception

- Created new repo (`TidySweep`) for a multi-room toy-cleaning robot
  (FIRST Robotics-style debris bot × Roomba hybrid).
- Firm constraints captured: BeagleBone ecosystem compute platform;
  CC-BY-SA 4.0 for documentation; CERN-OHL-P 2.0 for hardware; must handle
  static obstacles (thresholds, furniture) and living obstacles (cats, dogs,
  humans) as a distinct non-contact hazard class; must pick up irregular
  objects up to 2 in (50.8 mm) cubes; must empty hopper into a stationary
  external bin; must monitor battery and autonomously return to a charging
  dock.
- Ran `planning-and-task-breakdown` → produced `tasks/plan.md` and
  `tasks/todo.md` (Phase 0-5 breakdown).
- Ran `project-overseer` in greenfield mode → stood up root governance
  federation (`AGENTS.md`, `CLAUDE.md`, `README.md`, `LICENSE-DOCS`,
  `LICENSE-HARDWARE`, `LICENSING.md`, `REFERENCES.md`, `TODO.md`,
  `PROJECT_INDEX.md`) as Phase 0 of the WBS.
- Phase 1 (ConOps/requirements) is blocked pending operator input on: room/
  floor inventory, threshold height, bin location/interface, charging dock
  scheme, BOM budget ceiling, and desired autonomy level (supervised vs.
  fully unsupervised operation). See `tasks/plan.md` "Open Questions".

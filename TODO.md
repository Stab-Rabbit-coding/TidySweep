# TidySweep — Work Breakdown Structure (WBS)

Formal WBS per the project governance standard in [`AGENTS.md`](AGENTS.md).
Detailed task acceptance criteria and dependencies for the currently-active
phase live in [`tasks/todo.md`](tasks/todo.md) and [`tasks/plan.md`](tasks/plan.md);
this file is the authoritative top-level index — every item here maps 1:1
to an entry in those files. Status legend: `[x]` complete, `[~]` in
progress, `[!]` reopened for rework, `[ ]` ready/not started, `[X]` blocked.

## 0. Governance & Compliance

- [x] 0.1 Root governance files (CLAUDE.md, AGENTS.md, README.md)
- [x] 0.2 Licensing infrastructure (LICENSE-DOCS, LICENSE-HARDWARE, LICENSING.md)
- [x] 0.3 REFERENCES.md skeleton with initial BeagleBone SKU citations
- [x] 0.4 TODO.md WBS + PROJECT_INDEX.md + Claude-MEMORY.md
- [ ] 0.5 Select firmware/software source-code license (CERN-OHL-P does not itself license software; see `LICENSING.md` open item)

## 1. Requirements & Concept of Operations (ConOps)

- [X] 1.1 ConOps.md — mission profile — **blocked**: needs user input on room/floor inventory (see Open Questions, `tasks/plan.md`)
- [ ] 1.2 Obstacle taxonomy (static thresholds/furniture vs. dynamic/living: cats, dogs, humans)
- [ ] 1.3 Payload envelope (2 in / 50.8 mm cube max) + ASTM F963 small-parts exclusion citation
- [X] 1.4 Mass/power/space budget skeleton — **blocked**: depends on 1.1-1.3

## 2. Mechanical Subsystem

- [ ] 2.1 Chassis & drivetrain trade study (differential vs. tracked, threshold-climbing)
- [ ] 2.2 Intake/pickup mechanism concept (pinch-point guarding standard required — see REFERENCES.md open items)
- [ ] 2.3 Hopper + bin-emptying mechanism concept
- [ ] 2.4 Charging dock mechanical interface concept

## 3. Electrical / Compute Subsystem

- [ ] 3.1 BeagleBone SKU + sensor suite selection against I/O budget
- [ ] 3.2 Motor driver + power distribution architecture
- [ ] 3.3 Battery + charging safety-standard selection (REFERENCES.md entry required)

## 4. Software Subsystem

- [ ] 4.1 Navigation/SLAM stack selection
- [ ] 4.2 Obstacle avoidance behavior tree (distinct living-obstacle response class)
- [ ] 4.3 Pickup control logic
- [ ] 4.4 Dock/empty-hopper routine
- [ ] 4.5 Battery monitoring + return-to-charger behavior

## 5. Integration & Validation

- [ ] 5.1 Bench integration smoke test
- [ ] 5.2 Static-obstacle field test
- [ ] 5.3 Supervised living-obstacle field test
- [ ] 5.4 Full end-to-end mission test (pickup → hopper → dock → dump → return-to-charge)

---

**Current phase:** Phase 0 (Governance & Compliance) complete. Phase 1
(Requirements & ConOps) is blocked on user input — see §1.1/§1.4 above and
the "Open Questions" section of `tasks/plan.md`.

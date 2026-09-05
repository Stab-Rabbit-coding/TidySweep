# Implementation Plan: TidySweep — Multi-Room Toy-Cleaning Robot

## Overview

TidySweep is an autonomous multi-room floor robot that finds, picks up, and hauls
away irregular toys and debris up to 2 in (50.8 mm) cubes, then empties its
onboard hopper into a stationary external bin and returns to a charging dock
under its own battery management. It is a hybrid of a FIRST Robotics-style
active debris-collection mechanism (intake roller/claw + hopper) and a Roomba-
style autonomous floor-coverage robot (LIDAR/vision SLAM, docking, scheduled
coverage). Compute and motor control run on the BeagleBone ecosystem
(BeagleBone AI-64 or BeagleBone Black + PocketBeagle satellite, TBD by Task 3).
All documentation ships under CC-BY-SA 4.0; all hardware (mechanical CAD,
schematics, PCB layout) ships under CERN-OHL-P 2.0. This is a real build —
every part is fabricated or procured, no conceptual placeholders.

This plan produces the *scaffolding and Phase 0/1 breakdown only*. It hands off
to `project-overseer` to convert this into the repo's authoritative TODO.md WBS
and execute task-by-task, and to `compound-engineering:ce-strategy` for
higher-level sequencing/risk framing across phases. Detailed mechanical/
electrical/software design tasks beyond Phase 1 are intentionally left at
medium granularity here — project-overseer will decompose each Phase 2+ item
further as its own WBS branch when that phase opens.

## Architecture Decisions

- **Compute platform is a firm constraint (BeagleBone ecosystem)**, not an
  open trade study. Task 3 selects *which* BeagleBone SKU(s) satisfy the I/O
  budget (this is a size/selection decision, not a platform decision).
- **Vertical-slice ordering**: governance/licensing scaffolding first (it
  gates every subsequent commit's compliance), then a single "detect obstacle
  → stop/avoid" slice, then a single "detect toy → pick up → hopper" slice,
  then "hopper full → dock → empty into bin" slice, then "battery low → return
  to dock" slice, then multi-room navigation/mapping ties the slices together.
  This mirrors the Roomba-analogy subsystems the user listed in requirements
  order.
- **Licensing files are infrastructure, not an afterthought**: CC-BY-SA 4.0
  LICENSE-DOCS and CERN-OHL-P 2.0 LICENSE-HARDWARE must exist before any
  design or doc file is committed, per the user's global authenticity/
  attribution standard.
- **Living obstacles (cats/dogs/humans) are a distinct hazard class** from
  static furniture: they move unpredictably and must never be contacted, let
  alone driven over or intake-rollered. This drives a required "biological
  object" detection class (thermal/depth+motion, not just LIDAR occupancy)
  called out explicitly in Phase 3 rather than assumed to fall out of generic
  obstacle avoidance.
- **Standards vetting is mandatory before any safety-relevant spec is
  implemented** (per user's global Standards Vetting Policy): pinch-point/
  intake-roller guarding, battery charging safety (UL 2054 / IEC 62133-class
  reasoning), and toy-size choking-hazard handling logic against ASTM F963
  small-parts thresholds all need a REFERENCES.md entry before the mechanism
  is finalized, not after.

## Task List

### Phase 0: Repository & Governance Scaffolding

- [ ] Task 1: Root governance files (CLAUDE.md, AGENTS.md, README.md)
- [ ] Task 2: Licensing infrastructure (CC-BY-SA 4.0 docs, CERN-OHL-P 2.0 hardware)
- [ ] Task 3: REFERENCES.md skeleton + BeagleBone SKU selection citation
- [ ] Task 4: TODO.md formal WBS skeleton + PROJECT_INDEX.md + Claude-MEMORY.md stub

### Checkpoint: Phase 0

- [ ] Repo has LICENSE-DOCS (CC-BY-SA-4.0), LICENSE-HARDWARE (CERN-OHL-P-2.0), CLAUDE.md, AGENTS.md, REFERENCES.md, TODO.md, PROJECT_INDEX.md
- [ ] `git log` shows an initial commit with all scaffolding files
- [ ] No design or code file exists yet without its governing license file already in place

### Phase 1: Requirements & Concept of Operations (ConOps)

- [ ] Task 5: Write ConOps.md — mission profile (rooms, floor types, thresholds height, session duration, duty cycle)
- [ ] Task 6: Define obstacle taxonomy (static: thresholds/furniture; dynamic: cats/dogs/humans) with required detection ranges and response behaviors
- [ ] Task 7: Define payload envelope (2 in / 50.8 mm cube max, irregular shape, mass range) and hopper capacity target
- [ ] Task 8: Mass/power/space budget skeleton (per user's global weight-and-balance requirement) — placeholder table with real target numbers, not TBD

### Checkpoint: Phase 1

- [ ] ConOps.md, obstacle taxonomy, payload envelope, and mass/power budget all reviewed by user before mechanical/electrical design begins

### Phase 2: Mechanical Subsystem (hands off to project-overseer for sub-WBS)

- [~] Task 9: Chassis & drivetrain concept — differential drive (wheeled) decided; wheel-count/caster layout coupled to Task 10, not yet closed — see `DrivetrainConcept.md`
- [ ] Task 10: Intake/pickup mechanism concept (FRC-style roller/claw sized for 2 in cube, with guarding per ASTM/pinch-point standard) — determines final caster placement per `DrivetrainConcept.md`; check spare BeagleBone Blue H-bridge capacity (2 of 4 channels unused by drivetrain) before assuming a separate intake motor driver is needed
- [ ] Task 11: Hopper + bin-emptying mechanism concept (onboard hopper geometry with mesh/perforated bottom for passive dirt-shedding, dock-and-dump actuation) — see `HopperMechanism.md`
- [ ] Task 12: Charging dock mechanical interface (docking alignment geometry, pogo-pin contact) — **co-designed with Task 25/`ChargingDumpStation.md`**: the charging dock and the dump station are one physical unit, not two locations

### Phase 3: Electrical / Compute Subsystem (hands off to project-overseer)

- [ ] Task 13: BeagleBone SKU + peripheral sensor suite selection (LIDAR/depth camera, thermal/PIR for living-obstacle detection, IMU, wheel encoders)
- [ ] Task 14: Motor driver + power distribution architecture sized to drivetrain + intake motor loads
- [ ] Task 15: Battery + charging system selection with safety-standard citation (REFERENCES.md entry required before finalizing)

### Phase 4: Software Subsystem (hands off to project-overseer)

- [ ] Task 16: Navigation/SLAM stack selection for multi-room mapping
- [ ] Task 17: Obstacle avoidance behavior tree, with a distinct living-obstacle (cat/dog/human) response class
- [ ] Task 18: Pickup control logic (detect toy → approach → intake)
- [ ] Task 19: Dock/empty-hopper routine (hopper-full trigger → navigate to bin → actuate dump)
- [ ] Task 20: Battery monitoring + return-to-charger behavior

### Checkpoint: Phase 4

- [ ] Each subsystem's Phase 2-4 concept task has a corresponding project-overseer WBS branch open before implementation starts

### Phase 5: Integration & Validation

- [ ] Task 21: Bench integration of compute + motor control + one sensor (smoke test)
- [ ] Task 22: Single-room obstacle-avoidance field test (static obstacles only)
- [ ] Task 23: Living-obstacle field test (supervised, with actual pet/human present)
- [ ] Task 24: Full pickup → hopper → dock → dump → return-to-charge end-to-end test

### Phase 6: Charging & Dump Station Subsystem (added 2026-09-05, revised same day — merged with the charging dock into one physical station; mains-powered, separate budget from the robot's $500 BOM)

- [ ] Task 25: Station fan-separator + docking-bay mechanical concept (airflow-based toy/light-trash density separation, co-designed with Task 12) — see `ChargingDumpStation.md`
- [ ] Task 26: Station electrical design (fan/blower motor, one shared mains PSU feeding both the fan and the robot's DC charging contacts at 9-18V, dump-activation trigger derived from the docking-contact signal rather than a separate sensor)
- [ ] Task 27: Station safety-standard vetting (household appliance safety, fan-guarding, mains cord safety, exposed-charging-contact short-circuit risk) before fabrication

### Checkpoint: Phase 6

- [ ] Station concept validated against the placeholder $220 budget in `ChargingDumpStation.md`; Task 12/25 docking-bay geometry reconciled into one design; safety citations added to `REFERENCES.md` before any station prototype is built

## Risks and Mitigations

| Risk | Impact | Mitigation |
| ------ | -------- | ------------ |
| BeagleBone I/O budget insufficient for LIDAR + depth cam + motor control simultaneously | High | Task 13 does an explicit I/O/throughput budget before SKU is locked; PocketBeagle satellite offload considered |
| Living-obstacle detection false-negatives (robot contacts a pet) | High — safety | Task 6/17 require a dedicated detection class and a conservative stop-distance; supervised field test (Task 23) gates any unsupervised operation |
| Intake mechanism creates a pinch/entanglement hazard | Medium — safety | Task 10 requires a guarding citation in REFERENCES.md before fabrication (ASTM/ANSI machine-guarding class standard) |
| Toy choking-hazard interaction (robot handling small-parts-adjacent toys) | Medium | Task 7 explicitly bounds payload envelope against ASTM F963 small-parts cylinder as a documented exclusion, not an assumption |
| Licensing scaffolding retrofitted after design work begins | Medium — compliance | Phase 0 is sequenced first and is a hard gate in the Architecture Decisions |
| Scope creep — full Roomba+FRC hybrid is a large multi-year build | Medium | Phases 2-4 stay at concept/selection granularity here; project-overseer opens each as its own WBS branch only when prior phase checkpoint passes |
| $500 BOM ceiling may be incompatible with LIDAR/depth-camera-class perception | Medium (downgraded from High 2026-09-05) | Compute half resolved: BeagleBone Blue selected at ~$45-50, integrating motor driver/IMU/encoders/charger that would otherwise be separate line items (see `ComputeSelection.md`), freeing budget into contingency. Sensor-suite half still open — ultrasonic + PIR/thermal remains the cost-feasible target over LIDAR/depth camera; Task 17 must design against that range/reliability profile, not assume LIDAR |
| Station fan-separator airflow sizing is unvalidated (may tumble light toys along with trash, or fail to carry tissue-class debris) | Medium | Task 25 flags airflow CFM/static-pressure sizing as an explicit open question requiring empirical testing, not assumed solved by the concept note in `ChargingDumpStation.md` |
| Mains-powered charging/dump station with a fan is a new safety surface in a home with kids/pets, now compounded by exposed charging contacts at the same location | Medium — safety | Task 27 requires household-appliance, fan-guarding, and charging-contact short-circuit safety citations in `REFERENCES.md` before any station prototype is built; preferring an off-the-shelf UL/ETL-listed blower module over a from-scratch fan design is noted as a way to inherit existing certification |
| Merging the charging dock and dump station into one unit couples Task 12 and Task 25 — a design change to one now forces re-checking the other | Low | Both tasks explicitly cross-reference `ChargingDumpStation.md`; the Phase 6 checkpoint requires their geometry be reconciled into one design before either closes |
| Caster placement in `DrivetrainConcept.md` assumes a front-mounted, forward-scooping intake before Task 10 has actually designed one | Low | Explicitly flagged as a working default, not a decision — front-caster placement must be revisited if Task 10 designs a top-loading or rear-mounted intake instead |

## Open Questions — RESOLVED 2026-09-05

- Room/floor inventory: **up to 5 rooms, single-story; hardwood or low-pile carpet; interior thresholds up to 3/8 in (9.5 mm) tall.** See `ConOps.md`.
- Bin interface: **dump-through-chute** — robot docks at a fixed chute and actuates the hopper; it does not enter or carry the bin itself. See `ConOps.md`.
- Charging scheme: **pogo-pin contact charging** at a fixed dock — this requires tighter docking alignment tolerance than inductive would have. See `ConOps.md`.
- BOM ceiling: **$500 max per-unit BOM.** Flagged as a **high risk** in the Risks table below — this is a tight budget against a BeagleBone-class compute platform plus any LIDAR/depth-camera-class sensing, and materially constrains Task 13's sensor-suite selection.
- Autonomy level: **unsupervised by default, with a supervision override** (user can pause / manually drive / single-step, e.g. during commissioning or when personally monitoring a living-obstacle encounter). This does not relax the Task 23 supervised-field-test gate before unsupervised operation ships — the override is a runtime user control, not a substitute for validation.

New open item: session duration / duty cycle target was not part of the original blocker list but is needed to size the battery (Task 15). `ConOps.md` records an engineering-derived placeholder (single-charge full-house coverage, ≤45 min active runtime) explicitly flagged for confirmation before Task 15 is finalized — this is a derived assumption, not a user-supplied number.

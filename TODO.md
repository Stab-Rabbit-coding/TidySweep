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

- [x] 1.1 ConOps.md — mission profile (see [`ConOps.md`](ConOps.md))
- [x] 1.2 Obstacle taxonomy (see [`ObstacleTaxonomy.md`](ObstacleTaxonomy.md)) — living-obstacle standard citation (REF-STD-002) still requires verification
- [x] 1.3 Payload envelope (see [`PayloadEnvelope.md`](PayloadEnvelope.md)) — small-parts exclusion cited to 16 CFR Part 1501 §1501.4 (REF-STD-001)
- [x] 1.4 Mass/power/space budget skeleton (see [`MassPowerBudget.md`](MassPowerBudget.md)) — target allocation only, not a BOM; flags $500 ceiling as tight against BeagleBone AI-64 + LIDAR

## 2. Mechanical Subsystem

- [~] 2.1 Chassis & drivetrain trade study — differential drive (wheeled, not tracked) decided; chassis is a D-shape (18×9 in rectangle + 9 in radius semicircle union), 18 in wide × 18 in total depth, per a full-width front scoop; wheel-count/caster layout left open, coupled to §2.2 (see [`DrivetrainConcept.md`](DrivetrainConcept.md))
- [~] 2.2 Intake/pickup mechanism concept — passive plow + active flipper (single motor, angled end-sections for side capture) decided (see [`IntakeMechanism.md`](IntakeMechanism.md)); pinch-point guarding standard still required before fabrication
- [~] 2.3 Hopper + dump mechanism concept — mesh sized to retain a 1×1 LEGO brick (≤6 mm aperture, corrected from an earlier oversized placeholder), hopper is a removable quick-release module for unjamming (see [`HopperMechanism.md`](HopperMechanism.md)); latch hardware and removal direction (top vs. rear) still open
- [ ] 2.4 Charging dock mechanical interface concept — robot-side half of the combined station in §6; co-designed with §6.1, not a separate location (see [`ChargingDumpStation.md`](ChargingDumpStation.md))

## 3. Electrical / Compute Subsystem

- [~] 3.1 BeagleBone SKU + sensor suite selection against I/O budget — SKU decided (BeagleBone Blue, see [`ComputeSelection.md`](ComputeSelection.md)); occupancy/living-obstacle sensor suite still open
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

## 6. Charging & Dump Station Subsystem (added 2026-09-05, revised same day to merge with the charging dock — one combined station, not two locations; mains-powered, separate budget from the robot's $500 BOM)

- [ ] 6.1 Station fan-separator + docking-bay mechanical concept, co-designed with §2.4 (see [`ChargingDumpStation.md`](ChargingDumpStation.md))
- [ ] 6.2 Station electrical design (fan/blower, shared mains PSU feeding both the fan and the robot's DC charging contacts, dump-activation trigger derived from the docking-contact signal)
- [ ] 6.3 Station safety-standard vetting (household appliance safety, fan guarding, mains cord safety, exposed-charging-contact short-circuit risk)

---

**Current phase:** Phase 0 (Governance & Compliance) and Phase 1
(Requirements & ConOps) both complete as of 2026-09-05. Phase 3's §3.1
compute SKU decision (BeagleBone Blue) was made early, out of WBS order, at
operator request. Phase 6 (Charging & Dump Station Subsystem) was added
2026-09-05 and revised the same day to merge with the charging dock into
one physical station — it is a mains-powered accessory with its own
budget, separate from the robot's $500 BOM. **§2.4 and §6.1 are now a
co-designed pair, not independent tasks** — whichever is picked up first
should read `ChargingDumpStation.md` in full. Phase 2 (Mechanical
Subsystem) is ready to open — start with §2.1 (chassis/drivetrain trade
study), which is unblocked and has no dependencies. §3.1's remaining half
(occupancy/living-obstacle sensor suite) and all of §6 are also ready
whenever picked up.

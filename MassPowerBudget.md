# Mass / Power / Space / Cost Budget (Target Allocation)

Status: Task 8 (`TODO.md` §1.4). Licensed CC-BY-SA 4.0 per
[`LICENSING.md`](LICENSING.md).

This is a **target allocation** table, not a bill of materials — no
component has been selected yet (that's Phase 2/3). Its job is to give
Phase 2/3 selection work a real number to design against instead of
discovering the $500 BOM ceiling (`ConOps.md`) is infeasible only after
parts are already chosen. Every row is a placeholder engineering target,
explicitly not "TBD," and every task that selects real hardware
(`TODO.md` §2.x/§3.x) must reconcile its actual numbers against this table
and update it — this file is expected to change as Phase 2/3 lock in real
parts.

## Mass and power budget

| Subsystem | Mass target, lbm (kg) | Power draw target, W (peak / mission-avg) |
|---|---|---|
| Chassis / structure | 1.9 (0.86) | 0 (passive) |
| Drivetrain (motors, wheels, driver) | 1.2 (0.54) | 15 / 6 |
| Intake mechanism (roller/claw + actuator) | 0.8 (0.36) | 10 / 3 |
| Hopper + dump actuator (incl. quick-release hardware) | 0.7 (0.32) | 5 / 1 |
| Compute (BeagleBone-class SBC) | 0.1 (0.05) | 3 / 3 |
| Sensor suite (obstacle + living-obstacle + IMU + encoders) | 0.3 (0.14) | 4 / 4 |
| Battery pack | 1.0 (0.45) | — (source, not load) |
| Charging contacts (robot-side, pogo-pin) | 0.1 (0.05) | 0 mission / ~40 while docked-charging (not a mission-power load) |
| Wiring, connectors, fasteners, misc. | 0.2 (0.09) | 1 / 1 |
| Contingency margin (~5% mass, sized power headroom) | 0.2 (0.09) | 2 / 2 |
| **Total** | **6.5 lbm (2.95 kg)** | **~40 W peak / ~20 W mission-average** |

## Space envelope target

**Revised 2026-09-05 (third revision, same day): D-shape as a rectangle +
semicircle union**, correcting the pure-semicircle interpretation that
preceded it. The chassis is an 18 in × 9 in (457 mm × 229 mm) rectangle at
the front, unioned with a 9 in (229 mm) radius semicircle at the rear
sharing the rectangle's 18 in rear edge as its diameter — the same "D"
family as a stock Roomba-style body (flat front, straight sidewalls, then
a curved rear), not a true half-disc. See `DrivetrainConcept.md` for the
full geometry discussion and caster-placement consequences.

- Flat front (scoop bay) width: 18 in (457 mm) — unchanged
- Straight sidewall depth: 9 in (229 mm) — new in this revision
- Curved rear radius: 9 in (229 mm) — unchanged from the prior revision
- **Front-to-back depth: 18 in (457 mm) total** (9 in rectangle + 9 in
  semicircle radius) — restores the depth the very first full-circle
  revision had, while keeping the full-width flat front the pure-semicircle
  revision also had
- Height: 7 in (178 mm) — unchanged, no new input on height

**Doorway-clearance check:** unchanged conclusion — 18 in (457 mm) width
still clears a typical US residential interior doorway (nominal 28-32 in
clear opening) with comfortable margin.

**Chassis structure mass/cost impact:** the rectangle+semicircle union
(~289 sq in: 162 sq in rectangle + ~127 sq in semicircle) is the largest
plan-view area of any revision so far — larger than the full 18 in circle
(~254.5 sq in), the pure semicircle (~127.2 sq in), and the original
14 in × 12 in rectangle (~168 sq in). Chassis structure mass/cost were
increased from the pure-semicircle revision's 1.6 lbm / $55 to **1.9 lbm
(0.86 kg) / $62**, a modest increase rather than a full area-proportional
one, since the added rectangular section is simpler flat-panel
construction than the front-edge reinforcement the pure-semicircle version
needed.

**Packaging risk downgraded, not closed:** the pure-semicircle revision's
9 in depth squeeze (flagged as a Medium risk in `tasks/plan.md`) is
resolved by this revision's 18 in total depth — comparable to the very
first full-circle revision, which had no such risk flagged. Task 10/11
detailed layout still needs to do the real component placement, as it
would for any chassis shape; this is no longer treated as an elevated risk
specific to this geometry.

## Cost budget (against the $500 BOM ceiling)

Updated 2026-09-05 after Task 13 selected BeagleBone Blue as the compute
platform (see `ComputeSelection.md`). Blue integrates the motor H-bridge
driver, 9-axis IMU, quadrature encoder interface, and LiPo charge
management onto the compute board itself, which frees budget previously
allocated to those as separate parts — that saving is redirected to
contingency margin below rather than assumed away.

| Subsystem | Cost target ($) |
|---|---|
| Chassis / structure (D-shape: 18×9 in rectangle + 9 in radius semicircle, 18 in total depth) | 62 |
| Drivetrain (motors + wheels only — driver is onboard Blue) | 45 |
| Intake mechanism | 45 |
| Hopper + dump actuator (incl. quick-release/removable-module hardware, added 2026-09-05) | 35 |
| Compute (BeagleBone Blue — integrated motor driver, IMU, encoder interface, LiPo charger, WiFi/BT) | 50 |
| Sensor suite (ultrasonic/PIR occupancy + living-obstacle array only — IMU/encoders now on the compute board, **not** LIDAR, see note) | 45 |
| Battery pack (cells only — charge management is onboard Blue) | 35 |
| Charging contacts (robot-side pogo-pin) | 15 |
| Wiring, connectors, fasteners, misc. | 20 |
| Contingency margin | 148 |
| **Total** | **$500** |

**Note on the sensor-suite row — this is the remaining half of the "$500
BOM ceiling" risk flagged in `tasks/plan.md`:** a 2D LIDAR-class sensor
(~$99+) would alone consume roughly 20% of the entire budget even with
compute now settled cheaply. This table still targets an
**ultrasonic-array + PIR/thermal** sensor suite rather than LIDAR/depth
camera as the cost-feasible path — Task 13's remaining open item (sensor
selection) must treat this as the starting assumption and justify any
LIDAR/depth-camera deviation against the ceiling, not default to it.

## Cross-check against `ConOps.md`

The ~20 W mission-average power draw against a ~45 min (0.75 h) mission
placeholder (`ConOps.md`) implies roughly 15 Wh of energy consumed per
mission. A battery pack at the $35 cost target (typical of a small
Li-ion/LiPo pack in this price class) should comfortably clear that with
margin for the contingency and charging-inefficiency losses — this is a
consistency check, not a battery selection; Task 15 still does the real
sizing once a specific cell/pack is chosen.

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
| Chassis / structure | 1.8 (0.82) | 0 (passive) |
| Drivetrain (motors, wheels, driver) | 1.2 (0.54) | 15 / 6 |
| Intake mechanism (roller/claw + actuator) | 0.8 (0.36) | 10 / 3 |
| Hopper + dump actuator | 0.6 (0.27) | 5 / 1 |
| Compute (BeagleBone-class SBC) | 0.1 (0.05) | 3 / 3 |
| Sensor suite (obstacle + living-obstacle + IMU + encoders) | 0.3 (0.14) | 4 / 4 |
| Battery pack | 1.0 (0.45) | — (source, not load) |
| Charging contacts (robot-side, pogo-pin) | 0.1 (0.05) | 0 mission / ~40 while docked-charging (not a mission-power load) |
| Wiring, connectors, fasteners, misc. | 0.2 (0.09) | 1 / 1 |
| Contingency margin (~5% mass, sized power headroom) | 0.3 (0.14) | 2 / 2 |
| **Total** | **6.4 lbm (2.90 kg)** | **~40 W peak / ~20 W mission-average** |

## Space envelope target

**Revised 2026-09-05: circular chassis, 18 in (457 mm) diameter** — a
Roomba-style circular platform, consistent with the differential-drive
layout in `DrivetrainConcept.md` (2 drive wheels near the chassis center
for pivot-in-place, one caster near the leading edge). This replaces the
earlier rectangular 14 in × 12 in placeholder footprint.

- Diameter: 18 in (457 mm)
- Height: 7 in (178 mm) — unchanged from the earlier placeholder; no new
  input on height, so it is carried forward, not re-derived.

**Doorway-clearance check:** an 18 in (457 mm) diameter body clears a
typical US residential interior doorway (nominal 28-32 in / 711-813 mm,
clear opening a couple inches less after jamb/stop) with comfortable
margin — this is a consistency check against `ConOps.md`'s multi-room
operating environment, not a new requirement.

**Chassis structure mass/cost impact:** an 18 in diameter circle
(~254 sq in) is roughly 50% larger in plan-view area than the prior
14 in × 12 in rectangle (~168 sq in). The chassis structure line above
was increased from 1.5 to 1.8 lbm (0.68 to 0.82 kg) and from $50 to $60
(see cost table below) to reflect the added material, funded out of
contingency margin rather than left unaccounted for.

**Open item for Task 10:** the intake mechanism's frontal opening width is
now bounded by the available chord width near the leading edge of an
18 in diameter circle, not an independent rectangular front panel — Task
10 must design against this circular envelope, not assume a flat-fronted
chassis.

## Cost budget (against the $500 BOM ceiling)

Updated 2026-09-05 after Task 13 selected BeagleBone Blue as the compute
platform (see `ComputeSelection.md`). Blue integrates the motor H-bridge
driver, 9-axis IMU, quadrature encoder interface, and LiPo charge
management onto the compute board itself, which frees budget previously
allocated to those as separate parts — that saving is redirected to
contingency margin below rather than assumed away.

| Subsystem | Cost target ($) |
|---|---|
| Chassis / structure (18 in diameter circular platform) | 60 |
| Drivetrain (motors + wheels only — driver is onboard Blue) | 45 |
| Intake mechanism | 45 |
| Hopper + dump actuator | 30 |
| Compute (BeagleBone Blue — integrated motor driver, IMU, encoder interface, LiPo charger, WiFi/BT) | 50 |
| Sensor suite (ultrasonic/PIR occupancy + living-obstacle array only — IMU/encoders now on the compute board, **not** LIDAR, see note) | 45 |
| Battery pack (cells only — charge management is onboard Blue) | 35 |
| Charging contacts (robot-side pogo-pin) | 15 |
| Wiring, connectors, fasteners, misc. | 20 |
| Contingency margin | 155 |
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

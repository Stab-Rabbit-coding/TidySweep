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
| Chassis / structure | 1.5 (0.68) | 0 (passive) |
| Drivetrain (motors, wheels, driver) | 1.2 (0.54) | 15 / 6 |
| Intake mechanism (roller/claw + actuator) | 0.8 (0.36) | 10 / 3 |
| Hopper + dump actuator | 0.6 (0.27) | 5 / 1 |
| Compute (BeagleBone-class SBC) | 0.1 (0.05) | 3 / 3 |
| Sensor suite (obstacle + living-obstacle + IMU + encoders) | 0.3 (0.14) | 4 / 4 |
| Battery pack | 1.0 (0.45) | — (source, not load) |
| Charging contacts (robot-side, pogo-pin) | 0.1 (0.05) | 0 mission / ~40 while docked-charging (not a mission-power load) |
| Wiring, connectors, fasteners, misc. | 0.2 (0.09) | 1 / 1 |
| Contingency margin (~5% mass, sized power headroom) | 0.3 (0.14) | 2 / 2 |
| **Total** | **6.1 lbm (2.77 kg)** | **~40 W peak / ~20 W mission-average** |

## Space envelope target

Overall chassis footprint target (not additive — this is the outer
envelope, sized to clear the 3/8 in (9.5 mm) threshold from `ConOps.md`
with adequate approach-angle clearance, and to house the intake + hopper):

- Length: 14 in (356 mm)
- Width: 12 in (305 mm)
- Height: 7 in (178 mm)

## Cost budget (against the $500 BOM ceiling)

Updated 2026-09-05 after Task 13 selected BeagleBone Blue as the compute
platform (see `ComputeSelection.md`). Blue integrates the motor H-bridge
driver, 9-axis IMU, quadrature encoder interface, and LiPo charge
management onto the compute board itself, which frees budget previously
allocated to those as separate parts — that saving is redirected to
contingency margin below rather than assumed away.

| Subsystem | Cost target ($) |
|---|---|
| Chassis / structure | 50 |
| Drivetrain (motors + wheels only — driver is onboard Blue) | 45 |
| Intake mechanism | 45 |
| Hopper + dump actuator | 30 |
| Compute (BeagleBone Blue — integrated motor driver, IMU, encoder interface, LiPo charger, WiFi/BT) | 50 |
| Sensor suite (ultrasonic/PIR occupancy + living-obstacle array only — IMU/encoders now on the compute board, **not** LIDAR, see note) | 45 |
| Battery pack (cells only — charge management is onboard Blue) | 35 |
| Charging contacts (robot-side pogo-pin) | 15 |
| Wiring, connectors, fasteners, misc. | 20 |
| Contingency margin | 165 |
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

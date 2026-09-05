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

| Subsystem | Cost target ($) |
|---|---|
| Chassis / structure | 50 |
| Drivetrain (motors, wheels, driver) | 65 |
| Intake mechanism | 40 |
| Hopper + dump actuator | 30 |
| Compute (BeagleBone Black-class — **not** AI-64, see note) | 60 |
| Sensor suite (ultrasonic/PIR array — **not** LIDAR, see note) | 65 |
| Battery pack | 35 |
| Charging contacts (robot-side) | 15 |
| Wiring, connectors, fasteners, misc. | 25 |
| Contingency margin | 115 |
| **Total** | **$500** |

**Note on the compute/sensor cost rows — this is the direct output of the
"$500 BOM ceiling" risk flagged in `tasks/plan.md`:** at current approximate
market pricing, BeagleBone AI-64 (~$130-150) plus a 2D LIDAR-class sensor
(~$99+) would alone consume 45-50% of the entire budget, leaving little
margin for drivetrain, structure, and the intake mechanism. This table
therefore targets **BeagleBone Black-class compute** and an
**ultrasonic-array + PIR/thermal** sensor suite rather than AI-64 +
LIDAR/depth-camera, as the cost-feasible path — Task 13 must treat this as
the starting assumption and justify any deviation against the ceiling, not
default to the higher-end SKU.

## Cross-check against `ConOps.md`

The ~20 W mission-average power draw against a ~45 min (0.75 h) mission
placeholder (`ConOps.md`) implies roughly 15 Wh of energy consumed per
mission. A battery pack at the $35 cost target (typical of a small
Li-ion/LiPo pack in this price class) should comfortably clear that with
margin for the contingency and charging-inefficiency losses — this is a
consistency check, not a battery selection; Task 15 still does the real
sizing once a specific cell/pack is chosen.

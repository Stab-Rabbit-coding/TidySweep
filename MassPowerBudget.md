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
| Chassis / structure | 1.6 (0.73) | 0 (passive) |
| Drivetrain (motors, wheels, driver) | 1.2 (0.54) | 15 / 6 |
| Intake mechanism (roller/claw + actuator) | 0.8 (0.36) | 10 / 3 |
| Hopper + dump actuator | 0.6 (0.27) | 5 / 1 |
| Compute (BeagleBone-class SBC) | 0.1 (0.05) | 3 / 3 |
| Sensor suite (obstacle + living-obstacle + IMU + encoders) | 0.3 (0.14) | 4 / 4 |
| Battery pack | 1.0 (0.45) | — (source, not load) |
| Charging contacts (robot-side, pogo-pin) | 0.1 (0.05) | 0 mission / ~40 while docked-charging (not a mission-power load) |
| Wiring, connectors, fasteners, misc. | 0.2 (0.09) | 1 / 1 |
| Contingency margin (~5% mass, sized power headroom) | 0.3 (0.14) | 2 / 2 |
| **Total** | **6.2 lbm (2.81 kg)** | **~40 W peak / ~20 W mission-average** |

## Space envelope target

**Revised 2026-09-05 (second revision, same day): D-shape (semicircular
half-disc) chassis**, superseding the brief full-circle revision that
preceded it. The operator chose a full 18 in wide front scoop spanning the
entire chassis width. Because the longest possible chord on an 18 in
diameter circle is 18 in itself — achieved only through the center — a
full-width flat front necessarily makes the rear a true semicircle, not a
mostly-round shape with a flattened face. See `DrivetrainConcept.md` for
the full geometry discussion and caster-placement consequences.

- Flat front (scoop bay) width: 18 in (457 mm) — unchanged
- **Front-to-back depth: 9 in (229 mm)** — down from the 18 in a full
  circle would have given, since depth is now just the semicircle's radius
- Height: 7 in (178 mm) — unchanged, no new input on height

**Doorway-clearance check:** unchanged conclusion — 18 in (457 mm) width
still clears a typical US residential interior doorway (nominal 28-32 in
clear opening) with comfortable margin. The reduced 9 in depth doesn't
affect this check; width is the binding dimension for doorways.

**Chassis structure mass/cost impact:** a semicircular half-disc of 9 in
radius (~127 sq in) is roughly half the plan-view area of the full 18 in
circle from the prior revision (~254 sq in), and somewhat *smaller* than
even the original 14 in × 12 in rectangular placeholder (~168 sq in).
Chassis structure mass/cost were reduced from the full-circle revision's
1.8 lbm / $60 to **1.6 lbm (0.73 kg) / $55**, splitting the difference
rather than scaling area-proportionally, because the full-width flat front
edge is a long unsupported span carrying the scoop's reaction loads and
will need real reinforcement, not just the material a smaller area implies.

**New risk, not yet resolved — internal packaging within 9 in of depth:**
the drivetrain, hopper, battery, and compute (see rows above) must all fit
behind the intake mechanism within a 9 in front-to-back depth, after the
scoop mechanism itself claims some of that depth for its roller/ramp
geometry. This is flagged as an open risk in `tasks/plan.md`, not assumed
solved — Task 10/11 detailed layout must validate it fits before this
chassis shape is treated as final.

## Cost budget (against the $500 BOM ceiling)

Updated 2026-09-05 after Task 13 selected BeagleBone Blue as the compute
platform (see `ComputeSelection.md`). Blue integrates the motor H-bridge
driver, 9-axis IMU, quadrature encoder interface, and LiPo charge
management onto the compute board itself, which frees budget previously
allocated to those as separate parts — that saving is redirected to
contingency margin below rather than assumed away.

| Subsystem | Cost target ($) |
|---|---|
| Chassis / structure (D-shape half-disc, 18 in wide × 9 in deep, reinforced front edge) | 55 |
| Drivetrain (motors + wheels only — driver is onboard Blue) | 45 |
| Intake mechanism | 45 |
| Hopper + dump actuator | 30 |
| Compute (BeagleBone Blue — integrated motor driver, IMU, encoder interface, LiPo charger, WiFi/BT) | 50 |
| Sensor suite (ultrasonic/PIR occupancy + living-obstacle array only — IMU/encoders now on the compute board, **not** LIDAR, see note) | 45 |
| Battery pack (cells only — charge management is onboard Blue) | 35 |
| Charging contacts (robot-side pogo-pin) | 15 |
| Wiring, connectors, fasteners, misc. | 20 |
| Contingency margin | 160 |
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

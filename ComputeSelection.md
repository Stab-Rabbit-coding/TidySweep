# Compute Platform Selection

Status: Task 13 (`TODO.md` §3.1). Licensed CC-BY-SA 4.0 per
[`LICENSING.md`](LICENSING.md). Decision below covers the compute *board*
only — the occupancy/living-obstacle sensor suite is a separate line item
in `MassPowerBudget.md` and a separate follow-up under this same task.

## Candidates considered

| Candidate | Verdict | Why |
|---|---|---|
| BeagleBone Black + Robotics Cape | Not selected | Same capability class as BeagleBone Blue below, but as two parts instead of one; standalone Robotics Cape's current retail availability could not be confirmed this session (see Verification notes) |
| **BeagleBone Blue** | **Selected** | Single integrated board; onboard motor drivers, servo outputs, encoder inputs, IMU, LiPo charger, and WiFi/BT cover nearly every Phase 3 electrical line item at once; confirmed in production with active distributor links as of 2026-09-05 |
| PocketBeagle 2 Industrial + PocketPilot cape | **Rejected** | PocketPilot targets the original PocketBeagle (different SoC generation); no stated PocketBeagle 2 support; repository dormant since ~2018; wrong actuator class (flight-controller/ESC-oriented, not ground-drivetrain H-bridge-oriented) |

## Decision: BeagleBone Blue

**Onboard features directly satisfying `MassPowerBudget.md` line items:**

| MassPowerBudget.md line item | Covered by BeagleBone Blue's... |
|---|---|
| Compute | TI AM3358, 1 GHz Cortex-A8, 512MB RAM, 4GB eMMC |
| Drivetrain motor control | 4 bidirectional DC motor H-bridge outputs |
| Intake + hopper-dump actuation | 8 servo/PWM outputs (drivetrain uses the H-bridges, actuators use servo channels — headroom for both plus growth) |
| Sensor suite — IMU | Onboard 9-axis IMU (accel/gyro/mag) + barometer, at zero incremental cost |
| Sensor suite — wheel encoders | 4 quadrature encoder inputs, matched to a differential-drive wheel pair plus spares |
| Battery / charging | Onboard 2-cell LiPo balance charger, 9-18V charger input, charge-state LED — see note below on pogo-pin dock integration |
| (New capability, not previously budgeted) | Onboard 802.11 b/g/n WiFi + Bluetooth 4.1/BLE — usable for the supervision-override remote monitoring/control link in `ConOps.md` at no added BOM cost |

**Not covered — still separate purchases:** occupancy-mapping and
living-obstacle detection sensors (ultrasonic array, PIR/thermal). Blue's
"1.8V analog" and "3.3V GPIO" JST headers are the attachment point for
these; final sensor selection remains open under Task 13.

**Cost:** confirmed available at ~$45 (primelec.com listing, 2026-09-05)
against distributor links (Mouser, Element14, OKDO) published on
beagleboard.org's own product page. This is below the $60 "Compute" line in
`MassPowerBudget.md`'s cost table — see the update to that file.

**Design implication flagged for Task 12/15:** BeagleBone Blue's onboard
charger accepts 9-18V on its charger input and manages 2S LiPo balancing
directly. The pogo-pin dock (`ConOps.md`) may be able to feed this input
directly rather than requiring a separate charge-management board — Task 12
(charging dock mechanical interface) and Task 15 (battery selection) should
evaluate this before designing a separate charge circuit.

## Verification notes (per REFERENCES.md discipline)

- BeagleBone Blue production status: confirmed via `beagleboard.org/blue`
  2026-09-05 — page lists active Mouser/Element14/OKDO distributor links,
  no discontinuation notice. Price confirmed via a single distributor
  (primelec.com, $45); not cross-checked against a second distributor this
  session — treat as an order-of-magnitude confirmation, re-verify exact
  price at time of purchase.
- Robotics Cape (StrawsonDesign) current retail availability: **not
  confirmed this session** (strawsondesign.com returned a certificate
  error; the `librobotcontrol` GitHub README documents Cape and Blue
  side-by-side but does not state whether Cape is still sold). This absence
  of confirmation, not a confirmed discontinuation, is the actual basis for
  preferring Blue — stated as such rather than overclaiming Cape is
  discontinued.
- PocketPilot repository state: confirmed via GitHub fetch 2026-09-05 —
  changelog's most recent entry is January 2018, 7 open issues, 0 merged
  PRs visible, no PocketBeagle 2 mention anywhere in the repository.
  License confirmed as CC-BY-SA-4.0 (not CERN-OHL-P) via the same fetch.
- PocketBeagle 2 Industrial specs (AM6254 quad Cortex-A53, 1GB DDR4, 64GB
  eMMC, -40°C to 85°C, 72-pin header) confirmed via
  `beagleboard.org/pocketbeagle2` and
  `beagleboard.org/boards/pocketbeagle-2-industrial`, both fetched
  2026-09-05. Neither page states cross-generation cape/pin compatibility
  with the original PocketBeagle — this is why the PocketPilot pairing is
  rejected on stated evidence, not assumed compatible by default.

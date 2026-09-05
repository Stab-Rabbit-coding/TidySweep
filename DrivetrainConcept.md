# Chassis & Drivetrain Concept

Status: Task 9 (`TODO.md` §2.1). Licensed CERN-OHL-P 2.0 per
[`LICENSING.md`](LICENSING.md) for the design; this file is documentation
(CC-BY-SA 4.0) describing it.

## Decided: differential drive, wheeled (not tracked)

Confirmed with the operator 2026-09-05, closing the differential-vs-tracked
half of Task 9's trade study.

**Why this is the right call against `ConOps.md`'s requirements, not just a
default:**

- **Threshold climbing is not the constraint tracks would be needed for.**
  Standard wheel-climbing guidance is that wheel radius should meaningfully
  exceed the obstacle height for reliable climbing without a lead-in ramp.
  Against the 3/8 in (9.5 mm) threshold in `ConOps.md`, even a small
  2-3 in (51-76 mm) diameter wheel (1-1.5 in / 25-38 mm radius) clears this
  with margin, and interior transition strips are typically beveled rather
  than a sharp step, easing it further. Tracks solve a terrain problem
  TidySweep doesn't have.
- **Zero-radius turning** matters more here than tracked terrain capability:
  multi-room navigation around furniture (`ObstacleTaxonomy.md` Class 2)
  and reorienting away from a living obstacle (Class 3/4) both benefit from
  in-place pivoting, which differential drive gives for free.
- **Tracks risk marking/scuffing hardwood floors** (`ConOps.md` floor type)
  and have higher rolling resistance than wheels on hard flooring —
  a real downside, not just an omitted feature.
- **Matches the compute platform.** `ComputeSelection.md`'s BeagleBone Blue
  has 4 onboard H-bridge motor outputs. Differential drive needs only 2,
  leaving 2 free — see "Available H-bridge capacity" below, a genuine
  integration opportunity, not filler.
- **Cost:** 2 drive motors instead of 4 (a tank-tread or 4-wheel-drive
  layout) fits inside the existing $45 "Drivetrain (motors + wheels only)"
  line in `MassPowerBudget.md` with more margin, not less.

## Chassis footprint: 18 in (457 mm) diameter, circular

Confirmed with the operator 2026-09-05. Sets the outer envelope this
drivetrain and Task 10's intake mechanism both design within — see
`MassPowerBudget.md`'s Space envelope section for the doorway-clearance
check and the resulting chassis structure mass/cost update. Consistent
with the differential-drive, Roomba-style layout below: drive wheels near
the disc's center support pivot-in-place, and the intake mechanism's
frontal opening is bounded by the chord width available near the leading
edge of the circle, not an independent flat front panel.

## Open: wheel count and caster layout — coupled to Task 10, not decided here

The operator specifically flagged that this shouldn't be settled as a pure
locomotion question, because the active intake mechanism (Task 10, not yet
designed) affects where weight and ground-contact pressure need to be.
This section states the coupling and a working default, not a final
answer — Task 10 detailed design can override the default below.

**Working default: 2 drive wheels near the chassis center (on a common
axle, for pivot-in-place), plus a single front caster — not a rear caster,
and not two casters.**

Reasoning:

- **3-point ground contact, not 4.** Mobile-robotics practice generally
  prefers 3 ground-contact points (2 driven + 1 idle) over 4, because 3
  points always define a plane and guarantee all wheels stay loaded on an
  uneven surface. A 4-point layout (e.g., 2 drive wheels + front and rear
  casters) can leave one contact point unloaded or hanging while crossing
  an edge like the 3/8 in threshold, unless compliant suspension is added —
  which is extra mechanical complexity this ConOps doesn't otherwise need.
  This argues for exactly one caster, front or rear, not two.
- **Front caster is favored over rear (unlike a stock Roomba, which uses a
  rear caster) because of the intake mechanism, not despite it.** An
  active FRC-style roller/claw intake (Task 10) most plausibly sits at the
  front of the chassis, scooping as the robot drives forward, and likely
  needs consistent downward ground-contact pressure to engage irregular
  toys reliably. A front caster sits directly under or near that load,
  supporting the intake's nose weight and helping it ride smoothly over
  the threshold bevel. A rear caster (Roomba's layout) would leave the
  intake's front nose unsupported and cantilevered off the drive-wheel
  axle — more prone to dipping, dragging, or losing consistent floor
  contact right at the moment it's crossing a threshold or engaging a toy.
- **This default assumes a front-mounted, forward-scooping intake.** If
  Task 10 instead designs a top-loading, centrally-mounted, or
  rear-mounted intake, this caster placement should be revisited — it is
  explicitly not locked in.

## Available H-bridge capacity — a Task 10/14 opportunity, not yet claimed

With differential drive using 2 of BeagleBone Blue's 4 onboard motor
H-bridge outputs, **2 channels remain free.** This is worth flagging to
Task 10 (intake mechanism) and Task 14 (motor driver architecture): if the
intake mechanism's roller/claw motor is a brushed DC motor within Blue's
H-bridge current rating, it could run directly off one of the spare
H-bridges rather than requiring a separate motor driver board — a
potential simplification in the same spirit as the charging-station PSU
consolidation in `ChargingDumpStation.md`. Not yet confirmed: Task 10 must
first establish the intake motor's current draw against Blue's H-bridge
rating before this is treated as decided.

## Cross-references

- `ConOps.md` — threshold height, floor type constraints
- `ObstacleTaxonomy.md` — furniture/living-obstacle avoidance benefiting
  from zero-radius turning
- `ComputeSelection.md` — BeagleBone Blue's 4 H-bridge motor outputs
- `MassPowerBudget.md` — Drivetrain cost/mass line, unaffected by this
  decision (already sized for a 2-motor differential-drive assumption)
- `TODO.md` §2.2 (Task 10, intake mechanism) — governs final caster
  placement and the H-bridge-sharing opportunity above

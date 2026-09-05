# Concept of Operations (ConOps)

Status: Task 5 (`TODO.md` §1.1). Answers the mission-profile questions
raised in `tasks/plan.md`. Licensed CC-BY-SA 4.0 per [`LICENSING.md`](LICENSING.md).

## Operating environment

- **Rooms:** up to 5 rooms, single-story residence. (Multi-story operation
  is out of scope for this ConOps — not raised by the operator and not
  assumed; revisit as a new requirement if it comes up.)
- **Floor types:** hardwood or low-pile carpet. Deep-pile rugs, area rugs
  with unsecured edges, and multi-story stair transitions are explicitly
  **out of scope** until stated otherwise.
- **Thresholds:** interior door thresholds / floor-transition strips up to
  3/8 in (9.5 mm) tall. This height is a **traversable** feature, not an
  obstacle to avoid — the drivetrain trade study (`TODO.md` §2.1) must
  confirm ground clearance and approach-angle geometry clear this height
  without high-centering.

## Payload

- Irregular toys/debris up to 2 in (50.8 mm) cube (see `PayloadEnvelope.md`
  for the full envelope and the small-parts exclusion).

## Hopper-to-bin interface

- **Dump-through-chute.** The robot docks at a fixed chute location and
  actuates its onboard hopper to empty through the chute; it does not enter,
  carry, or dock inside the stationary bin itself. This means the mechanical
  interface (`TODO.md` §2.3) only needs to solve alignment-to-chute-mouth and
  a dump actuation, not a full bin-entry maneuver.

## Charging

- **Pogo-pin contact charging** at a fixed dock. Contact charging demands
  tighter docking-approach alignment tolerance than inductive charging would
  have — the docking navigation task (`TODO.md` §4.5) must treat final
  approach as a precision alignment problem, not just "get close."

## Autonomy model

- **Default: unsupervised.** The robot runs its full mission — patrol,
  detect, pick up, return to dump at the chute, return to charge — without a
  human in the loop.
- **Supervision override:** the user can pause, manually drive, or
  single-step the robot at any time (commissioning, debugging, or choosing
  to personally monitor a living-obstacle encounter).
- This override is a **runtime user control**, not a substitute for
  validation. Unsupervised operation does not ship until the supervised
  living-obstacle field test (`TODO.md` §5.3) passes. The override existing
  does not relax that gate.

## Budget ceiling

- **$500 max per-unit BOM.** This is treated as a hard constraint on Phase 3
  component selection, not a target to exceed and revisit later. See the
  "$500 BOM ceiling" risk entry in `tasks/plan.md` — this number is tight
  enough that it may force a lower-cost sensor suite (ultrasonic + PIR/
  thermal rather than LIDAR/depth camera) than would otherwise be preferred,
  and Task 13 must show its work against this ceiling explicitly.

## Session duration / duty cycle — ENGINEERING ASSUMPTION, NOT YET CONFIRMED

This was not one of the five blocking questions answered by the operator.
It is needed to size the battery (`TODO.md` §3.3) and is recorded here as a
placeholder derived from the other constraints, not a supplied requirement:

- Target: complete a full 5-room patrol-and-pickup mission, plus one dump
  cycle and return-to-charge, within a single battery charge.
- Placeholder active-runtime budget: ≤45 min per mission, consistent with
  typical small-robot battery/motor budgets at this BOM ceiling.
- **This must be confirmed or revised before Task 15 (battery selection) is
  finalized** — flagged as an open item, not silently assumed permanent.

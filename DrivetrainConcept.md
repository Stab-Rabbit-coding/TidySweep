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

## Chassis footprint: D-shape as a rectangle + semicircle union, 18 in (457 mm) wide

**Revised 2026-09-05 (second revision, same day) — corrects the prior pure-
semicircle interpretation.** The chassis is the union of an 18 in × 9 in
(457 mm × 229 mm) rectangle at the front and a 9 in (229 mm) radius
semicircle at the rear, sharing the rectangle's 18 in rear edge as the
semicircle's diameter. This is the same "D" family of shape as a stock
Roomba-style vacuum's body (flat front face, straight sidewalls for some
depth, then a curved rear), not the true half-disc the prior revision
assumed.

- **Flat front (the scoop bay):** 18 in (457 mm) wide — unchanged.
- **Straight sidewalls:** 9 in (229 mm) deep, immediately behind the front
  edge — this is new relative to the prior revision.
- **Curved rear:** semicircular arc, radius 9 in (229 mm), same as before.
- **Front-to-back depth: 18 in (457 mm) total** (9 in rectangle + 9 in
  semicircle radius) — back to the same total depth the very first
  full-circle revision had, while still keeping the full 18 in flat front
  the pure-semicircle revision also had. This resolves the internal-
  packaging squeeze flagged against the pure-semicircle version: see
  `MassPowerBudget.md` for the updated area/mass and the now-downgraded
  packaging risk in `tasks/plan.md`.
- **Plan-view area: ~289 sq in** (162 sq in rectangle + ~127 sq in
  semicircle) — larger than any prior revision (full circle 254.5 sq in,
  pure semicircle 127.2 sq in, original rectangle 168 sq in).

## Open: wheel count and caster layout — coupled to Task 10, not decided here

The operator specifically flagged that this shouldn't be settled as a pure
locomotion question, because the active intake mechanism (Task 10, not yet
designed) affects where weight and ground-contact pressure need to be.
This section states the coupling and a working default, not a final
answer — Task 10 detailed design can override the default below.

**Working default: 2 drive wheels positioned within the rectangular
midsection (roughly at or near the rectangle/semicircle junction), plus a
single caster tucked just behind the scoop within the rectangular
section's front portion — not a rear caster, and not two casters.**

Reasoning:

- **The full-width scoop removes the front edge itself as a mounting
  location.** With the entire 18 in flat front occupied by the intake
  mechanism, no wheel or caster can sit directly on that edge without
  interrupting the scoop. The caster must instead sit just inboard/aft of
  the scoop.
- **The 9 in rectangular midsection (new in this revision) gives that
  caster, and the drive wheels, straight sidewalls to sit within** rather
  than immediately fighting a curving body wall right behind the front
  edge, as the pure-semicircle revision would have required. This is a
  meaningful packaging improvement, not just a cosmetic change.
- **3-point ground contact, not 4,** for the same reason as before: 3
  points always define a plane and guarantee all wheels stay loaded
  crossing an edge like the 3/8 in threshold; a 4-point layout risks one
  contact point unloading without added suspension compliance this ConOps
  doesn't otherwise need.
- **A single front-center caster (not corner casters) is preferred**
  specifically because it sits centered behind the full-width scoop where
  that mechanism's ground-contact-pressure load actually is.
- **Drive-wheel axle position relative to overall center of mass/area is
  a Task 10/11 detailed-design question**, not resolved here — the added
  rectangular section shifts the shape's centroid forward relative to the
  pure-semicircle revision, which may argue for the axle sitting further
  back (nearer the rectangle/semicircle junction) than it would on a pure
  disc, to keep pivot-in-place behavior balanced. Noted as a consideration,
  not decided.

## Threshold crossing with a flat front edge — new consideration

A full flat 18 in front edge crossing the 3/8 in threshold means the
entire width of the leading edge meets the threshold's bevel
simultaneously (a line contact), unlike a rounded bumper's point contact.
This is a standard design pattern (e.g., a car bumper or snowplow blade
riding a beveled transition) and not inherently a problem, but the
scoop mechanism's own lowest ground-engaging edge — not just a caster or
bumper — is what will meet the threshold first. Task 10 needs to give that
edge its own ramp/chamfer geometry; this is not solved by the drivetrain
concept alone.

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
- `MassPowerBudget.md` — Drivetrain cost/mass line unaffected by the shape
  change (already sized for a 2-motor differential-drive assumption);
  chassis structure line updated for the new ~289 sq in area
- `TODO.md` §2.2 (Task 10, intake mechanism) — governs final caster
  placement and the H-bridge-sharing opportunity above

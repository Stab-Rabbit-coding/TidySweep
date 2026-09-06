# Intake Mechanism Concept

Status: Task 10 (`TODO.md` §2.2). Licensed CERN-OHL-P 2.0 per
[`LICENSING.md`](LICENSING.md) for the design; this file is documentation
(CC-BY-SA 4.0) describing it.

## Decided: two-stage passive plow + active flipper (option #4)

Confirmed with the operator 2026-09-05, selected from the Task 10 trade
study (roller / flipper-bar / belt conveyor / plow+flipper / vacuum-assist
— vacuum-assist rejected outright as conflicting with `HopperMechanism.md`'s
no-vacuuming decision and mismatched to solid 2 in toy masses).

**Stage 1 — passive plow.** A rigid, chamfered scoop spans the full 18 in
flat front edge (`DrivetrainConcept.md`'s scoop bay). No motor — it is
pure geometry, gathering objects as the robot drives forward and guiding
them up a ramp toward Stage 2. Its leading edge chamfer does double duty
as the threshold-crossing ramp `DrivetrainConcept.md` flagged as needed
for the 3/8 in (9.5 mm) threshold — one part solving two problems, not two
separate designs.

**Stage 2 — active flipper.** A rotating shaft spanning the same 18 in
width, fitted with flexible flaps (rubber or foam), sweeps objects the
plow has gathered up and back into the hopper mouth. One motor drives the
full-width shaft.

## Side capture: angled end-sections on the same shaft, not independent side brushes

Confirmed with the operator 2026-09-05. The question was whether dedicated
side flippers are needed given carpet is an in-scope floor type
(`ConOps.md`) where a passive plow's reliance on toys sliding sideways is
less dependable than on hardwood.

**Decision: extend the Stage 2 flipper shaft's outer end sections with
angled (auger-style) paddle geometry, sharing the same motor and shaft as
the central lifting flaps** — not separate, independently-motorized
side brushes. As the shaft rotates, the angled end sections impart an
inward-sweeping component in addition to the lift, similar to how a
snowblower's helical flighting moves material toward a center chute while
a single shaft spins.

**Why not independent side brushes (the Roomba-style default):** true side
brushes rotate about a vertical axis, perpendicular to the flipper shaft's
horizontal axis, so they cannot share its motor — each one is a separate
motor, a separate H-bridge or servo channel, a separate pinch-guard, and a
separate draw against the $45 / 0.8 lbm intake budget in
`MassPowerBudget.md`. The D-shape's full-width flat front already reaches
into corners a round bumper couldn't, which is the main problem side
brushes solve on a stock vacuum — so the marginal benefit of true side
brushes here is smaller than it would be on a round-bumper robot, and
doesn't yet justify the added motor/cost/complexity.

**Fallback, not yet needed:** if Task 22's field testing (which explicitly
includes carpet, per `ConOps.md`) shows the angled end-sections still miss
toys near the corners, independently-motorized vertical-axis side brushes
become the next design iteration. This is flagged as an open empirical
question for after a prototype exists, not assumed resolved by the
concept-level reasoning here.

## Motor / H-bridge budget — resolves the opportunity flagged in `DrivetrainConcept.md`

The whole intake mechanism (plow, passive, plus the flipper shaft with
integrated end-sections) runs off **one motor**. This confirms the
"Available H-bridge capacity" opportunity `DrivetrainConcept.md` flagged
but left unconfirmed: differential drive uses 2 of BeagleBone Blue's 4
onboard H-bridges, and this intake design claims a 3rd, leaving exactly 1
spare for the hopper-dump actuator (Task 11) — no separate motor driver
board needed for the intake, as hoped.

## Caster placement — confirms the working default in `DrivetrainConcept.md`

`DrivetrainConcept.md`'s caster-placement default assumed "a front-mounted,
forward-scooping intake" and flagged it as provisional pending Task 10.
The plow + flipper design confirmed here **is** exactly that: front-
mounted, forward-scooping, needing ground-contact pressure at the plow's
leading edge. The front-caster-tucked-behind-the-scoop default is now
validated, not just assumed — no revision needed to `DrivetrainConcept.md`'s
caster layout.

## Safety — pinch-point guarding still required before fabrication

Unchanged open item from `REFERENCES.md`, now scoped more specifically:
the Stage 2 flipper's nip point (where flaps meet the hopper mouth) and
the plow-to-flipper transition are the specific pinch/entanglement hazard
zones needing a guard (grate or shroud that passes toys but not fingers)
before fabrication. Still **not yet researched or cited** — no standard
selected.

## Open items (detailed design, not concept-level)

- Flap material and spacing (rubber vs. foam, flap count/pitch) — not
  specified here.
- Plow ramp angle and chamfer dimensions — must clear the 3/8 in threshold
  per `DrivetrainConcept.md` and reliably gather a 2 in (50.8 mm) cube per
  `PayloadEnvelope.md`; not derived here.
- Angled end-section geometry (helix angle, length) — needs iteration
  against actual toy behavior, not assumed correct from this concept note.
- Motor torque/speed sizing against the plow's expected resistance load —
  deferred to detailed design.

## Budget check

Fits within the existing $45 cost / 0.8 lbm (0.36 kg) mass targets in
`MassPowerBudget.md`: one motor, a mostly-passive structural plow, and one
flapped shaft is consistent with what that budget assumed — no change to
`MassPowerBudget.md` required by this decision.

## Cross-references

- `DrivetrainConcept.md` — scoop bay width/depth envelope, caster
  placement (now confirmed), threshold-ramp need (now resolved by the
  plow), available H-bridge capacity (now claimed)
- `HopperMechanism.md` — mesh-bottom hopper the flipper feeds into; the
  no-vacuuming decision that ruled out the vacuum-assist option
- `ConOps.md` — carpet as an in-scope floor type, driving the side-capture
  decision
- `PayloadEnvelope.md` — 2 in (50.8 mm) cube sizing target for the plow/
  flipper geometry
- `MassPowerBudget.md` — intake mechanism cost/mass line
- `REFERENCES.md` — open pinch-guarding standard citation
- `TODO.md` §5.2 (Task 22, field test) — where the side-capture fallback
  question gets an empirical answer

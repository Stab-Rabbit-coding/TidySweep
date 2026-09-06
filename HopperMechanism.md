# Hopper Mechanism Concept

Status: Task 11 (`TODO.md` §2.3). Licensed CERN-OHL-P 2.0 per
[`LICENSING.md`](LICENSING.md) — this is a mechanical design file, not
documentation.

## Mesh bottom — passive dirt shedding, not a second collection function

The onboard hopper floor is a mesh / perforated panel rather than a solid
pan. Purpose: the intake mechanism will incidentally scoop loose dirt,
grit, and fine debris along with toys; the mesh lets that incidental
material fall back through to the floor during transit rather than
accumulating in the hopper.

**This is explicitly not a fine-debris vacuuming feature** — confirmed with
the operator 2026-09-05. TidySweep does not collect or carry fine dirt to
the dump bin; it only keeps the toy hopper itself clean of incidental
debris so hopper capacity stays dedicated to toys. `PayloadEnvelope.md`'s
scope (toy pickup, not general vacuuming) is unchanged by this addition.

## Design parameters (targets, pending Task 9/10 mechanical trade studies)

- **Mesh aperture target: ≤6 mm (0.24 in) — REVISED 2026-09-05, corrects
  the prior ≤0.5 in (12.7 mm) placeholder.** The operator set a concrete
  minimum-retained-object spec: the mesh must catch a 1×1 ("1 dot") LEGO
  brick. Per REF-STD-003 in `REFERENCES.md` (LDraw.org's technical
  specification, cross-checked against BrickLink's packaging dimension for
  LEGO part 3005), a 1×1 brick's base footprint is 8 mm × 8 mm nominal
  (real molded parts run very slightly under this for clutch-fit, commonly
  cited near 7.8 mm). **The prior 12.7 mm placeholder would have let a 1×1
  brick fall straight through — it is superseded, not just tightened.** A
  6 mm target gives retention margin below the ~7.8-8 mm brick footprint
  across tumbled orientations and whatever hole geometry (round vs. square
  vs. slotted) Task 11 detailed design selects; exact hole shape and the
  resulting real retention margin are not derived here.
- **This also resolves `PayloadEnvelope.md`'s prior open item** (no stated
  minimum toy size): the 1×1 LEGO brick spec effectively sets the smallest
  in-scope object at ~8 mm (0.31 in) across its narrowest dimension — see
  the update to `PayloadEnvelope.md`.
- **Material:** corrosion-resistant mesh or perforated sheet (e.g.,
  stainless steel hardware cloth or a perforated polymer panel), selected
  in Task 10/11 detailed design — not specified further here at concept
  level.
- **Structural role:** the mesh floor must still support toy weight and
  intake-mechanism loads without sagging into the drivetrain/chassis
  envelope from `MassPowerBudget.md` — a structural check, not just a
  screen, deferred to Task 11 detailed design.

## Removable hopper module — quick unjamming (added 2026-09-05)

The hopper is a **removable module**, not a fixed internal compartment,
specifically so a jammed toy (wedged between the flipper and the hopper
mouth, or caught against the mesh) can be cleared quickly rather than
requiring chassis disassembly.

- **Quick-release mechanism:** tool-less latches or a slide-and-lock rail
  system — exact hardware not selected here, deferred to Task 11 detailed
  design.
- **Removal direction:** because the mesh floor must stay near the ground
  during operation (per the passive dirt-shedding design above), the
  hopper cannot simply drop out the bottom — it must lift out through a
  top or rear access point in the chassis shell. Which of the two is
  better given the D-shape body's internal layout (drivetrain, battery,
  compute all sharing the same 18 in × 18 in envelope, per
  `DrivetrainConcept.md`) is a Task 11 open item, not decided here.
- **Interaction with the mesh:** a removable hopper also makes the mesh
  itself removable for cleaning if it clogs with shed dirt/debris over
  time — a secondary benefit of this requirement, not a separate design
  goal.

## Depth envelope — D-shape chassis (added 2026-09-05, revised same day)

`DrivetrainConcept.md` and `MassPowerBudget.md` define the chassis as a
D-shape: an 18 in × 9 in rectangle at the front (housing the scoop and
some of the drivetrain), unioned with a 9 in radius semicircle at the
rear — 18 in total front-to-back depth. An earlier same-day revision had
this as a pure 9 in-deep semicircle, which was flagged as a tight
packaging squeeze; that risk is downgraded now that total depth is back to
18 in. Task 11 detailed design still needs to do real component placement,
as it would for any chassis shape, but this is no longer an elevated risk
specific to the geometry.

## Interface to the charging & dump station

Unchanged from `ConOps.md`: the hopper dumps its (toy-only, mesh-sifted)
contents through the fixed chute into the station. See
`ChargingDumpStation.md` for what happens on the station side of that
interface.

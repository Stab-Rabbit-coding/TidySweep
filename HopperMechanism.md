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

- **Mesh aperture target:** ≤0.5 in (12.7 mm), small enough to pass loose
  dirt/grit/pet hair, large enough to retain any toy within the
  `PayloadEnvelope.md` size range. **Open item:** `PayloadEnvelope.md` sets
  a maximum toy size (2 in / 50.8 mm cube) but no minimum — a mesh aperture
  this size assumes no in-scope toy is smaller than roughly 0.5-0.75 in
  across its narrowest dimension. This must be confirmed once Task 10
  (intake mechanism) is designed against real toy samples, not assumed
  permanently from this placeholder.
- **Material:** corrosion-resistant mesh or perforated sheet (e.g.,
  stainless steel hardware cloth or a perforated polymer panel), selected
  in Task 10/11 detailed design — not specified further here at concept
  level.
- **Structural role:** the mesh floor must still support toy weight and
  intake-mechanism loads without sagging into the drivetrain/chassis
  envelope from `MassPowerBudget.md` — a structural check, not just a
  screen, deferred to Task 11 detailed design.

## Depth constraint — D-shape chassis (added 2026-09-05)

`DrivetrainConcept.md` and `MassPowerBudget.md` now define the chassis as
a D-shape (semicircular half-disc), 18 in wide × only 9 in front-to-back
deep, with the front scoop mechanism itself claiming some of that 9 in.
The hopper must fit within whatever depth remains behind the intake
mechanism and ahead of/around the drive wheels, battery, and compute —
this is a tighter packaging envelope than the hopper concept was
originally sketched against. Flagged as an open risk in `tasks/plan.md`;
Task 11 detailed design must validate hopper volume/toy capacity is still
adequate within this depth before the mesh-bottom geometry above is
finalized.

## Interface to the charging & dump station

Unchanged from `ConOps.md`: the hopper dumps its (toy-only, mesh-sifted)
contents through the fixed chute into the station. See
`ChargingDumpStation.md` for what happens on the station side of that
interface.

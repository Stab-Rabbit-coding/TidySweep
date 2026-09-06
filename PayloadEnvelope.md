# Payload Envelope

Status: Task 7 (`TODO.md` §1.3). Licensed CC-BY-SA 4.0 per
[`LICENSING.md`](LICENSING.md).

## In-scope payload

| Property | Value |
|----------|-------|
| Max bounding cube | 2 in × 2 in × 2 in (50.8 mm × 50.8 mm × 50.8 mm) |
| Min in-scope object (added 2026-09-05) | ~8 mm (0.31 in) across its narrowest dimension — set by the operator's requirement that the onboard hopper mesh must retain a 1×1 ("1 dot") LEGO brick. See REF-STD-003 in `REFERENCES.md` and `HopperMechanism.md`'s mesh-aperture revision. This is a retention target for objects that do get scooped, not a detection/pickup guarantee — see the small-parts note below for how this relates to the exclusion |
| Shape | Irregular — not assumed to be a rigid cube; the intake mechanism (`TODO.md` §2.2) must handle arbitrary irregular geometry within the bounding cube, not just cube-shaped objects |
| Mass range | To be bounded by the intake-mechanism trade study (`TODO.md` §2.2) — not yet set here; flagged as an open item for that task rather than guessed |
| Material assumption | Rigid or semi-rigid toy materials (plastic, wood, light metal). Soft/deformable items (plush toys) are not excluded but are not the sizing case — the bounding cube and mechanism must be validated against rigid worst-case geometry first |

## Explicit exclusion: small-parts-sized items

**16 CFR Part 1501** ("Method for Identifying Toys and Other Articles
Intended for Use by Children Under 3 Years of Age Which Present Choking,
Aspiration, or Ingestion Hazards Because of Small Parts"), §1501.4, defines
the federal small-parts test cylinder used to identify choking-hazard-sized
items for children under 3. See `REFERENCES.md` REF-STD-001.

TidySweep's payload envelope **excludes** small-parts-cylinder-sized debris
as a target: this robot is designed to pick up 2 in (50.8 mm)-class toys,
not to perform choking-hazard remediation for items sized to pass the
§1501.4 cylinder. This is a documented scope boundary, not an assumption:

- Items that pass through the §1501.4 test cylinder are **out of scope** for
  guaranteed pickup. The intake mechanism is not required to detect or
  ingest them reliably.
- This exclusion does **not** mean the robot may deliberately avoid such
  items in an unsafe way (e.g., pushing them toward a location a child could
  reach) — that behavior question belongs to the intake/navigation design
  (`TODO.md` §2.2/§4.3) and is noted here as a downstream design
  constraint, not resolved by this document.
- 16 CFR Part 1501 governs products intended for children under 3; it does
  not itself regulate robot behavior. It is cited here only to define the
  size threshold used for TidySweep's own scope boundary, not as a
  compliance claim about the robot itself.

**Note — this does not contradict the min-object mesh-retention target
above.** A 1×1 LEGO brick (~8 mm) is itself small enough to fit inside the
§1501.4 test cylinder, so it falls within this exclusion for *guaranteed
pickup* — the intake is not required to reliably find and scoop every
brick that size. The mesh-retention requirement is a different concern:
*if* a small item that size is incidentally scooped up (e.g., stuck to a
larger toy, or caught along with other objects), the hopper should not
lose it back out through the mesh floor mid-transit. Guaranteed-pickup
exclusion and incidental-retention are independent design goals, not in
tension — this is not offered as a choking-hazard compliance claim either
way.

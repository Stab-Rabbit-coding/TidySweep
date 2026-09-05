# Charging & Dump Station — Combined Concept

Status: Phase 6 (`TODO.md` §6), revised 2026-09-05 — the charging dock and
the fan-separator bin are **one physical station, not two locations**,
confirmed with the operator. This supersedes the earlier framing where the
bin (`DumpBinSeparator.md`, since renamed to this file) was treated as
separate from the charging dock (`TODO.md` §2.4 / Task 12). Licensed
CERN-OHL-P 2.0 per [`LICENSING.md`](LICENSING.md) for the design; this file
is documentation (CC-BY-SA 4.0) describing it.

## Why combining them matters

The robot only ever needs to learn and execute **one** docking maneuver.
Previously this concept treated "dock to charge" and "dock to dump" as two
separate alignment problems; they are now the same approach, docked at the
same station, satisfying both functions in one visit. This simplifies
Task 12 (charging-dock mechanical interface, robot-side) and Task 25
(bin fan-separator mechanical concept, station-side) into co-designed
halves of one interface rather than two independent geometries.

It also removes duplicate hardware:

- **One mains power supply**, not two. The same PSU that converts mains
  power to the 9-18V DC the robot's onboard BeagleBone Blue charger input
  expects (per `ComputeSelection.md`) also powers the fan/blower motor.
- **The docking event itself is the dump-activation trigger.** Once the
  robot's pogo-pin contacts mate with the station, that same contact/
  presence signal (or a data line alongside it) can signal "robot is
  docked and dumping" to the station's fan controller — no separate IR
  break-beam or wireless link needed, which was an open question in the
  prior concept.

## Station layout (concept)

1. Robot approaches and docks; pogo-pin contacts mate for charging (see
   `ConOps.md` "Charging & Dump Station").
2. Docking triggers (a) charge current to begin flowing into the robot's
   onboard charger, and (b) the hopper-dump sequence and fan activation,
   either concurrently or in a short fixed sequence (dump first, then hold
   position to charge — sequencing not yet decided, see open questions).
3. Toys and any incidental light trash fall from the hopper through the
   station's chute.
4. The fan/blower creates an airflow path across the fall zone: toys drop
   into the main toy-collection compartment; light trash (tissue, lint,
   paper) is carried by the airflow into a separate light-trash
   compartment, ideally through a screen/filter stage.
5. Fan runs only for a short period after docking (duration TBD by Task 26
   testing), not continuously.

## Open design questions (Task 25/26)

- **Charge-vs-dump sequencing:** does the robot dump immediately on
  docking, then remain docked to charge, or does it charge first and dump
  only when commanded? Simplest default: dump immediately on docking
  (empty the hopper before a long charge sit), but not decided.
- **Airflow sizing:** unchanged from the prior concept — exact fan CFM/
  static-pressure to carry tissue-class trash without disturbing toys
  needs empirical testing, not assumed from the placeholder budget below.
- **Filter/exhaust:** the fan's exhaust path still needs a screen/filter
  stage so light trash doesn't blow back into the room.
- **Trigger signal design:** whether "docked" is sensed purely by charge
  current flowing (simplest, no extra part) or a dedicated data line/pin
  on the docking connector — affects `ComputeSelection.md`'s pogo-pin
  contact design and is a Task 12/26 joint decision.

## Station budget (target, separate from the robot's $500 BOM)

Revised from the prior stand-alone-bin concept to remove the duplicate PSU
and simplify the trigger, per the consolidation above.

| Item | Mass target, lbm (kg) | Power draw (mains, while active) | Cost target ($) |
| --- | --- | --- | --- |
| Station structure (docking bay + chute + two-compartment separation body) | 4.0 (1.8) | — | 70 |
| Charging contacts (station-side pogo-pins) + wiring | 0.2 (0.09) | — | 15 |
| Shared mains PSU (feeds robot charging contacts at 9-18V DC **and** the fan motor) | 0.6 (0.27) | Charging: ~15-20 W typical; fan: 30-60 W while active | 45 |
| Fan/blower motor | 0.5 (0.23) | (see PSU row) | 40 |
| Dump-activation trigger (docking-contact-derived signal, not a separate sensor) | 0.05 (0.02) | <1 W | 10 |
| Filter/screen stage | 0.2 (0.09) | — | 15 |
| Misc fasteners/wiring | 0.2 (0.09) | — | 10 |
| Contingency margin | 0.25 (0.11) | — | 15 |
| **Total** | **6.0 lbm (2.7 kg)** | **~15-20 W continuous (charging) + 30-60 W active-only (fan, seconds per dock event)** | **$220** |

Total held at the same $220 placeholder as the prior stand-alone concept —
the savings from removing a duplicate PSU and a separate trigger sensor are
reallocated to the dedicated charging-contacts line and a smaller
contingency pool, not assumed as pure savings. Still a placeholder pending
Task 25/26 detailed design.

## Footprint target

Unchanged in principle from the prior concept, now understood as one
combined station: 16 in × 12 in × 20 in H (406 mm × 305 mm × 508 mm),
housing the docking bay, charging contacts, chute, and both collection
compartments. Docking-bay geometry must match the robot's approach/
alignment design from Task 12 — not yet fixed.

## Safety — standards vetting required before fabrication

Unchanged core items from the prior concept, plus one addition from
combining charging and dumping at the same station:

- Household electrical appliance safety (candidate: UL 507 for electric
  fans, or the IEC 60335 series) — **not yet researched or cited**.
- Fan-blade/intake finger-safety guarding, given proximity to children —
  extends the same open machine-guarding item flagged for the robot's
  intake mechanism in `REFERENCES.md`.
- Mains cord/plug safety if a custom enclosure is built rather than an
  off-the-shelf certified blower module.
- **New:** exposed charging contacts at a floor-level station are a
  short-circuit/fire risk if bridged by a dropped metal object (a toy with
  metal parts, a dropped key), even though 9-18V DC is not itself a shock
  hazard at that level. Contact placement/recessing and fusing/current-
  limiting on the charging supply should be considered in Task 12/26 —
  not yet researched or cited as a specific standard.

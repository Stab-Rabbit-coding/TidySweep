# Stationary Dump Bin — Fan Separator Concept

Status: new subsystem, Phase 6 (`TODO.md` §6), added 2026-09-05 at operator
request. Licensed CERN-OHL-P 2.0 per [`LICENSING.md`](LICENSING.md) for the
mechanical/electrical design; this file itself is documentation (CC-BY-SA
4.0) describing that design.

## Why this exists

Per `HopperMechanism.md`, the robot's hopper carries toys only — but toys
picked up alongside light incidental trash (tissue, paper scraps, lint)
that's too large to fall through the hopper mesh will still ride along to
the bin. The bin needs to separate that light trash from the toys so a
household doesn't have to hand-sort the bin after every dump.

## Scope and budget — separate from the robot

**This is a stationary, mains-powered appliance, not part of the mobile
robot.** Confirmed with the operator 2026-09-05: it has its own budget,
separate from the robot's $500 BOM ceiling in `MassPowerBudget.md`. See the
"Bin budget" table below.

## Concept: airflow-based density separation

1. Robot docks at the chute (`ConOps.md`) and actuates its hopper dump.
2. Toys and light trash fall together into the bin's intake chute.
3. A fan/blower creates an airflow path across the fall zone. Toys (denser,
   heavier per the `PayloadEnvelope.md` size/material assumptions) fall
   through the airflow largely unaffected and drop into the main toy
   collection compartment below.
4. Light trash (tissue, paper, lint — low mass-to-area ratio) gets carried
   by the airflow into a separate light-trash compartment, ideally through
   a screen/filter stage so the fan doesn't just blow it back out into the
   room.
5. Fan runs only during/immediately after a dump event, not continuously —
   activation trigger is an open design question (see below).

This is the same physical principle as a household leaf blower/vac
separating leaves from debris, or a simple air classifier — not a novel
mechanism, but sizing the airflow correctly (enough to carry tissue,
not enough to tumble a light toy) is real design work for Task 25, not
assumed solved by this concept note.

## Open design questions (Task 25/26)

- **Fan activation trigger:** options include (a) a mechanical/IR
  break-beam sensor at the chute triggering the fan for a fixed duration,
  or (b) a wireless trigger sent from the robot's onboard BeagleBone Blue
  (which has WiFi/BT per `ComputeSelection.md`) to a simple receiver/MCU in
  the bin when it begins its dump. Option (b) is more elegant but adds a
  wireless link and a second small compute/receiver to the bin's BOM;
  option (a) is simpler and fully bin-local. Not decided — flagged for
  Task 26.
- **Airflow sizing:** exact fan CFM/static-pressure needed to reliably
  carry tissue-class light trash without disturbing toys is not derived
  here — this requires either a literature-based air-classifier sizing
  approach or empirical testing once a prototype exists. Not to be assumed
  from the placeholder budget below.
- **Filter/exhaust:** the fan's exhaust path needs a screen or filter stage
  so light trash doesn't get blown back into the room — mechanical detail
  deferred to Task 25.

## Bin budget (target, separate from the robot's $500 BOM)

| Item | Mass target, lbm (kg) | Power draw (mains, while active) | Cost target ($) |
|---|---|---|---|
| Bin structure (chute + two-compartment body) | 4.0 (1.8) | — | 70 |
| Fan/blower motor | 0.5 (0.23) | 30-60 W | 40 |
| Activation trigger (mechanical/IR, Task 26 to decide vs. wireless) | 0.1 (0.05) | <1 W | 15 |
| Mains power supply, cord, enclosure/strain relief | 0.5 (0.23) | — (supply only) | 40 |
| Filter/screen stage | 0.2 (0.09) | — | 15 |
| Misc fasteners/wiring | 0.2 (0.09) | — | 10 |
| Contingency margin | 0.5 (0.23) | — | 30 |
| **Total** | **6.0 lbm (2.7 kg)** | **~30-60 W, active only (duty cycle: seconds per dump, not continuous)** | **$220** |

This $220 target is a placeholder pending Task 25/26 detailed design —
flagged for confirmation, not a final BOM, consistent with how the robot's
own `MassPowerBudget.md` is treated.

## Footprint target

- Intake chute opening height: must align with the robot's dump-chute
  discharge height from the mechanical design in `HopperMechanism.md`/Task
  12 (charging-dock-adjacent chute geometry) — not yet fixed, since the
  robot's own chute height isn't finalized until Task 9/11 close.
- Overall bin footprint target: 16 in × 12 in × 20 in H (406 mm × 305 mm ×
  508 mm), sized to hold a reasonable multi-day toy volume in the main
  compartment plus a smaller light-trash compartment — a placeholder, not
  derived from an actual toy-volume calculation yet.

## Safety — standards vetting required before fabrication

A mains-powered appliance with a fan, operating on the floor of a home
with children and pets, needs safety vetting before it is built, per the
project's Standards Vetting Policy. **Not yet researched or cited** — flag
for Task 27 (new):

- Household electrical appliance safety (candidate: UL 507 for electric
  fans, or the IEC 60335 series for household appliance safety) —
  requires verification before REFERENCES.md gets an entry.
- Fan-blade/intake finger-safety guarding for a device children will be
  near — extends the same open "machine-guarding standard" item already
  flagged for the robot's intake mechanism in `REFERENCES.md`.
- Mains cord/plug safety (strain relief, cord rating) if a custom
  enclosure is built rather than using an off-the-shelf certified blower
  unit — worth considering an off-the-shelf UL/ETL-listed blower module
  specifically to inherit its existing safety certification rather than
  re-deriving fan safety from scratch, but not decided here.

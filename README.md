# TidySweep

A multi-room autonomous toy-cleaning robot — a cross between a FIRST
Robotics-style active debris-collection mechanism and a Roomba-style
autonomous floor-coverage robot.

**Status: Phase 0 (repository & governance scaffolding) complete. Phase 1
(requirements/ConOps) is blocked on operator input.** No mechanical,
electrical, or software design work has started yet. See
[`TODO.md`](TODO.md) for the full Work Breakdown Structure and
[`tasks/plan.md`](tasks/plan.md) for the current-phase plan.

## What it will do

- Navigate multiple rooms, avoiding static obstacles (low thresholds,
  tables, chairs, furniture) and living obstacles (cats, dogs, humans)
  without contact.
- Pick up irregular-shaped objects up to 2 in (50.8 mm) cubes.
- Empty its onboard hopper into a stationary external bin.
- Monitor its own battery level and autonomously return to a charging dock.

## Platform

Compute and motor control run on the [BeagleBone](https://beagleboard.org/)
ecosystem (candidate SKUs: BeagleBone Black, BeagleBone AI-64,
PocketBeagle — final selection pending, see `TODO.md` §3.1).

## License

- **Documentation** (this README, all `.md` files, diagrams): [CC-BY-SA 4.0](LICENSE-DOCS)
- **Hardware** (CAD, schematics, PCB layouts): [CERN-OHL-P 2.0](LICENSE-HARDWARE)
- **Firmware/software**: [CC0 1.0 Universal](LICENSE-SOFTWARE) — not CC-BY-SA;
  Creative Commons' own FAQ recommends against CC licenses for software,
  and CC0 is the one exception they carve out as acceptable.

See [`LICENSING.md`](LICENSING.md) for the full file-type mapping.

## Governance

All AI agents and contributors: read [`AGENTS.md`](AGENTS.md) first. It is
the authoritative, model-agnostic instruction set for this repository.

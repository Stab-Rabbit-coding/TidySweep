---
name: TidySweep
last_updated: 2026-09-05
---

# TidySweep Strategy

## Target problem

Households with kids and/or pets accumulate toy clutter too large or
irregular for a standard robot vacuum to ingest, so floors stay cluttered
between manual pickups. Picking toys up by hand is a chore nobody wants, and
doing it fully unattended — without damaging toys, floors, pets, or people —
is what no existing single-purpose robot (ingest-only vacuum, or a manual
debris-bot) solves.

## Our approach

We combine active mechanical pickup (a FIRST Robotics-style roller/claw and
hopper, sized for real irregular toys) with safety-first, non-contact
handling of living obstacles as a first-class hazard class — rather than
optimizing purely for suction-based coverage speed the way a standard robot
vacuum does — so the robot can be trusted to run unattended in a home with
kids and pets.

## Who it's for

**Primary:** Parents-with-pets in a multi-room household — they're hiring
TidySweep to clear toy clutter and pet-scattered debris from floors between
active use, unattended, without the robot contacting or startling children
or animals.

## Key metrics

- **Pickup success rate** - % of detected eligible objects (≤2 in / 50.8 mm
  cube) successfully ingested per run; measured from onboard event logs.
- **Living-obstacle non-contact rate** - % of cat/dog/human encounters
  resolved with zero physical contact; measured from onboard logs and
  supervised field-test observation. Safety-critical — target near-100%,
  and any regression here is a hard stop on further autonomy expansion.
- **Unattended mission completion rate** - % of full missions (pickup →
  hopper → dock → dump → return-to-charge) completed without manual
  intervention; measured from mission-state-machine telemetry.
- **Hopper-to-bin empty success rate** - % of dock-and-dump attempts that
  fully empty the hopper into the stationary bin without jam or spill;
  measured from onboard logs plus physical bin-fill spot checks.
- **Battery-to-dock success rate** - % of low-battery events resulting in
  successful autonomous return to the charger before shutdown; measured
  from onboard telemetry.

## Tracks

### Active Intake & Handling

The pickup mechanism, hopper, and bin-dump actuation — everything involved
in physically grasping an irregular toy and getting it out of the house.

_Why it serves the approach:_ This is the half of the approach that a
standard robot vacuum can't do at all; it's the mechanical bet.

### Safety-Critical Perception

Detection and response logic for living obstacles (cats, dogs, humans),
kept architecturally distinct from static-obstacle mapping.

_Why it serves the approach:_ This is the other half of the approach — the
non-contact guarantee is what makes unattended operation trustworthy.

### Autonomy & Navigation

Multi-room SLAM, coverage planning, static-obstacle avoidance, and
docking/charging navigation.

_Why it serves the approach:_ Makes the robot cover a real home
unattended, which both other tracks depend on to matter in practice.

### Compute & Platform

BeagleBone-ecosystem integration, sensor fusion, power distribution, and
the software/firmware runtime tying the other tracks together.

_Why it serves the approach:_ The fixed platform constraint that every
other track's implementation has to fit within.

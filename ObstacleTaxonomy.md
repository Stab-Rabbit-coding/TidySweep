# Obstacle Taxonomy

Status: Task 6 (`TODO.md` §1.2). Enumerates obstacle classes and the
required detection range / mandated response per class. Licensed CC-BY-SA
4.0 per [`LICENSING.md`](LICENSING.md).

Per [`AGENTS.md`](AGENTS.md), living obstacles are a **distinct hazard
class** from static furniture and must never be handled as a special case of
generic occupancy-mapping avoidance.

## Class 1 — Traversable static features

**Members:** interior thresholds / floor-transition strips ≤3/8 in (9.5 mm)
tall (per `ConOps.md`).

**Detection:** not treated as an obstacle to avoid. Verified at design time
via drivetrain ground-clearance and approach-angle geometry (`TODO.md`
§2.1); at runtime, wheel-encoder/IMU deviation from expected traversal
behavior (e.g., unexpected stall) is the fallback signal that a threshold
was mis-classified as traversable.

**Response:** proceed over the feature; do not reroute.

## Class 2 — Static avoid-obstacles

**Members:** tables, chairs, low furniture legs, walls, and any other
non-living fixed object above the Class 1 threshold height or otherwise not
traversable.

**Detection:** occupancy-mapping sensor (LIDAR or depth camera, pending the
Task 13 sensor-suite selection against the $500 BOM ceiling — see
`tasks/plan.md` risk entry). Minimum detection range: to be set by Task 13
once the sensor is chosen; not assumed here.

**Response:** reroute around the obstacle; update the occupancy map for
subsequent passes.

## Class 3 — Living obstacles: cats and dogs

**Members:** cats, dogs, and other small-to-medium pets that may be present
and moving unpredictably.

**Detection:** a sensing mode distinct from Class 2's occupancy mapping —
motion + thermal/PIR fusion (candidate sensors pending Task 13), because a
static-occupancy sensor alone cannot distinguish "furniture that will not
move" from "animal that may move into the path." Minimum stop-initiation
distance: **3 ft (0.9 m)**, set here as a conservative internally-derived
design target — not sourced from a specific verified standard.

**Response:** full stop, then reroute only once the animal has cleared the
path or a timeout elapses; never proceed on an assumption that the animal
will move out of the way. Zero physical contact is the target — see
"Living-obstacle non-contact rate" in `STRATEGY.md`.

## Class 4 — Living obstacles: humans

**Members:** adults and children present in the operating environment.

**Detection:** same sensing stack as Class 3. Minimum stop-initiation
distance: **4 ft (1.2 m)** — larger than the Class 3 distance given higher
consequence of contact and the possibility of a human moving toward the
robot rather than away from it. Also internally-derived, not yet
standard-sourced (see Standards note below).

**Response:** same as Class 3 — full stop, reroute only once clear, zero
physical contact.

## Standards note (REF-STD-002, requires verification)

ISO 13482:2014, "Robots and robotic devices — Safety requirements for
personal care robots," is the standard most directly applicable to a
mobile-servant-class domestic robot operating around humans, and is the
natural candidate to formally back the Class 3/4 stop distances above. It
has **not yet been independently verified this session** — the ISO catalog
page (`https://www.iso.org/standard/53820.html`) returned an anti-bot
challenge rather than content during the verification attempt, so its
scope/section applicability is recorded in `REFERENCES.md` as "requires
verification," not asserted as authoritative here. The stop-distance values
above are therefore engineering judgment pending that verification, not a
standards-derived number — do not cite them as ISO-13482-compliant until
REF-STD-002 is confirmed and a specific section is identified.

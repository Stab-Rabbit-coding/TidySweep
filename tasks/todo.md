# TidySweep Task List (handoff to project-overseer)

Full context and rationale: see `tasks/plan.md`. Phase 0/1 tasks below are
scoped for direct execution. Phase 2+ tasks are concept-level entries that
project-overseer should expand into their own WBS sub-branches once the prior
phase's checkpoint passes.

## Phase 0: Repository & Governance Scaffolding

### Task 1: Root governance files
**Description:** Create CLAUDE.md (pointing to AGENTS.md as authoritative, per this user's existing Serenity-UAV convention), AGENTS.md (model-agnostic project instructions), and README.md (project summary, licensing badges, build status placeholder that is honest about pre-alpha state).
**Acceptance criteria:**
- [ ] CLAUDE.md exists and defers to AGENTS.md
- [ ] AGENTS.md states: platform constraint (BeagleBone), licensing (CC-BY-SA-4.0 docs / CERN-OHL-P-2.0 hardware), unit convention (imperial-primary, metric parens), and this-is-a-real-build philosophy
- [ ] README.md states project one-liner, license badges, and current phase (Phase 0 scaffolding)
**Verification:**
- [ ] Files render correctly as Markdown (no broken links)
- [ ] Manual check: AGENTS.md content matches user's global CLAUDE.md governance requirements
**Dependencies:** None
**Files:** `CLAUDE.md`, `AGENTS.md`, `README.md`
**Estimated scope:** Small

### Task 2: Licensing infrastructure
**Description:** Add `LICENSE-DOCS` (full CC-BY-SA 4.0 legal text) and `LICENSE-HARDWARE` (full CERN-OHL-P 2.0 legal text), plus a short `LICENSING.md` explaining which license governs which file types (docs/markdown/images → CC-BY-SA-4.0; CAD/schematics/PCB/firmware-adjacent hardware description → CERN-OHL-P-2.0) and where to find each license's canonical source URL.
**Acceptance criteria:**
- [ ] LICENSE-DOCS text matches the canonical CC-BY-SA 4.0 legal code verbatim
- [ ] LICENSE-HARDWARE text matches the canonical CERN-OHL-P 2.0 legal code verbatim
- [ ] LICENSING.md cites both canonical source URLs (validated, not guessed) and maps file globs to licenses
**Verification:**
- [ ] Manual check: license texts are fetched from their authoritative source (creativecommons.org, ohwr.org/cern_ohl) rather than paraphrased
**Dependencies:** None (parallel with Task 1)
**Files:** `LICENSE-DOCS`, `LICENSE-HARDWARE`, `LICENSING.md`
**Estimated scope:** Small

### Task 3: REFERENCES.md skeleton + BeagleBone SKU selection
**Description:** Create REFERENCES.md per the user's global Standards Vetting Policy format (REF-ID, full title, validated URL, section applied, citing locations). First entries: the BeagleBone SKU(s) datasheet(s) under consideration (BeagleBone AI-64, BeagleBone Black, PocketBeagle) with their I/O/compute specs, to support the Task 13 selection later.
**Acceptance criteria:**
- [ ] REFERENCES.md exists with the required column structure and a "Removed / Superseded Citations" section (initially empty)
- [ ] At least one REF-ID entry per candidate BeagleBone SKU with a validated datasheet URL
**Verification:**
- [ ] Manual check: every URL in REFERENCES.md resolves and matches the cited publisher
**Dependencies:** None
**Files:** `REFERENCES.md`
**Estimated scope:** Small

### Task 4: WBS/index scaffolding
**Description:** Create TODO.md as a formal Work Breakdown Structure (top-level phases matching tasks/plan.md phases, each with numbered WBS items), PROJECT_INDEX.md listing the initial file tree, and Claude-MEMORY.md as the auditable mirror of this session's auto-memory writes for this project.
**Acceptance criteria:**
- [ ] TODO.md uses formal WBS numbering (e.g. 1.0 Governance, 1.1 Root governance files, ...) and reflects Phase 0-5 from tasks/plan.md
- [ ] PROJECT_INDEX.md lists every file created so far
- [ ] Claude-MEMORY.md exists (may start empty with a header, populated as memories are written)
**Verification:**
- [ ] Manual check: TODO.md WBS items map 1:1 to tasks/plan.md task list (no orphaned items either direction)
**Dependencies:** Tasks 1-3 (needs final file list for PROJECT_INDEX.md)
**Files:** `TODO.md`, `PROJECT_INDEX.md`, `Claude-MEMORY.md`
**Estimated scope:** Medium

## Checkpoint: Phase 0
- [ ] All Phase 0 files committed in one initial commit
- [ ] User has reviewed licensing files and governance docs before any design work begins

## Phase 1: Requirements & ConOps

### Task 5: ConOps.md
**Description:** Document mission profile: target rooms/floor types, threshold height range robot must climb, session duration, expected duty cycle, and operating environment assumptions (pets/children present).
**Acceptance criteria:**
- [ ] ConOps.md states concrete numbers (not TBD) for threshold height, floor types, and session duration — pending Open Questions being answered by user first
**Dependencies:** Phase 0 checkpoint
**Estimated scope:** Small
**Note:** blocked on Open Question "room/floor inventory" in tasks/plan.md — flag to user before drafting.

### Task 6: Obstacle taxonomy
**Description:** Enumerate obstacle classes (static: thresholds, table/chair legs, low furniture; dynamic/living: cats, dogs, humans) with required detection range and mandated robot response per class.
**Acceptance criteria:**
- [ ] Each obstacle class has a minimum detection range and a specified robot behavior (stop / reroute / slow-approach)
- [ ] Living-obstacle class explicitly distinguished from static-furniture class with a stricter (non-contact) response rule
**Dependencies:** Task 5
**Estimated scope:** Small

### Task 7: Payload envelope
**Description:** Define max toy size (2 in / 50.8 mm cube, per user spec), irregular-shape handling assumptions, and mass range; document exclusion of ASTM F963 small-parts-cylinder-sized items as out of scope (choking-hazard-sized debris is not this robot's job).
**Acceptance criteria:**
- [ ] Payload envelope table with real dimensions in inches (mm) per global unit convention
- [ ] Explicit small-parts exclusion documented with ASTM F963 citation added to REFERENCES.md
**Dependencies:** Task 3 (REFERENCES.md must exist)
**Estimated scope:** Small

### Task 8: Mass/power/space budget skeleton
**Description:** Create a budget table (chassis mass, battery mass, payload mass, total mass target in lbm/kg; power draw per subsystem in W; footprint envelope in in/mm) with real placeholder-free target numbers per the user's global weight-and-balance requirement.
**Acceptance criteria:**
- [ ] Table has a row per subsystem (drivetrain, intake, hopper, compute, sensors, battery) with non-TBD numeric targets
- [ ] Total mass and power rows sum correctly from subsystem rows
**Dependencies:** Tasks 5-7
**Estimated scope:** Medium

## Checkpoint: Phase 1
- [ ] User reviews and signs off on ConOps.md, obstacle taxonomy, payload envelope, and mass/power budget before Phase 2 mechanical design opens

## Phase 2: Mechanical Subsystem (concept-level — expand in project-overseer)
- [ ] Task 9: Chassis & drivetrain trade study (differential drive vs. tracked, threshold-climbing requirement)
- [ ] Task 10: Intake/pickup mechanism concept, with pinch-point guarding standard cited in REFERENCES.md
- [ ] Task 11: Hopper + bin-emptying mechanism concept
- [ ] Task 12: Charging dock mechanical interface concept

## Phase 3: Electrical / Compute Subsystem (concept-level — expand in project-overseer)
- [ ] Task 13: BeagleBone SKU + sensor suite selection against I/O budget
- [ ] Task 14: Motor driver + power distribution architecture
- [ ] Task 15: Battery + charging safety-standard selection (REFERENCES.md entry required)

## Phase 4: Software Subsystem (concept-level — expand in project-overseer)
- [ ] Task 16: Navigation/SLAM stack selection
- [ ] Task 17: Obstacle avoidance behavior tree (living-obstacle class distinct)
- [ ] Task 18: Pickup control logic
- [ ] Task 19: Dock/empty-hopper routine
- [ ] Task 20: Battery monitoring + return-to-charger behavior

## Phase 5: Integration & Validation (concept-level — expand in project-overseer)
- [ ] Task 21: Bench integration smoke test
- [ ] Task 22: Static-obstacle field test
- [ ] Task 23: Supervised living-obstacle field test
- [ ] Task 24: Full end-to-end mission test

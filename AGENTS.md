# TidySweep — AI Agent Instructions

Authoritative, model-agnostic project instructions for all AI agents (Claude,
GitHub Copilot, or any other assistant) working in this repository. IDE
integrations and other AI agents should treat this file, not model-specific
stub files, as the source of truth.

## What this project is

TidySweep is a multi-room autonomous toy-cleaning robot: a cross between a
FIRST Robotics-style active debris-collection mechanism and a Roomba-style
autonomous floor-coverage robot. It navigates multiple rooms, avoids static
obstacles (low thresholds, tables, chairs, furniture) and living obstacles
(cats, dogs, humans), picks up irregular objects up to 2 in (50.8 mm) cubes,
empties its hopper into a stationary external bin, and autonomously returns
to a charging dock when its battery is low.

**This is a real, physical build.** Every mechanical and electrical
component described in this repository is intended to be fabricated or
procured — not a conceptual exercise. Quote real mass, power, and dimension
numbers; never leave engineering values as "TBD."

## Firm constraints (not open trade studies)

- **Compute/control platform: BeagleBone ecosystem only** (BeagleBone Black,
  BeagleBone AI-64, PocketBeagle family). Design work selects *which* SKU(s)
  fit the I/O/compute budget — it does not re-litigate the platform choice.
- **Documentation license: CC-BY-SA 4.0** — see [`LICENSE-DOCS`](LICENSE-DOCS)
  and [`LICENSING.md`](LICENSING.md).
- **Hardware license: CERN-OHL-P 2.0** — see [`LICENSE-HARDWARE`](LICENSE-HARDWARE)
  and [`LICENSING.md`](LICENSING.md).
- **Living obstacles are a distinct hazard class** from static furniture.
  Cats, dogs, and humans move unpredictably and must never be contacted.
  Detection/response logic for this class must be designed and tested
  separately from generic static-obstacle avoidance — never assume it falls
  out "for free" from LIDAR occupancy mapping alone.

## Governance federation

- This root `AGENTS.md` is authoritative for the whole repository.
- Each first-level subdirectory that contains its own distinct subsystem
  (mechanical/, electrical/, software/, docs/ — created as the project
  reaches Phase 2+) will carry its own `CLAUDE.md` stub pointing back here
  and, where that subsystem has subsystem-specific rules, its own `AGENTS.md`
  cross-referencing this file. None exist yet as of Phase 0 — this repo has
  no subsystem directories.
- `TODO.md` is the authoritative top-level Work Breakdown Structure (WBS).
  `tasks/plan.md` and `tasks/todo.md` hold the detailed task breakdown for
  the currently active phase; every `TODO.md` line item maps 1:1 to an entry
  in those files (or their Phase 2+ successors, once opened).
- `PROJECT_INDEX.md` lists the current file tree and must be updated whenever
  active files are added. Archived files move out of `PROJECT_INDEX.md` into
  a corresponding `ARCHIVE_INDEX.md` (not yet created — no files have been
  archived).
- `REFERENCES.md` catalogs every standard, regulation, or technical reference
  cited anywhere in the repo, keyed by REF-ID. Never cite a standard section
  that hasn't been verified against the actual published document; mark it
  "requires verification" and open a TODO item instead of guessing.
- `Claude-MEMORY.md` is the auditable mirror of this project's Claude
  auto-memory writes. Other AI agents should maintain their own
  `<Agent>-MEMORY.md` mirror file at the repo root if they have persistent
  memory of this project.

## Engineering standards (inherited from the operator's global standards, applied here)

- **Units**: imperial-primary with metric in parentheses — e.g., `10 in
  (254 mm)`, `2.5 lbm (1.13 kg)`, `4.8 lbf (21.4 N)`. Use `lbm` for mass and
  `lbf` for force; never bare "lb" where the distinction matters. Airspeed is
  not applicable to this ground robot, but any linear/angular rate values
  follow the same imperial-primary convention.
- **Weight, balance, power, space**: every mechanical/electrical design
  decision must account for these with real numbers, tracked in the mass/
  power/space budget (see `tasks/plan.md` Task 8 / `TODO.md` §1.4).
- **Standards vetting**: any design specification with effect beyond cosmetic
  appearance must be vetted against an applicable industry standard or
  regulation before implementation, cited in `REFERENCES.md` by REF-ID.
- **Jurisdiction**: all legal/regulatory requirements are based on United
  States jurisdiction.
- **Authenticity**: no fabricated references, citations, or standards.
  Human contributors are credited by GitHub username; each AI system/model
  is cited separately for its own contribution (e.g., Claude Sonnet 5 is
  distinguished from other Claude models or other AI systems).

## Coding standards

- Language preference order: **Python3 > C++ > Bash > JavaScript**.
- 4-space indentation in all languages, regardless of language default.
- Verbose commenting per each language's convention; for formats that don't
  support inline comments (e.g., KiCad files), document decisions in an
  accompanying Markdown file instead.
- Strict linting per language; all lint rules enforced (e.g., markdownlint
  with all rules enabled for Markdown).
- All pull requests must pass CI validation (security + lint, at minimum)
  before merging.

## Workflow notes

- When adding a standards citation, check `REFERENCES.md` by REF-ID first.
  If not present, add it with a validated URL and specific section before
  using the REF-ID elsewhere. Never invent a section number.
- Any AI-generated todo list for build work must be added as WBS sub-items in
  `TODO.md` (root) and reflected in the relevant `tasks/*.md` file, so
  unresolved issues carry across sessions.

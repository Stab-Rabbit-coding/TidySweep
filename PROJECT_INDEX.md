# PROJECT_INDEX

Current active file tree for TidySweep. Update whenever active files are
added. When a file is archived, move its entry to `ARCHIVE_INDEX.md`
(not yet created — no files have been archived).

```text
TidySweep/
├── AGENTS.md              # Authoritative AI-agent instructions (model-agnostic)
├── CLAUDE.md               # Stub pointing to AGENTS.md
├── Claude-MEMORY.md        # Auditable mirror of Claude's auto-memory writes for this project
├── ConOps.md               # Phase 1: Concept of Operations (mission profile)
├── LICENSE-DOCS            # CC-BY-SA 4.0 full legal text (governs documentation)
├── LICENSE-HARDWARE        # CERN-OHL-P 2.0 full legal text (governs hardware description files)
├── LICENSING.md            # File-type → license mapping
├── MassPowerBudget.md      # Phase 1: mass/power/space/cost target allocation
├── ObstacleTaxonomy.md     # Phase 1: obstacle classes and detection/response rules
├── PayloadEnvelope.md      # Phase 1: payload size envelope + small-parts exclusion
├── PROJECT_INDEX.md        # This file
├── README.md               # Project overview and status
├── REFERENCES.md           # Standards/reference catalog (REF-ID keyed)
├── STRATEGY.md             # Product strategy anchor (ce-strategy output)
├── TODO.md                 # Authoritative top-level WBS
└── tasks/
    ├── plan.md              # Current-phase implementation plan (architecture decisions, risks, open questions)
    └── todo.md              # Detailed task breakdown with acceptance criteria for Phase 0/1
```

## Notes

- No subsystem directories (`mechanical/`, `electrical/`, `software/`)
  exist yet — they will be created when Phase 2+ design work opens, each
  with its own `CLAUDE.md`/`AGENTS.md` federation entry per `AGENTS.md`.
- No `ARCHIVE_INDEX.md` yet — nothing has been archived.

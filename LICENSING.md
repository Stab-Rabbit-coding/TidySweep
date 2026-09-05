# Licensing

TidySweep uses two licenses, split by content type, per the project's dual
documentation/hardware nature.

## Documentation — CC-BY-SA 4.0

**Applies to:** all `*.md` files, images, diagrams, ConOps/requirements text,
build guides, and any other narrative or explanatory content in this
repository (including this file).

**License:** Creative Commons Attribution-ShareAlike 4.0 International.
Full legal text: [`LICENSE-DOCS`](LICENSE-DOCS).
Canonical source: <https://creativecommons.org/licenses/by-sa/4.0/legalcode>

## Hardware — CERN-OHL-P 2.0

**Applies to:** all mechanical CAD (OpenSCAD/FreeCAD sources, STLs, STEP
files), electrical schematics, PCB layouts (KiCad projects), Gerbers, BOMs,
and any other hardware-description files in this repository.

**License:** CERN Open Hardware Licence Version 2 — Permissive.
Full legal text: [`LICENSE-HARDWARE`](LICENSE-HARDWARE).
Canonical source: <https://ohwr.org/project/cernohl/wikis/Documents/CERN-OHL-version-2>
(mirrored verbatim via the SPDX license-list-data project,
<https://github.com/spdx/license-list-data/blob/main/text/CERN-OHL-P-2.0.txt>,
since CERN's own hosting of the raw legal text has moved/changed over time).

## File-type mapping

| Glob | License |
|------|---------|
| `**/*.md`, `**/*.png`, `**/*.jpg`, `**/*.svg` (diagrams/docs) | CC-BY-SA-4.0 |
| `**/*.scad`, `**/*.FCStd`, `**/*.stl`, `**/*.step`, `**/*.stp` | CERN-OHL-P-2.0 |
| `**/*.kicad_sch`, `**/*.kicad_pcb`, `**/*.kicad_pro`, Gerbers, BOMs | CERN-OHL-P-2.0 |
| Firmware/software source (`**/*.py`, `**/*.cpp`, `**/*.sh`) | Not yet decided — open item, see `TODO.md` §0.5; CERN-OHL-P does not itself govern software licensing, so a separate software license (candidate: Apache-2.0 or MIT, compatible with CERN-OHL-P hardware description files) must be selected before firmware work begins. |

Every new source file should carry a one-line header comment (or Markdown
front-matter) naming the governing license, per this table.

# Licensing

TidySweep uses three licenses, split by content type.

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

## Firmware / software — CC0 1.0 Universal

**Applies to:** all firmware/software source in this repository (e.g.
`**/*.py`, `**/*.cpp`, `**/*.sh` on the BeagleBone Blue compute platform).

**License:** CC0 1.0 Universal (public domain dedication).
Full legal text: [`LICENSE-SOFTWARE`](LICENSE-SOFTWARE).
Canonical source: <https://creativecommons.org/publicdomain/zero/1.0/legalcode>

**Why CC0 and not CC-BY-SA 4.0 for code — decided 2026-09-05.** Creative
Commons' own FAQ recommends against using CC licenses for software:

> "We recommend against using Creative Commons licenses for software.
> Instead, we strongly encourage you to use one of the very good software
> licenses which are already available... Unlike software-specific
> licenses, CC licenses do not contain specific terms about the
> distribution of source code... [and CC licenses] don't address patent
> rights."

(<https://creativecommons.org/faq/>, fetched 2026-09-05 — see REF-LIC-004
in `REFERENCES.md`.) The one exception CC's own FAQ carries is CC0: "the
CC0 Public Domain Dedication is GPL-compatible and acceptable for
software." The operator chose CC0 over an OSI/FSF software license (e.g.
GPL-3.0, Apache-2.0, MIT) specifically to stay within the Creative Commons
family used elsewhere in this repository, while still following CC's own
guidance rather than applying CC-BY-SA to code against that guidance. This
resolves the open item previously tracked as `TODO.md` §0.5.

## File-type mapping

| Glob | License |
|------|---------|
| `**/*.md`, `**/*.png`, `**/*.jpg`, `**/*.svg` (diagrams/docs) | CC-BY-SA-4.0 |
| `**/*.scad`, `**/*.FCStd`, `**/*.stl`, `**/*.step`, `**/*.stp` | CERN-OHL-P-2.0 |
| `**/*.kicad_sch`, `**/*.kicad_pcb`, `**/*.kicad_pro`, Gerbers, BOMs | CERN-OHL-P-2.0 |
| Firmware/software source (`**/*.py`, `**/*.cpp`, `**/*.sh`) | CC0-1.0 |

Every new source file should carry a one-line header comment (or Markdown
front-matter) naming the governing license, per this table.

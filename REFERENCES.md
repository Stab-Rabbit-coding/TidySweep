# REFERENCES

Catalog of every industry standard, regulation, and authoritative technical
reference cited anywhere in this repository. Every citation in code,
documentation, schematics, or build guides must use the REF-ID assigned here.
Never invent or guess a section number — if a section cannot be verified, it
is marked "requires verification" below with a corresponding TODO in
`TODO.md`.

## Active Citations

| REF-ID | Title | URL | Section(s) Applied | Cited In |
|--------|-------|-----|---------------------|----------|
| REF-HW-001 | BeagleBone Black System Reference Manual / product page | <https://beagleboard.org/black> | Full board spec (candidate SKU for `TODO.md` §3.1 compute selection) — **requires verification**: specific I/O pinout/section not yet reviewed | `tasks/plan.md` Task 13 (pending) |
| REF-HW-002 | BeagleBone AI-64 product page | <https://beagleboard.org/ai-64> | Full board spec (candidate SKU for `TODO.md` §3.1 compute selection) — **requires verification**: specific compute/AI-accelerator section not yet reviewed | `tasks/plan.md` Task 13 (pending) |
| REF-HW-003 | PocketBeagle product page | <https://beagleboard.org/pocket> | Full board spec (candidate satellite/offload SKU for `TODO.md` §3.1) — **requires verification**: specific I/O section not yet reviewed | `tasks/plan.md` Task 13 (pending) |
| REF-LIC-001 | Creative Commons Attribution-ShareAlike 4.0 International, Legal Code | <https://creativecommons.org/licenses/by-sa/4.0/legalcode> | Full text — governs all documentation in this repository | `LICENSE-DOCS`, `LICENSING.md` |
| REF-LIC-002 | CERN Open Hardware Licence Version 2 — Permissive (CERN-OHL-P v2.0) | <https://ohwr.org/project/cernohl/wikis/Documents/CERN-OHL-version-2> (text mirrored verbatim at <https://github.com/spdx/license-list-data/blob/main/text/CERN-OHL-P-2.0.txt>) | Full text — governs all hardware description files in this repository | `LICENSE-HARDWARE`, `LICENSING.md` |
| REF-STD-001 | 16 CFR Part 1501 — Method for Identifying Toys and Other Articles Intended for Use by Children Under 3 Years of Age Which Present Choking, Aspiration, or Ingestion Hazards Because of Small Parts | <https://www.govinfo.gov/content/pkg/CFR-2023-title16-vol2/xml/CFR-2023-title16-vol2-part1501.xml> | §1501.4 (small-parts test cylinder, Figure 1) — used to define the payload-envelope exclusion boundary, verified via GovInfo XML fetch 2026-09-05 | `PayloadEnvelope.md` |

## Requires Verification (open items, tracked as TODO.md §0.x)

- REF-HW-001/002/003 above are cited at the product-page level only. Once
  `TODO.md` §3.1 (BeagleBone SKU selection) is worked, each must be updated
  to cite the specific System Reference Manual PDF and pinout table/section
  actually relied upon — see `TODO.md` §0.1.
- **REF-STD-002 (candidate, not yet an Active Citation):** ISO 13482:2014,
  "Robots and robotic devices — Safety requirements for personal care
  robots." Candidate standard to formally back the Class 3/4 stop distances
  in `ObstacleTaxonomy.md`. Attempted verification 2026-09-05 via the ISO
  catalog page (`https://www.iso.org/standard/53820.html`) and Wikipedia
  returned an anti-bot challenge / 404 respectively — **not verified this
  session**. Do not treat the stop-distance numbers in `ObstacleTaxonomy.md`
  as ISO-13482-compliant until this is confirmed with a specific section
  reference.
- Safety-relevant standards not yet added (flagged in `tasks/plan.md` Risks
  table, to be added when the corresponding design task opens):
  - Machine-guarding / pinch-point standard for the intake roller mechanism
    (`TODO.md` §2.2) — **not yet researched or cited**.
  - Battery/charging safety standard (candidate: UL 2054 or IEC 62133 family)
    for the charging system (`TODO.md` §3.3) — **not yet researched or
    cited**.

## Removed / Superseded Citations

None yet.

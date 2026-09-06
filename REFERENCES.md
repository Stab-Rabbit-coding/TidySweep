# REFERENCES

Catalog of every industry standard, regulation, and authoritative technical
reference cited anywhere in this repository. Every citation in code,
documentation, schematics, or build guides must use the REF-ID assigned here.
Never invent or guess a section number — if a section cannot be verified, it
is marked "requires verification" below with a corresponding TODO in
`TODO.md`.

## Active Citations

| REF-ID | Title | URL | Section(s) Applied | Cited In |
| -------- | ------- | ----- | --------------------- | ---------- |
| REF-HW-001 | BeagleBone Black System Reference Manual / product page | <https://beagleboard.org/black> | Full board spec — considered, not selected (see `ComputeSelection.md`) — **requires verification**: specific I/O pinout/section not reviewed | `ComputeSelection.md` |
| REF-HW-002 | BeagleBone AI-64 product page | <https://beagleboard.org/ai-64> | Full board spec — considered, not selected (see `ComputeSelection.md`, `MassPowerBudget.md` BOM-ceiling risk note) — **requires verification**: specific compute/AI-accelerator section not reviewed | `ComputeSelection.md` |
| REF-HW-003 | PocketBeagle product page | <https://beagleboard.org/pocket> | Full board spec — original (non-2) generation, not selected | `ComputeSelection.md` |
| REF-HW-004 | BeagleBone Blue product page | <https://beagleboard.org/blue> | Full board spec (onboard motor H-bridges, servo/PWM outputs, quadrature encoder inputs, 9-axis IMU, LiPo charger, WiFi/BT) — **selected** for Task 13 compute platform, see `ComputeSelection.md`. Section-level System Reference Manual citation still pending (product-page level only so far) | `ComputeSelection.md`, `MassPowerBudget.md` |
| REF-HW-005 | PocketBeagle 2 Industrial product page | <https://www.beagleboard.org/boards/pocketbeagle-2-industrial> | Full board spec (AM6254 quad Cortex-A53, 1GB DDR4, 64GB eMMC, -40 to 85°C, 72-pin header) — considered as part of a PocketBeagle 2 + PocketPilot pairing, **rejected**: no stated cape/pin compatibility across PocketBeagle generations, see `ComputeSelection.md` | `ComputeSelection.md` |
| REF-HW-006 | PocketPilot flight-controller cape, GitHub repository | <https://github.com/PocketPilot/PocketPilot> | Full repository — considered, **rejected**: targets original PocketBeagle (different SoC generation than PocketBeagle 2), repository dormant since ~2018, no PocketBeagle 2 support stated. License: CC-BY-SA-4.0 (not CERN-OHL-P) — relevant only if ever forked/derived into this repo, not for off-the-shelf purchase/use | `ComputeSelection.md` |
| REF-LIC-001 | Creative Commons Attribution-ShareAlike 4.0 International, Legal Code | <https://creativecommons.org/licenses/by-sa/4.0/legalcode> | Full text — governs all documentation in this repository | `LICENSE-DOCS`, `LICENSING.md` |
| REF-LIC-002 | CERN Open Hardware Licence Version 2 — Permissive (CERN-OHL-P v2.0) | <https://ohwr.org/project/cernohl/wikis/Documents/CERN-OHL-version-2> (text mirrored verbatim at <https://github.com/spdx/license-list-data/blob/main/text/CERN-OHL-P-2.0.txt>) | Full text — governs all hardware description files in this repository | `LICENSE-HARDWARE`, `LICENSING.md` |
| REF-STD-001 | 16 CFR Part 1501 — Method for Identifying Toys and Other Articles Intended for Use by Children Under 3 Years of Age Which Present Choking, Aspiration, or Ingestion Hazards Because of Small Parts | <https://www.govinfo.gov/content/pkg/CFR-2023-title16-vol2/xml/CFR-2023-title16-vol2-part1501.xml> | §1501.4 (small-parts test cylinder, Figure 1) — used to define the payload-envelope exclusion boundary, verified via GovInfo XML fetch 2026-09-05 | `PayloadEnvelope.md` |
| REF-STD-003 | LDraw.org File Format Specification — LEGO element dimensions in LDraw Units (LDU) | <https://www.ldraw.org/article/218> | 1×1 brick base footprint: 20 LDU × 20 LDU = 8 mm × 8 mm (1 LDU = 0.4 mm); brick height 24 LDU = 9.6 mm; stud diameter 12 LDU = 4.8 mm, stud height 4 LDU = 1.6 mm. Cross-checked against BrickLink's packaging dimension for part 3005 (0.8 × 0.8 × 1.15 cm), consistent within packaging tolerance. Both fetched 2026-09-05. LDraw's own spec notes these are "real world approximations," not exact molded-part tolerances — actual physical 1×1 bricks run slightly under 8 mm for clutch-fit, commonly cited near 7.8 mm, not independently verified against a physical part this session | `HopperMechanism.md`, `PayloadEnvelope.md` |

## Requires Verification (open items, tracked as TODO.md §0.x)

- REF-HW-004 (BeagleBone Blue, the selected SKU) is cited at the
  product-page level only. Before Task 13 closes, update it to cite the
  specific System Reference Manual PDF and pin-table section actually
  relied upon for wiring the drivetrain/actuator/encoder connections — see
  `TODO.md` §0.1.
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
  - Machine-guarding / pinch-point standard for the intake mechanism
    (`TODO.md` §2.2, `IntakeMechanism.md`) — specifically the Stage 2
    flipper's nip point and the plow-to-flipper transition — **not yet
    researched or cited**.
  - Battery/charging safety standard (candidate: UL 2054 or IEC 62133 family)
    for the charging system (`TODO.md` §3.3) — **not yet researched or
    cited**.
  - Household appliance / electric fan safety standard (candidate: UL 507
    or the IEC 60335 series) for the charging & dump station's fan-separator
    (`TODO.md` §6.3, `ChargingDumpStation.md`) — **not yet researched or
    cited**. The same machine-guarding item above extends to the station's
    fan intake, since it will operate on the floor of a home with children.
    A short-circuit/fire-risk consideration for the station's exposed
    charging contacts (now co-located with the fan) is also flagged in
    `ChargingDumpStation.md` and not yet backed by a citation.

## Removed / Superseded Citations

None yet.

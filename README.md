<!-- Python & Package Manager -->
[![Python](https://img.shields.io/badge/python-3.14-blue.svg)](https://www.python.org/)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white)](https://conventionalcommits.org)

<!-- Identity -->
[![canVODpy](https://img.shields.io/badge/canVODpy-test--data-2d6a4f)](https://github.com/nfb2021/canvodpy)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
<!-- Zenodo DOI badge — replace XXXXXXX with the assigned DOI number after first release -->
<!-- [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX) -->
[![CLIMERS @ TU Wien](https://img.shields.io/badge/CLIMERS-TU_Wien-006699)](https://www.tuwien.at/en/mg/geo/climers)
[![VODnet](https://img.shields.io/badge/-VODnet-2d6a4f?labelColor=555555&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAAAXNSR0IArs4c6QAAAHhlWElmTU0AKgAAAAgABAEaAAUAAAABAAAAPgEbAAUAAAABAAAARgEoAAMAAAABAAIAAIdpAAQAAAABAAAATgAAAAAAAABIAAAAAQAAAEgAAAABAAOgAQADAAAAAQABAACgAgAEAAAAAQAAAA6gAwAEAAAAAQAAAA4AAAAAjn8NzQAAAAlwSFlzAAALEwAACxMBAJqcGAAAAflJREFUKBWtUEtoE1EUPe+9SczHiam/aixtqi1E7aai4kK0CAVBDFZwrQs3xp2KIriYtiKuav3QRVxYKIjFVihWrCBIaaWioKidQBsxi3SwYmMmkxidYWaemYEEKUgRPHDhXu4575x3gf+NKfVD3UQ2u/Zv7wrLF8mPfV2ZH1ZCNIM7xUCAHHjyfN6wQ8mZo3vvE4Av57tzOjfd/WZpivfJSW5wkzvomnzFe2SFTyyU+iFJtCpk1eaRfOIw84TuRsN7kEkVMDzyEjPvUtga2YiDTRFM5+m+F8XYHMZuzDqaWlQf8yVMpmJ0/DUu9g6hVNQAy8au3W04NHAV85oFRulZS+LDkIjtWmcyHT6vQHYoXwrouTWKkv4LLOAHE4N4K6dxZ2AISl4DpawVDVrYcXSFZtTPGSV8IatjUVErJ+Cwbdstx3Vw8CG+pmQIHg+HUVlWo7aSp/qz9Kn3W5p5S/x4DJ8/lfGt4kAow7bmBpQ9fuQ3RUFtM4Uz61Qk/vijbpLbgtc61n05zjQ1hCvXHmB9fT3OnT8NOWfi+uxP0IJxE4S4jrXzxrffm1xlb75Aud/cEFmD9vYW6KaNUoUmCpS3BblUPNk45sR0UBM6Qzx2qd9LVnfqujGS+64puaX8olEuj4uMHHnc2dTrcFZGtCOMxv11KxP/kfEbTTzNcyb5ar0AAAAASUVORK5CYII=&logoColor=white)](https://vodnet.netlify.app)

# canVODpy — Test Data

Reference GNSS dataset for [canVODpy](https://github.com/nfb2021/canvodpy) pipeline validation and end-to-end testing. Contains real observations from **Rosalia, Austria** — DOY **2025-001** (2025-01-01), full 24-hour day. RINEX 2.11 data is from **MOFLUX, MO, US** on DOY **2025-001** by courtesy of Caltech via Christian Frankenberg. NMEA data is from **Hainich Nationalpark** receiver recorded with a **u-blox NEO-M9N** receiver (1 hour on DOY **2026-001**).

## Usage

This repository is used as the `packages/canvod-readers/tests/test_data/` submodule in canvodpy, and as the `test_data/` directory in canvodpy-demo.

**Clone for standalone use:**

```bash
# Inside canvodpy-demo
git clone https://github.com/nfb2021/canvodpy-test-data.git test_data

# Or as part of canvodpy (included automatically via submodules)
git clone --recurse-submodules https://github.com/nfb2021/canvodpy.git
```

---

## Structure

```text
test_data/
├── valid/
│   ├── rinex_v3_04/                           # RINEX v3.04 observation files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/01_GNSS/01_raw/
│   │       │   └── 25001/                     # 96 × 15-min files (rref001*.25o)
│   │       └── 02_canopy/01_GNSS/01_raw/
│   │           └── 25001/                     # 96 × 15-min files (ract001*.25o)
│   │
│   ├── rinex_v2_11/                           # RINEX v2.11 observation files (Missouri Ozark Site, Missouri, US)
│   │   └── 02_Moflux/
│   │       ├── 01_reference/
│   │       │   └── 25001/                     # 24 × 1-hour files (MOZR01CAL_R_*.rnx)
│   │       └── 02_canopy/
│   │           └── 25001/                     # 24 × 1-hour files (MOZA01CAL_R_*.rnx)
│   │
│   ├── sbf/                                   # Septentrio Binary Format files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/            # 96 × 15-min files (rref001*.25_)
│   │       └── 02_canopy/25001/               # 96 × 15-min files (ract001*.25_)
│   │
│   ├── nmea/                                  # NMEA files
│   │   ├── 01_Rosalia/
│   │       ├── 01_reference/25001/            # 96 × 15-min files (rref001*.251)
│   │       └── 02_canopy/25001/               # 96 × 15-min files (ract001*.251)
│   │
│   │   └── 02_Hainich/                        # u-blox NEO-M9N, 1-hour campaign (01.01.2026)
│   │       ├── 01_reference/                  # HAIR02MPI_R_20260010000_01H_01S_AA.nmea
│   │       └── 02_canopy/                     # HAIA02MPI_R_20260010000_01H_01S_AA.nmea
│   │
│   ├── rinex_v3_04_nav_data/                  # RINEX v3.04 Mixed Navigation Data
│   │   ├── 01_reference/                      # 96 × 15-min files (rref001*.25p)
│   │   └── 02_canopy/                         # 96 × 15-min files (ract001*.25p)
│   │
│   ├── rinex_v3_05_stripped/                  # Stripped RINEX v3.05 observation files (MPI-BGC)
│   │   └── 01_ExampleSite/
│   │       ├── 01_reference/25001/            # EXPR01MPI_R_20250010000_10S_01S_AA.rnx
│   │       └── 01_canopy/25001/               # EXPA01MPI_R_20250010000_10S_01S_AA.rnx
│   │
│   ├── broadcast_ephemerides/                 # Broadcast ephemeris data (from SBF)
│   │   └── 02_canopy/
│   │
│   ├── aux_data/                              # Precise ephemeris products + aux Zarr
│   │   ├── 01_SP3/                            # COD0MGXFIN 2025-001 orbit (5 min)
│   │   ├── 02_CLK/                            # COD0MGXFIN 2025-001 clock (30 s)
│   │   └── aux_2025001.zarr/                  # Pre-computed SP3/CLK interpolation cache
│   │
│   └── stores/
│       └── rosalia_rinex/                     # Icechunk store snapshot for store tests
│
├── invalid/                                   # Malformed RINEX files for parser robustness
│   ├── binary_garbage.25o
│   ├── bitflip_numeric.25o
│   ├── blank_lines_in_data.25o
│   ├── blank_observations.25o
│   ├── crlf_line_endings.25o
│   ├── duplicate_epochs.25o
│   ├── duplicate_obs_types.25o
│   ├── empty.25o
│   ├── event_epoch.25o
│   ├── extra_long_sat_line.25o
│   ├── header_only.25o
│   ├── huge_satellite_count.25o
│   ├── invalid_epoch_flag.25o
│   ├── invalid_month.25o
│   ├── invalid_satellite_id.25o
│   ├── leap_second.25o
│   ├── misaligned_observations.25o
│   ├── missing_end_of_header.25o
│   ├── missing_obs_types.25o
│   ├── mixed_valid_corrupt.25o
│   ├── multiple_end_of_header.25o
│   ├── negative_seconds.25o
│   ├── non_ascii_header.25o
│   ├── non_numeric_observations.25o
│   ├── null_bytes.25o
│   ├── obs_type_count_mismatch.25o
│   ├── reversed_epochs.25o
│   ├── satellite_count_mismatch.25o
│   ├── truncated_at_epoch_boundary.25o
│   ├── truncated_header.25o
│   ├── truncated_mid_epoch.25o
│   ├── truncated_sat_line.25o
│   ├── wrong_version_v2.25o
│   ├── wrong_version_v4.25o
│   ├── zero_position.25o
│   └── zero_satellites.25o
│
├── LICENSE
└── README.md
```

The RINEX v2.11 data in `valid/rinex_v2_11/` are from the Missouri Ozark Site in
Missouri, US, by courtesy of Christian Frankenberg and Vincent Humphrey.

---

## Receivers

| ID             | Type               | Station code | Formats                             |
| -------------- | ------------------ | ------------ | ----------------------------------- |
| `reference_01` | Open-sky reference | `rref`       | RINEX v3.04, RINEX v2.11, SBF, NMEA |
| `canopy_01`    | Below-canopy       | `ract`       | RINEX v3.04, RINEX v2.11, SBF, NMEA |

---

## File naming

RINEX short-name convention:

```text
ract001d00.25o
└┬┘└┬┘└┬┘└┬┘└┬─┬┘
 │  │  │  │  │ └── Extension: o = observation, _ = SBF, 1 = NMEA
 │  │  │  │  └──── Year: 25 (2025)
 │  │  │  └─────── Session: 00 / 15 / 30 / 45 (minutes)
 │  │  └────────── Hour letter: a=00h … x=23h
 │  └───────────── DOY: 001
 └──────────────── Station: ract (Rosalia canopy), rref (Rosalia reference)
```

---

## Auxiliary data

COD (Center for Orbit Determination in Europe) final products, 2025-001:

| File                                     | Product                   | Interval |
| ---------------------------------------- | ------------------------- | -------- |
| `COD0MGXFIN_20250010000_01D_05M_ORB.SP3` | Multi-GNSS precise orbits | 5 min    |
| `COD0MGXFIN_20250010000_01D_30S_CLK.CLK` | Precise satellite clocks  | 30 s     |

---

## Invalid test files

The `invalid/` directory contains 36 malformed RINEX v3 observation files, each targeting a specific parser failure mode: truncation, corruption, structural violations, encoding issues, and edge cases (leap seconds, event epochs). Used by `test_reader_invalid.py` to verify graceful error handling.

---

## Icechunk store snapshot

`valid/stores/rosalia_rinex/` is a pre-built Icechunk store containing ingested RINEX data from the Rosalia canopy receiver. Used by store-level tests that need a real repository without running the full ingest pipeline.

---

## Ignored files

The `.gitignore` excludes:

- `.DS_Store` — macOS metadata
- `*.db` — runtime SQLite caches (e.g. `gnss_satellites_cache.db`)

---

## Data providers

| Contributor             | Affiliation                       | Data                               |
| ----------------------- | --------------------------------- | ---------------------------------- |
| Nicolas François Bader  | CLIMERS, TU Wien                  | Rosalia RINEX v3.04, SBF, NMEA     |
| Wouter Dorigo           | CLIMERS, TU Wien                  | Rosalia RINEX v3.04, SBF, NMEA     |
| Eugenio Diaz-Pines      | BFW / KIT / UPM / BOKU           | Head of Rosalia Research Forest    |
| Christian Frankenberg   | Caltech                           | MOFLUX RINEX v2.11                 |
| Vincent Humphrey        | MeteoSwiss                        | MOFLUX RINEX v2.11                 |
| Konstantin Schellenberg | FSU Jena / MPI-BGC                | Hainich NMEA (u-blox NEO-M9N)      |

---

## Zenodo release — Option A plan

This dataset will be published on Zenodo as a versioned, citable record.
Metadata is prepared in `.zenodo.json` and `CITATION.cff`.

### Pre-upload checklist

- [x] Fill in all ORCID placeholders in `CITATION.cff` and `.zenodo.json`
- [x] Resolve SP3/CLK duplication — canonical location is `valid/aux_data/{01_SP3,02_CLK}/`;
  duplicate copies under `valid/aux_data/00_aux_files/` and `valid/rinex_v3_04/01_Rosalia/`
  have been removed.
- [x] Commit `aux_2025001.zarr` — removed `*.zarr/` from `.gitignore`; the cache is
  included in the GitHub release archive and in `aux_data.tar.gz`. Required by demo
  notebooks 07 and 17.
- [x] Rename `valid/broadcast_epehemrides/` → `valid/broadcast_ephemerides/` (typo fixed).
- [ ] Add `related_identifiers` entry for `canvodpy-demo` once that repo is public.

### Archive structure (Option A — one archive per format type)

Each archive maps 1:1 to a top-level subdirectory under `valid/`. After extraction
all archives reconstruct the same `valid/` tree and require no path changes in
`_paths.py`.

| Archive                       | Contents                                            | Approx. compressed size |
| ----------------------------- | --------------------------------------------------- | ----------------------- |
| `rinex_v3_04.tar.gz`          | RINEX v3.04 obs, Rosalia                            | ~160 MB                 |
| `sbf.tar.gz`                  | SBF binary, Rosalia                                 | ~2.2 GB                 |
| `nmea.tar.gz`                 | NMEA, Rosalia + Hainich                             | ~35 MB                  |
| `aux_data.tar.gz`             | SP3, CLK, `aux_2025001.zarr`                        | ~290 MB                 |
| `rinex_v2_11.tar.gz`          | RINEX v2.11, MOFLUX                                 | ~9 MB                   |
| `rinex_v3_05_stripped.tar.gz` | Stripped RINEX v3.05, ExampleSite (MPI-BGC)         | < 1 MB                  |
| `nav_data.tar.gz`             | RINEX nav data (.25p), Rosalia                      | ~1.5 MB                 |
| `stores.tar.gz`               | Icechunk store snapshot, Rosalia                    | < 1 MB                  |
| `invalid.tar.gz`              | 36 malformed RINEX files                            | ~2.5 MB                 |

### Pooch integration (`_paths.py`)

After the Zenodo DOI is assigned, `_paths.py` in `canvodpy-demo` will be updated
to add a third resolution path that downloads and caches archives on first access:

```text
Resolution order:
1. Monorepo  → packages/canvod-readers/tests/test_data/valid/   (dev)
2. Standalone clone → ./test_data/valid/                         (git clone)
3. Pooch cache → ~/.cache/canvodpy/test_data/valid/              (auto-download)
```

Each path constant (`ROSALIA_CANOPY_DIR`, `SBF_CANOPY_DIR`, etc.) triggers
download of only the required archive, not the full dataset.

---

## License

Data collected by TU Wien, Department of Geodesy and Geoinformation.
[Apache License 2.0](LICENSE)

---

## Affiliation

Collected and maintained by **Nicolas François Bader**

[Climate and Environmental Remote Sensing Research Unit (CLIMERS)](https://www.tuwien.at/en/mg/geo/climers)
Department of Geodesy and Geoinformation, TU Wien

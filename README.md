# canvod-readers Test Data

Test data for canvod-readers package validation and end-to-end pipeline testing.
Covers **Rosalia, Austria** — DOY **2025-001** (2025-01-01), full 24-hour day.

## Structure

```
test_data/
├── valid/
│   ├── rinex_v3_04/                           # RINEX v3.04 observation files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/01_GNSS/01_raw/
│   │       │   └── 25001/                     # 96 × 15-min files (rref001*.25o)
│   │       └── 02_canopy/01_GNSS/01_raw/
│   │           └── 25001/                     # 96 × 15-min files (ract001*.25o)
│   │
│   ├── sbf/                                   # Septentrio Binary Format files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/            # 96 × 15-min files (rref001*.25_)
│   │       └── 02_canopy/25001/               # 96 × 15-min files (ract001*.25_)
│   │
│   ├── nmea/                                  # NMEA files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/            # 96 × 15-min files (rref001*.251)
│   │       └── 02_canopy/25001/               # 96 × 15-min files (ract001*.251)
│   │
│   ├── rinex_v3_04_nav_data/                  # RINEX v3.04 Mixed Navigation Data
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/            # 96 × 15-min files (rref001*.25p)
│   │       └── 02_canopy/25001/               # 96 × 15-min files (ract001*.25p)
│   │
│   ├── broadcast_ephemerides/                 # Broadcast ephemeris data (from SBF)
│   │   └── 02_canopy/
│   │
│   ├── aux_data/                              # Precise ephemeris products
│   │   ├── 00_aux_files/
│   │   │   ├── 01_SP3/                        # COD0MGXFIN 2025-001 orbit (5 min)
│   │   │   └── 02_CLK/                        # COD0MGXFIN 2025-001 clock (30 s)
│   │   ├── 01_SP3/                            # SP3 (pipeline search path)
│   │   └── 02_CLK/                            # CLK (pipeline search path)
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

## Receivers

| ID | Type | Station code | Format |
| --- | --- | --- | --- |
| `reference_01` | Open-sky reference | `rref` | RINEX v3.04, SBF |
| `canopy_01` | Below-canopy | `ract` | RINEX v3.04, SBF |

## File naming

RINEX short-name convention:

```
ract001d00.25o
└┬┘└┬┘└┬┘└┬┘└┬─┬┘
 │  │  │  │  │ └── Extension: o = observation, _ = SBF
 │  │  │  │  └──── Year: 25 (2025)
 │  │  │  └─────── Session: 00 / 15 / 30 / 45 (minutes)
 │  │  └────────── Hour letter: a=00h … x=23h
 │  └───────────── DOY: 001
 └──────────────── Station: ract (Rosalia canopy), rref (Rosalia reference)
```

## Auxiliary data

COD (Center for Orbit Determination in Europe) final products, 2025-001:

| File | Product | Interval |
| --- | --- | --- |
| `COD0MGXFIN_20250010000_01D_05M_ORB.SP3` | Multi-GNSS precise orbits | 5 min |
| `COD0MGXFIN_20250010000_01D_30S_CLK.CLK` | Precise satellite clocks | 30 s |

## Invalid test files

The `invalid/` directory contains 36 malformed RINEX v3 observation files,
each targeting a specific parser failure mode: truncation, corruption,
structural violations, encoding issues, and edge cases (leap seconds,
event epochs). Used by `test_reader_invalid.py` to verify graceful
error handling.

## Icechunk store snapshot

`valid/stores/rosalia_rinex/` is a pre-built Icechunk store containing
ingested RINEX data from the Rosalia canopy receiver. Used by store-level
tests that need a real repository without running the full ingest pipeline.

## Ignored files

The `.gitignore` excludes:

- `.DS_Store` — macOS metadata
- `*.db` — runtime SQLite caches (e.g. `gnss_satellites_cache.db`)
- `*.zarr/` — transient Zarr preprocessing caches (rebuilt each run)

## License

Data collected by TU Wien, Department of Geodesy and Geoinformation.

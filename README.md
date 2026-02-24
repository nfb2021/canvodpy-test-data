# canvod-readers Test Data

Test data for canvod-readers package validation and end-to-end pipeline testing.
Covers **Rosalia, Austria** — DOY **2025-001** (2025-01-01), full 24-hour day.

## Structure

```
test_data/
├── valid/
│   ├── rinex_v3_04/                         # RINEX v3.04 observation files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/01_GNSS/01_raw/
│   │       │   └── 25001/                   # 96 × 15-min files (rref001*.25o)
│   │       └── 02_canopy/01_GNSS/01_raw/
│   │           └── 25001/                   # 96 × 15-min files (ract001*.25o)
│   │
│   ├── sbf/                                 # Septentrio Binary Format files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/          # 96 × 15-min files (rref001*.25_)
│   │       └── 02_canopy/25001/             # 96 × 15-min files (ract001*.25_)
│   │
│   ├── nmea/                                # NMEA files
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/          # 96 × 15-min files (rref001*.251)
│   │       └── 02_canopy/25001/             # 96 × 15-min files (ract001*.251)
│   │
│   ├── rinex_v3_04_nav_data/                 # Rinex v3.04 Mixed Navigation Data
│   │   └── 01_Rosalia/
│   │       ├── 01_reference/25001/          # 96 × 15-min files (rref001*.25p)
│   │       └── 02_canopy/25001/             # 96 × 15-min files (ract001*.25p)
│   │
│   ├── aux/                                 # Precise ephemeris products
│   │   ├── 00_aux_files/
│   │   │   ├── 01_SP3/                      # COD0MGXFIN 2025-001 orbit (5 min)
│   │   │   └── 02_CLK/                      # COD0MGXFIN 2025-001 clock (30 s)
│   │   ├── 01_SP3/                          # SP3 (pipeline search path)
│   │   └── 02_CLK/                          # CLK (pipeline search path)
│   └── stores/
│       └── rosalia_rinex/                   # Icechunk store snapshot for store tests
└── README.md
```

## Receivers

| ID             | Type               | Station code | Format           |
| -------------- | ------------------ | ------------ | ---------------- |
| `reference_01` | Open-sky reference | `rref`       | RINEX v3.04, SBF |
| `canopy_01`    | Below-canopy       | `ract`       | RINEX v3.04, SBF |

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

| File                                     | Product                   | Interval |
| ---------------------------------------- | ------------------------- | -------- |
| `COD0MGXFIN_20250010000_01D_05M_ORB.SP3` | Multi-GNSS precise orbits | 5 min    |
| `COD0MGXFIN_20250010000_01D_30S_CLK.CLK` | Precise satellite clocks  | 30 s     |

## Ignored files

The `.gitignore` excludes:

- `.DS_Store` — macOS metadata
- `*.db` — runtime SQLite caches (e.g. `gnss_satellites_cache.db`)
- `*.zarr/` — transient Zarr preprocessing caches (rebuilt each run)

## License

Data collected by TU Wien, Department of Geodesy and Geoinformation.

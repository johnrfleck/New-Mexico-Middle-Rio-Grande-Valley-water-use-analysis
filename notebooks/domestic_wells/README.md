# Domestic Wells Notebooks

## `domestic_wells_replication.ipynb` (Python)

Counts active domestic wells and their permitted diversion inside the MRGCD jurisdictional area and
the ABCWUA service area, reproducing the numbers in the accompanying white paper and talk
(MRGCD 24,239 wells / 67,389 AF; ABCWUA 8,557 / 24,406, OSE POD vintage 2026-06-15). It prints the
full counting ladder so every modeling choice is visible, validates against the published figures,
and plots cumulative permitted diversion over time.

- **Language / kernel:** Python 3 (`geopandas`, `pandas`, `shapely`, `matplotlib`).
- **Inputs:** three public shapefiles that are **not** committed here — see
  `../../data/domestic_wells/README.md` for where to download each one and where to place it.
- **Method summary:** `../../docs/domestic_wells/README.md`.

Run the cells in order; the notebook unzips the source shapefiles on first run and writes derived
CSVs + a chart to `data/domestic_wells/output/`.

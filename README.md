# New Mexico Middle Rio Grande Valley Water Use Analysis

This repository supports public review and replication of analyses related to water use in New Mexico's Middle Rio Grande Valley.

**📊 View the analysis site:** https://[your-username].github.io/New-Mexico-Middle-Rio-Grande-Valley-water-use-analysis/ (once GitHub Pages is enabled)

The first analysis lane focuses on **Net Flow Reduction (NFR)** between the Rio Grande at Otowi Bridge and the downstream San Marcial gages. NFR is an accounting measure:

`NFR = upstream inflow - downstream outflow`

It is not, by itself, a direct measurement of consumptive use. The difference can reflect human water use, riparian vegetation, evaporation, groundwater-surface water interactions, channel and reservoir operations, measurement issues, and climate variability. The goal of the notebooks is to make the accounting transparent enough that these possible explanations can be examined carefully.

## Current Contents

- `notebooks/nfr/01_define_nfr_and_build_series.ipynb` (R) — downloads USGS daily streamflow data,
  applies a three-gage completeness screen, converts daily mean discharge to annual acre-feet, and
  writes an annual NFR table.
- `notebooks/domestic_wells/domestic_wells_replication.ipynb` (Python) — counts active domestic wells
  and their permitted diversion inside the MRGCD jurisdictional area and the ABCWUA service area,
  reproducing the published figures (MRGCD 22,916 wells / 63,477 AF; ABCWUA 7,901 / 22,465). Prints
  the full counting ladder, validates against the published numbers, and charts cumulative permitted
  diversion over time. Source shapefiles are not committed — see
  `data/domestic_wells/README.md` for where to obtain them.

Additional notebooks, data notes, and Google Earth Engine scripts will be added as they are reviewed
and rewritten for public use.

## Repository Layout

- `notebooks/nfr/`: Net Flow Reduction notebooks.
- `notebooks/domestic_wells/`: domestic-wells analysis notebooks, when ready.
- `data/nfr/`: derived NFR data products created by the notebooks.
- `data/domestic_wells/`: instructions and outputs for domestic-wells analyses. Large source spatial datasets are not committed.
- `docs/`: methodology notes and source documentation.
- `gee/`: Google Earth Engine scripts or notes used to generate spatial and remote-sensing inputs.

## Running The Notebooks

Notebooks are written in the language each analysis was actually done in; open each in Jupyter (or
any notebook environment with the right kernel) and run the cells in order.

**`notebooks/nfr/` (R kernel)** — uses the USGS `dataRetrieval` package. Required R packages:
`dataRetrieval`, `dplyr`, `tidyr`, `readr`, `ggplot2`, `scales`.

**`notebooks/domestic_wells/` (Python 3 kernel)** — install dependencies with
`pip install -r requirements.txt` (`geopandas`, `pandas`, `shapely`, `matplotlib`). Download the
three source shapefiles first (see `data/domestic_wells/README.md`); the notebook unzips them on
first run.

## Status

This is an active public working repository. The material here is being shared early to make the analysis easier to inspect, question, and improve.

Interpretive claims should be treated as provisional unless they are supported directly by the notebooks and accompanying documentation.

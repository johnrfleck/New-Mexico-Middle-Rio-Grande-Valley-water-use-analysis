# New Mexico Middle Rio Grande Valley Water Use Analysis

This repository supports public review and replication of analyses related to water use in New Mexico's Middle Rio Grande Valley.

**📊 View the analysis site:** https://johnrfleck.github.io/New-Mexico-Middle-Rio-Grande-Valley-water-use-analysis/

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
- `notebooks/quadrant_map/quadrant_map_replication.ipynb` (Python) — reproduces "The Greening (and
  Browning) of the Albuquerque Metro Area," a five-class map of where water use (effective
  evapotranspiration) is rising or falling across the metro area, 2001–2024. Pulls water-use data
  live from Google Earth Engine (requires your own free GEE account — the notebook walks through
  signup) and the area boundary live from the Census Bureau's public TIGERweb API. No data
  download needed.

Additional notebooks, data notes, and Google Earth Engine scripts will be added as they are reviewed
and rewritten for public use.

## Repository Layout

- `notebooks/nfr/`: Net Flow Reduction notebooks.
- `notebooks/domestic_wells/`: domestic-wells analysis notebooks.
- `notebooks/quadrant_map/`: water-use trend quadrant-map notebook (Google Earth Engine).
- `data/nfr/`: derived NFR data products created by the notebooks.
- `data/domestic_wells/`: instructions and outputs for domestic-wells analyses. Large source spatial datasets are not committed.
- `data/quadrant_map/`: notes on Earth Engine setup; notebook outputs are written to `output/` (not committed).
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

**`notebooks/quadrant_map/` (Python 3 kernel)** — install dependencies with
`pip install -r requirements.txt` (`earthengine-api`, `geopandas`, `requests`, `rasterio`, `scipy`,
`matplotlib`). Requires your own free Google Earth Engine account and Google Cloud project — the
notebook's setup section walks through the five-minute signup and authentication. No manual data
download needed; the AOI and rasters are both fetched live.

## Status

This is an active public working repository. The material here is being shared early to make the analysis easier to inspect, question, and improve.

Interpretive claims should be treated as provisional unless they are supported directly by the notebooks and accompanying documentation.

## License

- **Code** (notebooks, scripts) — [MIT License](LICENSE).
- **Written content and figures** (`docs/`, methodology notes, charts) — [CC BY 4.0](LICENSE-CONTENT.md).

© 2026 John Fleck and Bob Berrens.

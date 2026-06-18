# New Mexico Middle Rio Grande Valley Water Use Analysis

This repository supports public review and replication of analyses related to water use in New Mexico's Middle Rio Grande Valley.

The first analysis lane focuses on **Net Flow Reduction (NFR)** between the Rio Grande at Otowi Bridge and the downstream San Marcial gages. NFR is an accounting measure:

`NFR = upstream inflow - downstream outflow`

It is not, by itself, a direct measurement of consumptive use. The difference can reflect human water use, riparian vegetation, evaporation, groundwater-surface water interactions, channel and reservoir operations, measurement issues, and climate variability. The goal of the notebooks is to make the accounting transparent enough that these possible explanations can be examined carefully.

## Current Contents

The repository currently includes the first public NFR notebook:

- `notebooks/nfr/01_define_nfr_and_build_series.ipynb`

That notebook downloads USGS daily streamflow data, applies a three-gage completeness screen, converts daily mean discharge to annual acre-feet, and writes an annual NFR table.

Additional notebooks, data notes, Google Earth Engine scripts, and domestic-wells analysis materials will be added as they are reviewed and rewritten for public use.

## Repository Layout

- `notebooks/nfr/`: Net Flow Reduction notebooks.
- `notebooks/domestic_wells/`: domestic-wells analysis notebooks, when ready.
- `data/nfr/`: derived NFR data products created by the notebooks.
- `data/domestic_wells/`: instructions and outputs for domestic-wells analyses. Large source spatial datasets are not committed.
- `docs/`: methodology notes and source documentation.
- `gee/`: Google Earth Engine scripts or notes used to generate spatial and remote-sensing inputs.

## Running The Notebook

The current notebook is written in R and uses the USGS `dataRetrieval` package.

Required R packages include:

- `dataRetrieval`
- `dplyr`
- `tidyr`
- `readr`
- `ggplot2`
- `scales`

Open the notebook in Jupyter or another notebook environment with an R kernel, then run the cells in order.

## Status

This is an active public working repository. The material here is being shared early to make the analysis easier to inspect, question, and improve.

Interpretive claims should be treated as provisional unless they are supported directly by the notebooks and accompanying documentation.

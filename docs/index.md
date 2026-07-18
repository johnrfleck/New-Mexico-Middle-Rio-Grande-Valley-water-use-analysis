# NM Middle Rio Grande Water Analysis

This repository supports public review and replication of analyses related to water use in New Mexico's Middle Rio Grande Valley.

## Domestic Wells Analysis (MRGCD & ABCWUA)

How many active domestic wells are located inside the boundaries of the Middle Rio Grande Conservancy District and the Albuquerque Bernalillo County Water Utility Authority service area?

- **[Methodology & caveats](domestic_wells/README.md)** — Overview of the counting ladder and data quality issues
- **[Interactive replication notebook](notebooks/domestic_wells/)** — Run the analysis yourself; explores OSE POD records, applies boundary logic, and reproduces published figures
- **Published results (OSE POD vintage 2026-06-15):**
  - MRGCD: 22,916 wells / 63,477 acre-feet per year
  - ABCWUA: 7,901 wells / 22,465 acre-feet per year

## Net Flow Reduction Analysis (Otowi–San Marcial)

What is the net flow reduction (NFR) between the Rio Grande at Otowi Bridge and downstream San Marcial gages? NFR is an accounting measure, not a direct measurement of consumptive use.

- **[Methodology](nfr/README.md)** — Gage selection, completeness screening, and limitations
- **[R analysis notebook](notebooks/nfr/)** — Downloads USGS daily streamflow data, computes annual acre-feet

## Running The Notebooks

Each notebook can be opened in Jupyter, JupyterLab, or Google Colab. See the notebook READMEs for language, dependencies, and data download instructions.

- **Domestic wells** (Python 3): `geopandas`, `pandas`, `shapely`, `matplotlib`
- **Net Flow Reduction** (R): `dataRetrieval`, `dplyr`, `tidyr`, `readr`, `ggplot2`, `scales`

## Status

This is an active public working repository. Material here is shared early to make the analysis easier to inspect, question, and improve.

Interpretive claims should be treated as provisional unless directly supported by the notebooks and documentation.

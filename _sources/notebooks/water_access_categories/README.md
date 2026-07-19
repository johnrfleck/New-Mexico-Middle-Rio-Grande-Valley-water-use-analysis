# Water Access Categories Notebooks

## `water_access_categories_replication.ipynb` (Python)

Reproduces three companion charts comparing lot size and water use across Bernalillo County
residential parcels inside the ABCWUA service area, split into four water-access categories
(ABCWUA only / + well / + ditch / + well + ditch).

- **Language / kernel:** Python 3 (`earthengine-api`, `geopandas`, `pandas`, `requests`,
  `shapely`, `matplotlib`).
- **Inputs:** Bernalillo County residential parcels are fetched live (no download needed) from
  the county's public ArcGIS REST feature service. Three shapefiles are **not committed** — see
  `../../data/water_access_categories/README.md` for where to obtain each one (two are public
  downloads; the MRGCD ISOlog layer must be requested directly from MRGCD). You also need your
  own free Google Earth Engine account and Google Cloud project — the notebook's setup section
  walks through signup.
- **Method summary:** `../../docs/water_access_categories/README.md`.
- **Published figures for comparison:** `../../docs/water_access_categories/lot_size_by_category_full_abcwua.png`,
  `effective_et_by_category_full_abcwua.png`, `total_water_use_by_category_full_abcwua.png`.

Run the cells in order. Step 4 (per-parcel effective ET via Earth Engine) is the slow step —
expect tens of minutes for the full ~190,000-parcel population. The notebook writes its charts
and derived outputs to `data/water_access_categories/output/`.

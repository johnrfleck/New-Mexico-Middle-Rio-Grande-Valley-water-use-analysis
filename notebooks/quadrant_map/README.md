# Quadrant Map Notebooks

## `quadrant_map_replication.ipynb` (Python)

Reproduces "The Greening (and Browning) of the Albuquerque Metro Area" — a five-class map of where
water use (effective evapotranspiration) has been rising or falling across the Albuquerque metro
area, 2001–2024.

- **Language / kernel:** Python 3 (`earthengine-api`, `geopandas`, `requests`, `rasterio`,
  `scipy`, `numpy`, `matplotlib`).
- **Inputs:** none to download — the area of interest is fetched live from the Census Bureau's
  public TIGERweb API, and the water-use rasters are pulled live from Google Earth Engine. You do
  need your own **free Google Earth Engine account and Google Cloud project** — the notebook's
  setup section walks through creating one and authenticating.
- **Method summary:** `../../docs/quadrant_map/README.md`.
- **Published figure for comparison:** `../../docs/quadrant_map/openet_quadrant_map_urbanarea_minus_river.png`.

Run the cells in order. The notebook downloads two GeoTIFFs (baseline and trend rasters) to
`data/quadrant_map/output/` and writes the rendered map there as well.

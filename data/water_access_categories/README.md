# Water Access Categories — data and how to obtain it

The water-access-categories replication notebook
(`notebooks/water_access_categories/water_access_categories_replication.ipynb`) needs **three
source shapefiles** — two of them the same public files used by the domestic-wells notebook (see
`data/domestic_wells/README.md` for full detail) plus one new one that has no public download.
They are not committed to this repository. Download/obtain them yourself, zip each one as
described below, and place the zips in `data/water_access_categories/input/source_shapefiles/`.
The notebook unzips them on first run.

**Bernalillo County residential parcels need no download** — the notebook fetches them live from
the county's public ArcGIS REST feature service.

## The three inputs

| Put this file here (`input/source_shapefiles/`) | Shapefile inside the zip | Source |
|---|---|---|
| `OSE_PODs.zip` | `Points_of_Diversion.shp` (+ sidecars) | NM OSE Points of Diversion (public) |
| `ABCWUAServiceArea.zip` | `ABCWUAServiceArea.shp` (+ sidecars) | OSE Public Water System boundary for ABCWUA (public) |
| `MRGCD_ISOlog.zip` | `MRGCDISOLogs2021.shp` (+ sidecars) | MRGCD 2021 ISOlog — **obtained from MRGCD**, not publicly downloadable |

Each zip must contain the shapefile and **all its sidecars** (`.shp`, `.shx`, `.dbf`, `.prj`,
`.cpg`) at the **root** of the zip (no enclosing folder). If your download uses different
filenames, either rename to match the table above or edit the `ARCHIVES` dictionary in the
notebook's setup cell.

---

### 1. OSE Points of Diversion (`OSE_PODs.zip`)

Same file used by the domestic-wells notebook — see `data/domestic_wells/README.md` for the full
download instructions, location-quality caveat, and vintage note. If you already downloaded this
for that notebook, just copy the same zip here.

### 2. ABCWUA service-area boundary (`ABCWUAServiceArea.zip`)

Same file used by the domestic-wells notebook — see `data/domestic_wells/README.md` for download
instructions and the open boundary-provisionality caveat. Copy the same zip here if you already
have it.

### 3. MRGCD 2021 ISOlog (`MRGCD_ISOlog.zip`)

MRGCD's parcel-level irrigation service log (2021 vintage) — the "which parcels have ditch/acequia
water access" layer used as the "ditch water" proxy in this analysis. **Obtained from MRGCD** —
this is not published on a public open-data portal.

- **Source:** Middle Rio Grande Conservancy District, Mapping & GIS —
  <https://www.mrgcd.com/mapping-gis/>. Request the ISOlog layer directly from MRGCD
  (`mapping@mrgcd.us`) if it isn't available through the public Data Viewer at
  <https://maps.mrgcd.com>.
- **CRS:** NAD83(HARN) / New Mexico Central (ftUS). The notebook reprojects it.
- **What it represents:** parcel-level records of MRGCD-serviceable irrigated land, 2021. This
  analysis uses it as a **proxy for ditch/acequia water access**, not a literal record of water
  rights or actual diversions — see the notebook's caveats section.

---

## Directory layout

```
data/water_access_categories/
  input/
    source_shapefiles/      <- put the three .zip files here (git-ignored)
    working_unzipped/        <- notebook extracts here (git-ignored)
  output/                    <- regenerated CSVs + chart PNGs (git-ignored)
```

The notebook is the source of truth for the classification method; see
`docs/water_access_categories/README.md` for the methodology summary.

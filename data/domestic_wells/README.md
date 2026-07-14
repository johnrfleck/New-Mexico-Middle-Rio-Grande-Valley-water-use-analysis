# Domestic Wells — data and how to obtain it

The domestic-wells replication notebook
(`notebooks/domestic_wells/domestic_wells_replication.ipynb`) needs **three public source
shapefiles**. They are large and/or third-party, so they are **not committed** to this repository.
Download them yourself, zip each one as described below, and place the zips in
`data/domestic_wells/input/source_shapefiles/`. The notebook unzips them on first run.

## The three inputs

| Put this file here (`input/source_shapefiles/`) | Shapefile inside the zip | Source |
|---|---|---|
| `OSE_PODs.zip` | `Points_of_Diversion.shp` (+ sidecars) | NM OSE Points of Diversion |
| `MRGCD-Jurisdictional-Boundary.zip` | `MRGCD_Jurisdictional_Area.shp` (+ sidecars) | MRGCD jurisdictional boundary |
| `ABCWUAServiceArea.zip` | `ABCWUAServiceArea.shp` (+ sidecars) | OSE Public Water System boundary for ABCWUA |

Each zip must contain the shapefile and **all its sidecars** (`.shp`, `.shx`, `.dbf`, `.prj`,
`.cpg`) at the **root** of the zip (no enclosing folder). If your download uses different filenames,
either rename to match the table above or edit the `ARCHIVES` dictionary in the notebook's setup cell.

---

### 1. OSE Points of Diversion (`OSE_PODs.zip`)

Every permitted well and surface diversion in New Mexico, from the OSE **W.A.T.E.R.S.** database,
statewide, point geometry with ~100 attribute fields. **Updated monthly**, so a fresh download will
differ from the vintage used here.

- **Download (shapefile):** NM OSE geospatial open-data portal —
  <https://geospatialdata-ose.opendata.arcgis.com/datasets/ose-points-of-diversion>
- **Mirror + data dictionary (`nmose_WATERS_PODs_data_dictionary_v8.xlsx`):** NM Water Data catalog —
  <https://catalog.newmexicowaterdata.org/dataset/ose-points-of-diversion>
- **CRS:** NAD83 UTM Zone 13N (EPSG:26913).
- **Vintage used for the published numbers:** **2026-06-15.** The notebook validates against the
  numbers for this vintage; a different download will produce different (newer) counts — that is
  expected, not an error.

> **Location-quality warning.** A majority of POD coordinates are PLSS legal-description **centroids**,
> not field GPS — accurate to the ~40–160 acre PLSS cell, not to the well, and many distinct wells
> **stack** on one coordinate. Do not use raw POD coordinates for parcel-level analysis. The notebook
> only tests point-in-boundary and explicitly handles boundary-ambiguous PLSS stacks.

### 2. MRGCD jurisdictional boundary (`MRGCD-Jurisdictional-Boundary.zip`)

The Middle Rio Grande Conservancy District jurisdictional area (6 polygons, Cochiti to below
Socorro). A **static** layer (geometry dated 2008-02-07); treat as fixed.

- **Source:** MRGCD Mapping & GIS — <https://www.mrgcd.com/mapping-gis/> (Data Viewer at
  <https://maps.mrgcd.com>; records not in the viewer can be requested from `mapping@mrgcd.us`).
- **CRS:** NAD83(HARN) / New Mexico Central (ftUS). The notebook reprojects it to the POD CRS.

### 3. ABCWUA service-area boundary (`ABCWUAServiceArea.zip`)

The Albuquerque Bernalillo County Water Utility Authority drinking-water service area. This is the
**OSE** representation, isolated from the statewide "New Mexico Public Water System Boundaries" layer
(the record where `PublicSyst = "Albuquerque Bernalillo County Water Utility Authority"`,
`Water_Syst = NM3510701`).

- **Download the statewide layer, then extract the ABCWUA record:** NM OSE PWS boundaries —
  <https://geospatialdata-ose.opendata.arcgis.com/datasets/new-mexico-public-water-system-boundaries>
- **CRS:** NAD83 / New Mexico State Plane Central (ftUS), EPSG:2903. The notebook reprojects it.

> **⚠️ The ABCWUA boundary is provisional.** The OSE PWS polygon (used here) and ABCWUA's own
> "Know Your Zone" map (<https://www.abcwua.org/?da_image=know-your-zone-map-2>) disagree by roughly
> **~1,200 domestic rights**. The published analysis uses the OSE polygon as the more **conservative**
> footprint (8,557 rights vs. ~9,738) and flags the ABCWUA count as provisional. Treat it as such.

---

## Directory layout

```
data/domestic_wells/
  input/
    source_shapefiles/      <- put the three .zip files here (git-ignored)
    working_unzipped/        <- notebook extracts here (git-ignored)
  output/                    <- regenerated CSVs + chart PNG (git-ignored)
```

The notebook is the source of truth for the counting method; see
`docs/domestic_wells/README.md` for the methodology summary.

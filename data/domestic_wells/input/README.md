# Domestic Wells — input data

Place the three downloaded source archives in `source_shapefiles/`:

- `OSE_PODs.zip`
- `MRGCD-Jurisdictional-Boundary.zip`
- `ABCWUAServiceArea.zip`

See `../README.md` for exactly where to download each one, the expected shapefile name inside each
zip, and the coordinate systems.

The notebook extracts these into `working_unzipped/` on first run. Both `source_shapefiles/` and
`working_unzipped/` are git-ignored — nothing here is redistributed with the repository.

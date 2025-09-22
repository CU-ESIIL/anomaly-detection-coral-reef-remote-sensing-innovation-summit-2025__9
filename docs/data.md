# Data & Access Plan

This page tracks the datasets feeding the anomaly detection workflow and how to retrieve them. Update it as you ingest new sources or publish derived products.

## Live remote sensing feeds
- **NOAA Coral Reef Watch (5 km)** — Daily SST anomaly, Degree Heating Week, and Bleaching Alert levels. Download via [FTP/HTTP](https://coralreefwatch.noaa.gov/product/5km/) or tap into the ERDDAP API for scripting.
- **Sentinel-2 Level-2A Surface Reflectance (10 m)** — Acquire via [Copernicus Open Access Hub](https://scihub.copernicus.eu/) or the [Microsoft Planetary Computer STAC API](https://planetarycomputer.microsoft.com/dataset/sentinel-2-l2a). Apply cloud masking and sunglint correction before analysis.
- **Harmonized Landsat-Sentinel (HLS)** — Use as a fallback when Sentinel-2 gaps occur. Access through the [NASA LP DAAC CMR API](https://cmr.earthdata.nasa.gov/search/site/docs/search/api.html).

## Reference layers & validation
- **Allen Coral Atlas benthic habitat classifications** ([download portal](https://allencoralatlas.org/)).
- **In-situ survey records** (e.g., NOAA National Coral Reef Monitoring Program) — request via partners, track permissions.
- **Marine protected area boundaries** from [UNEP-WCMC](https://www.protectedplanet.net/en/thematic-areas/marine-protected-areas).

## Processed assets & storage
- Stage intermediate rasters, parquet tables, and exports in the [Group 9 CyVerse folder](https://de.cyverse.org/data/ds/iplant/home/shared/esiil/Innovation_summit/Group_9?type=folder&resourceId=96910606-959e-11f0-b0fb-90e2ba675364).
- Mirror lightweight extracts needed for the website inside `docs/assets/data_snippets/` so figures and tables stay reproducible.
- Record provenance (data source, processing notebook, commit hash) in [`documentation/group-notes.md`](https://github.com/CU-ESIIL/anomaly-detection-coral-reef-remote-sensing-innovation-summit-2025__9/blob/main/documentation/group-notes.md).

## Data management checklist
- [ ] Confirm each dataset’s license allows sharing results publicly.
- [ ] Document spatial/temporal coverage and resolution in this table.
- [ ] Note preprocessing steps (cloud masking, corrections) alongside the scripts that implement them.
- [ ] Flag sensitive or restricted datasets so they are not accidentally published.

Add tables or sections below for specific reef sites, validation surveys, or derivative products as they come online.

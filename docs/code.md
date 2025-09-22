# Code Catalog

Document each script or notebook that supports the coral reef anomaly detection workflow. Include inputs, how to run it, and where to find outputs so teammates and visitors can reproduce results quickly.

## Pipeline overview
1. **Ingest & preprocess** — download Sentinel-2/HLS imagery, apply cloud and sunglint masks, resample to reef polygons.
2. **Thermal context** — pull NOAA Coral Reef Watch HotSpot and Degree Heating Week alerts for the focus region.
3. **Anomaly scoring** — compute rolling baselines, z-scores, or clustering-based anomalies across optical and thermal indicators.
4. **Visualization** — publish static figures, GIFs, and interactive maps summarizing detected hotspots.

## Scripts & notebooks
| Name | Description | Inputs | How to run | Outputs |
|------|-------------|--------|------------|---------|
| `notebooks/01_download_crw.ipynb` | Fetches NOAA Coral Reef Watch tiles for selected reefs. | Reef ID list | Launch in JupyterLab, run all cells. | `data/crw/*.nc` |
| `code/s2_preprocess.py` | Downloads Sentinel-2 L2A scenes, masks clouds, computes reflectance composites. | STAC item list | `python code/s2_preprocess.py --stac docs/assets/stac_query.json` | `data/sentinel2/clean/*.tif` |
| `code/anomaly_index.py` | Calculates spectral + thermal anomaly indices and saves GeoTIFF and parquet tables. | Clean reflectance rasters, CRW anomalies | `python code/anomaly_index.py --config configs/lizard_island.yaml` | `outputs/anomaly/*.tif`, `outputs/anomaly/*.parquet` |
| `notebooks/04_visualize.ipynb` | Generates overview plots, GIFs, and map tiles. | Outputs from anomaly index | Run interactively, export figures via provided cells. | `docs/assets/results/*.png` |

Update the table as you add new analyses. Link to GitHub permalinks if files move or change names.

## Testing & reproducibility
- Keep environment requirements in `requirements.txt` or separate `environment.yml` if needed.
- Include short docstrings or README snippets inside code folders describing parameters, dependencies, and runtime expectations.
- When possible, cache intermediate outputs in the [Group 9 CyVerse folder](https://de.cyverse.org/data/ds/iplant/home/shared/esiil/Innovation_summit/Group_9/) with a matching subdirectory structure.

## Open tasks
- [ ] Add automated data download script for nightly CRW ingest.
- [ ] Prototype bleaching probability model using historical survey data.
- [ ] Publish interactive map tiles to GitHub Pages or an external dashboard.

# Urban Sprawl Analysis (geoskill-urban-sprawl-analysis)

> Quantify sprawl morphology metrics from multi-temporal urban boundaries: compactness, fractal dimension, centroid shift and expansion area rate

---

## 1. Overview

Quantifies the morphology and spatiotemporal dynamics of urban sprawl from multi-temporal urban boundaries (binary rasters, 1 = built-up area): compactness (circularity 4πA/P²), fractal dimension (perimeter–area relation D = 2·ln(P/4)/ln(A)), built-up centroid coordinates and centroid displacement between adjacent periods (km), new/net added area (km²) and growth rate. Typical applications: urban expansion monitoring, sprawl morphology assessment, and compact-city indicator accounting for planning. Synthetic mode generates a sequence of urban patches that expand outward and drift eastward period by period, allowing both expected outcomes — "net expansion detected" and "centroid shifted east" — to be verified. Multi-period boundaries are vectorized with geopandas/shapely into a GeoJSON with year attributes, convenient for mapping and downstream spatial analysis.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-urban-sprawl-analysis.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `sprawl_metrics.json` | JSON | Per-period morphology metrics + inter-period changes + summary |
| `centroid_trajectory.json` | JSON | Centroid trajectory and total displacement |
| `urban_footprint.geojson` | GeoJSON | Multi-period urban boundary polygons (with years) |
| `output-manifest.json` | JSON | Run manifest |

## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)

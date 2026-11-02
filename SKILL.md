---
name: geoskill-urban-sprawl-analysis
description: '多期城市边界量化蔓延形态指标：紧凑度、分形维数、重心迁移与扩张面积速率'
---

# 城市蔓延分析 | Urban Sprawl Analysis

Quantifies the morphology and spatiotemporal dynamics of urban sprawl from multi-epoch urban boundaries (binary rasters, 1=built-up): compactness (circularity 4πA/P²), fractal dimension (perimeter–area relationship D=2·ln(P/4)/ln(A)), built-up centroid coordinates and centroid displacement between adjacent epochs (km), new/net added area (km²), and growth rate.

Typical applications: urban expansion monitoring, sprawl morphology assessment, and compact city indicator accounting in planning. The synthetic mode generates a sequence of urban patches that expand outward and drift eastward epoch by epoch, simultaneously validating two expectations: "net expansion detected" and "centroid shifts eastward". Multi-epoch boundaries are vectorized with geopandas/shapely into a GeoJSON with year attributes, facilitating mapping and downstream spatial analysis.

## Dependencies / 依赖

```bash
pip install 'numpy' 'rasterio' 'scipy' 'geopandas' 'shapely'
```

## Usage / 使用方法

### Basic Usage

```bash
python geoskill-urban-sprawl-analysis.py --bbox 116.0 39.0 117.0 40.0 --n-dates 4
```

### Example 1 (Synthetic Data, Offline)

```bash
python geoskill-urban-sprawl-analysis.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (Reading Multi-Epoch Binary Rasters, One Epoch per Band)

```bash
python geoskill-urban-sprawl-analysis.py --input urban_multidate.tif --output-dir ./out
```

### Example 3 (Custom Year Interval)

```bash
python geoskill-urban-sprawl-analysis.py --bbox 121 31 122 32 --synthetic --start-year 2005 --interval-years 5 --output-dir ./out
```

### Example 4 (3 Epochs + Silent Mode)

```bash
python geoskill-urban-sprawl-analysis.py --bbox 116 39 117 40 --synthetic --n-dates 3 --quiet --output-dir ./out
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `sprawl_metrics.json` | JSON | Per-epoch morphological metrics + changes between adjacent epochs + summary |
| `centroid_trajectory.json` | JSON | Centroid trajectory and total displacement |
| `urban_footprint.geojson` | GeoJSON | Multi-epoch urban boundary polygons (with year) |
| `output-manifest.json` | JSON | Run manifest |

## Data Source / 数据源 / Source

- Local multi-band binary GeoTIFF (one epoch per band, 1=built-up);
- `--synthetic` generates an offline expansion sequence (no network, no account required).

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; user data is never uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。

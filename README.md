# Capstone Project: Public Transport Analysis in Yerevan

This project analyzes public transportation accessibility and route usage in Yerevan using data scraping, spatial analysis, and real-world GPS validation data. All visual outputs in the final report (maps, graphs, etc.) are generated from these scripts and results.

---

## 📁 Structure Overview

```
Capstone/
├── Codes/                # All Python notebooks
├── Data/                 # Outputs and scraped data
```

---

## 🧠 Code-to-Findings Map

### 1. `data_gathering.ipynb`
- **Purpose:** Scrapes stops, items, and routes from Yandex Maps
- **Output files:**
  - `Data/yandex_scraped/full_items.json`
  - `Data/yandex_scraped/full_stops.geojson`
  - `Data/yandex_scraped/full_routes.geojson`

---

### 2. `yerevan_data.ipynb`
- **Purpose:** Downloads boundary, building, and walk network of Yerevan using OSMnx
- **Output files:**
  - `Data/source/yerevan_boundary.gpkg`
  - `Data/source/yerevan_buildings.gpkg`
  - `Data/source/yerevan_walk.gpkg`

---

### 3. `stop_isochrones.ipynb`
- **Purpose:** Generates walking accessibility (isochrone) maps for each public stop
- **Output files:**
  - `Data/isochrones/isochrones_5min.geojson`, ..., `isochrones_15min.geojson`
  - Unioned versions: `isochrones_10min_union.geojson`, etc.

---

### 4. `stops_routes_analysis.ipynb`
- **Purpose:** Analyzes how often each stop pair is used
- **Output file:**
  - `Data/routes_stops/full_routes_line_count.geojson`

---

### 5. `line_29_analysis.ipynb`
- **Purpose:** Analyzes GPS data and ticket validation counts for Line 29
- **Output files:**
  - `Data/line_29/auth_loc_with_dir.geojson`
  - `Data/line_29/line29_auth_count.geojson`
  - `Data/line_29/auth_loc_with_dir.csv`
  - `Data/line_29/line29_auth_count.xlsx`

---

## 📍 Visualizations in Paper

All isochrone layers, route intensity maps, and GPS authentication patterns are **visualized in QGIS** using the files above. These figures are directly shown in the Results section of the final report.

---

## ⚠️ Reproducibility Notes

- Code is written in Python (tested on Google Colab)
- All file paths are defined relative to the `Data/` folder using `base_dir` and `os.path.join(...)`
- No hardcoded paths are used — portable across local Jupyter and Colab

### ✅ Example path logic:
```python
import os
if os.path.exists('/content/drive/My Drive/Capstone/Data'):
    base_dir = '/content/drive/My Drive/Capstone/Data'
else:
    base_dir = os.path.join('..', 'Data')  # fallback for local

file_path = os.path.join(base_dir, 'yandex_scraped/full_stops.geojson')
```

---

## 🔧 Environment Setup

Install all dependencies at once:

```bash
pip install -r requirements.txt
```

Or manually install these packages:
- pandas
- geopandas
- shapely
- osmnx
- networkx
- matplotlib
- numpy
- openpyxl
- fiona
- pyproj

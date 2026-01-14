"# Global Cities Scoring"



\# GlobalCitiesScoring



A reproducible spatial analysis framework to quantify infrastructure accessibility and equity across global cities, using building-level geospatial data and facility proximity metrics. This repository contains the full dataset, processing notebooks, and output scores used in the analysis.



---



\## 1. System Requirements



\### ✅ Operating Systems:

\- Windows 10 / 11 (recommended)

\- macOS Monterey / Ventura

\- Ubuntu 20.04+



\### ✅ Software Dependencies:

\- Python ≥ 3.9

\- Jupyter Notebook ≥ 6.5

\- Pandas ≥ 1.4.2

\- NumPy ≥ 1.22

\- GeoPandas ≥ 0.12

\- Matplotlib / Seaborn

\- QGIS ≥ 3.28 (for `.qgz` project visualization)



\### ✅ Optional:

\- Git Large File Storage (Git LFS) if cloning full dataset

\- `pyshp`, `shapely`, `fiona` for shapefile support



\### ✅ Hardware:

\- Minimum 8GB RAM

\- SSD recommended for handling large CSVs (up to 2GB)

\- No GPU required



---



\## 2. Installation Guide



\### ⏳ Setup Time:

~10–15 mins on a standard desktop



\### 🔧 Setup Instructions



```bash

\# Clone repo (without LFS files >2GB)

git clone https://github.com/apoorva-0210/GlobalCitiesScoring.git

cd GlobalCitiesScoring



\# Create virtual environment

python -m venv env

env\\Scripts\\activate       # Windows

\# or

source env/bin/activate    # Mac/Linux



\# Install requirements

pip install -r requirements.txt
pip install pandas geopandas numpy matplotlib jupyterlab seaborn



3. Demo
#Run Sample Notebook
cd analysis/notebooks
jupyter notebook Analysis.ipynb

 Output:
City-wise accessibility score plots

Gini coefficient radar graphs

SDG alignment charts

Runtime:
~2–4 minutes per city on a standard machine

Full Analysis.ipynb: ~10 minutes for all summaries

4. Instructions for Use
To Run on Your Own City Data
Prepare input files:

Buildings.csv (with lat/lon of each building)

FacilityType.csv (with location and type: hospital, school, etc.)

Place in a new folder under data/{YourCity}/

Create a new notebook or copy from analysis/notebooks/Template.ipynb

Run the jupyter notebook for that city

 

5. To Reproduce Figures
All plots in the paper can be reproduced via:

analysis/notebooks/Analysis.ipynb

analysis/results/*.csv (already computed results)

All visualization PNGs included under analysis/results/


____________________________________________________________________________________________________________________________________________________________________

4) Pseudocode / workflow (paste into README or Supplementary Methods)
Workflow / Pseudocode (Building-level accessibility scoring pipeline)

Inputs

City boundary polygon (AOI)

OpenStreetMap (OSM) features: buildings, road network, facilities for 10 categories
(Civic, Fire, Government, Hospital, Public Services, School, Sports, Supermarket, Toilet, Transport)

Distance thresholds: T = {1 km, 5 km, 10 km} (or thresholds used in the manuscript)

Outputs

For each building: nearest-facility distance per category (network distance)

For each building: accessibility score per category

Aggregated city summaries and derived plots/maps

Pseudocode

Data Extraction (OSM)

For each city AOI:

Query OSM for building=* geometries within AOI → Buildings

Query OSM for facility features using category-specific tags → Facilities[category]

Obtain road network (drivable/walkable as defined) within AOI → RoadNetwork

Preprocessing

Clean geometries:

Remove invalid geometries and duplicates from buildings/facilities

Clip all layers to AOI boundary

Convert buildings to analysis points:

Compute centroid for each building polygon → BuildingPoints

Standardize coordinate reference system (CRS) for all layers

Prepare routing graph:

Convert RoadNetwork into graph G where nodes = intersections and edges = road segments with length weights

Network Distance Computation

For each building point b in BuildingPoints:

Find nearest graph node nb in G

For each facility category c:

Identify candidate facility nodes Nc (nearest graph nodes to facilities in category c)

Compute shortest path distance:

d(b,c) = min_{n in Nc} shortest_path_length(G, nb, n, weight="length")

Store d(b,c) in output table

Distance-to-Score Conversion (per category)

For each building b and category c:

Convert d(b,c) to a normalized score using thresholds:

If d ≤ 1 km → score = 1.0

Else if 1 < d ≤ 5 km → score = 0.5

Else if 5 < d ≤ 10 km → score = 0.25

Else → score = 0.0

Store score(b,c)

(Replace the scoring values with your exact scheme if different.)

Aggregation

For each building b:

Compute overall accessibility score:

Score_total(b) = aggregate_c score(b,c)
(e.g., mean / weighted mean across categories)

For each city:

Summarize distribution of Score_total(b) (mean, median, quantiles)

Create derived layers/maps (optional):

City-wide accessibility heatmaps / clustering / KDE inputs

Export Results

Save:

Per-building distance matrix (CSV/GeoPackage)

Per-building score tables

City-level summary tables used in the manuscript figures/tables








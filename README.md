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









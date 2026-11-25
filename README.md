# GeoTwin Lusaka: Building Intelligence & Urban Spatial Analytics

An integrated geospatial project combining building-density and height data, neighbourhood-level spatial analysis, PostgreSQL/PostGIS, and interactive 3D-ready visualization to explore Lusaka, Zambia.

## Live Project

**[Open the Interactive GeoTwin Lusaka Visualization](https://qureshi-kinza.github.io/Lusaka-UrbanTwin/GeoTwin_Lusaka_3D_Visualization.html)**

## Project Overview

GeoTwin Lusaka explores the spatial distribution and intensity of the built environment across Lusaka using building-density and estimated-height information.

The project develops a geospatial workflow that transforms building-level raster information into neighbourhood-scale indicators, identifies spatial clusters of urban intensity, and presents the results through an interactive visualization.

The workflow integrates remote sensing, GIS, spatial statistics, database management, and web-based visualization.

## Key Objectives

- Examine the spatial distribution of building density and estimated building height.
- Develop a composite Vertical Urban Intensity (VUI) indicator.
- Classify building morphology using density and height thresholds.
- Aggregate building intensity into neighbourhood-scale spatial units.
- Identify statistically significant hotspots and coldspots.
- Store and manage spatial outputs using PostgreSQL/PostGIS.
- Present spatial patterns through an interactive 3D-ready visualization.

## Data Sources

**Microsoft Building Density and Height Dataset — 2025 Q2**

The project uses a Cloud Optimized GeoTIFF covering the Lusaka study area.

- Building density: Band 1
- Estimated building height: Band 2, converted to metres by multiplying the normalized values by 100, as implemented in the notebook.
- Spatial processing: Python, Rasterio, GeoPandas, and related geospatial libraries.

The source raster is downloaded by the Google Colab notebook and is not included in this repository because of its file size.

## Methodology

### 1. Building Morphology Analysis

Building density and estimated height are combined to classify the built environment into four morphology categories:

- Dense-Lower
- Dense-Taller
- Sparse-Lower
- Sparse-Taller

The classification uses the median building-density threshold and the 90th-percentile height threshold.

### 2. Vertical Urban Intensity

A composite indicator is calculated:

**VUI = Building Density × Estimated Building Height**

VUI provides a relative measure of vertical urban intensity by combining the two building attributes.

### 3. Neighbourhood-Level Analysis

Building intensity is aggregated into a regular neighbourhood grid. The resulting units are classified into five intensity groups:

- Very Low
- Low
- Moderate
- High
- Very High

### 4. Spatial Hotspot Analysis

Spatial clustering is examined using Getis-Ord Gi* analysis with Queen contiguity spatial weights, 999 permutations, and Benjamini–Hochberg false-discovery-rate correction.

This identifies statistically significant high-value clusters, low-value clusters, and non-significant locations.

### 5. PostGIS Integration

Spatial datasets and analytical outputs are organized in PostgreSQL/PostGIS, including:

- Building intensity grid
- Neighbourhood intensity
- Hotspot analysis results

### 6. Interactive Visualization

An interactive web visualization presents building morphology, neighbourhood intensity, and VUI hotspot patterns in a 3D-ready grid-based environment.

## Key Results

| Indicator | Result |
|---|---:|
| Building-intensity grid cells | 378,847 |
| Neighbourhood units | 2,020 |
| Locations included in hotspot analysis | 2,019 |
| Significant hotspots | 154 |
| Significant coldspots | 304 |
| Non-significant locations | 1,561 |
| Spatial permutations | 999 |

Key finding: 152 of the 154 significant hotspots (98.7%) occur within the Very High neighbourhood-intensity category, demonstrating a strong spatial concentration of high VUI values.

## Project Visualizations

### 1. Building Morphology
![Lusaka Building Morphology](visualizations/Lusaka_Building_Morphology_Map.png)

### 2. Neighbourhood Building Intensity
![Lusaka Neighbourhood Building Intensity](visualizations/Lusaka_Neighbourhood_Building_Intensity.png)

### 3. Vertical Urban Intensity Hotspots
![Lusaka VUI Hotspot Analysis](visualizations/Lusaka_VUI_Hotspot_Map.png)

### 4. Integrated Spatial Analysis
![GeoTwin Lusaka Integrated Maps](visualizations/GeoTwin_Lusaka_Three_Maps.png)

## Project Data & Outputs

- **GeoPackages:** Neighbourhood intensity and VUI hotspot spatial datasets are available in the `data/` folder.
- **Statistical Results:** Five CSV files containing morphology, neighbourhood intensity, hotspot, and cross-tabulation statistics are available in the `results/` folder.
- **Google Colab Notebook:** The complete processing workflow is available in `GeoTwin_Lusaka_Zambia.ipynb`.

## Technology Stack

- **GIS & Remote Sensing:** Rasterio, GeoPandas, Shapely
- **Spatial Database:** PostgreSQL, PostGIS, SQLAlchemy
- **Spatial Statistics:** PySAL / ESDA, spatial weights, Local Moran's I
- **Data Analysis:** Python, NumPy, Pandas
- **Visualization:** Matplotlib, Plotly, HTML, JavaScript
- **Environment:** Google Colab, GitHub Pages

## Reproducibility

1. Open `GeoTwin_Lusaka_Zambia.ipynb` in Google Colab.
2. Connect Google Drive when prompted.
3. Run the notebook cells in sequence.
4. The notebook downloads the source raster and performs the geospatial processing.
5. Spatial datasets, statistical outputs, and visualization files are generated in the project output directory.

PostgreSQL/PostGIS setup is included in the notebook workflow.

## Important Limitations

- VUI is a relative intensity proxy, not a direct measurement of building volume, population density, or floor area.
- The interactive 3D-ready visualization represents sampled grid cells; it does not reconstruct individual buildings.
- Neighbourhood aggregation uses a projected coordinate system (EPSG:3857), so grid dimensions should be interpreted as approximate ground distances rather than exact local measurements.
- Hotspot results depend on the spatial weights definition, neighbourhood structure, and statistical significance correction.
- Results represent the source dataset's 2025 Q2 coverage and attributes.

## Author

**Qureshi Kinza **  
---

*GeoTwin Lusaka demonstrates an integrated geospatial workflow for building intelligence, neighbourhood-scale spatial analytics, and interactive urban visualization.*

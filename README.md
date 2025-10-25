# URBAN PLUVIAL FLOOD RISK EDA

## FOCUS AND SCOPE
**Type of Flooding**: Pluvial (Surface Water) Flooding, which occurs when excessive rainfall overwhelms the drainage system or cannot be absorbed, leading to water pooling on the ground.

**Scale**: Global, covering 91 administrative wards and 63 cities.

**Granularity**: Fine-grained, with 2,963 individual records, where each record corresponds to a specific road or area segment.

**Core features are:**

* Geospatial information: catchment ID, city, ward, latitude, and longitude

* Topography and environment: land use, soil group, elevation (m), and DEM source

* Infrastructure and hydrology: storm drain type, density, and closeness

* Historical rainfall intensity (mm/hr), rainfall source, and return period are examples of climate data.

* Risk assessment: Each segment's flood risk labels

## DATA PREPARATION

### 1. Data Loading & Initial Inspection
*   Loaded the dataset using Pandas.
*   Performed initial inspection using `.head()`, `.info()`, and `.isnull().sum()` to understand the data structure and identify missing values.

### 2. Data Cleaning & Manipulation
Filling null values to ensure data validity and output accuracy:
*   **Numerical Features:** Filled nulls with the median value.
    *   `elevation_m` → 25.13
    *   `drainage_density_km_per_km2` → 6.25
    *   `storm_drain_proximity_m` → 91.7
*   **Categorical Features:** Filled nulls with the mode (most frequent value).
    *   `soil_group` → 'B'
    *   `storm_drain_type` → 'CurbInlet'
    *   `rainfall_source` → 'ERA5'

**Decomposed `risk_labels`:**
  1. Extracted `event_date` from strings like `event_2025-05-02`.
  2. Cleaned the remaining labels and performed **one-hot encoding** to create binary columns for each risk type:
        *   `extreme_rain_history`
        *   `low_lying`
        *   `ponding_hotspot`
        *   `sparse_drainage`
        *   `monitor` (indicates low-risk segments for monitoring)
  3. Split `city_name`:
        * Separate `city` and `country` columns for more granular geographical analysis.
4.  Created Target Variable `is_risky`:
    *   A binary column where `1` indicates a segment has at least one of the active risk labels (`ponding_hotspot`, `low_lying`, `sparse_drainage`, `extreme_rain_history`), and `0` indicates it is only labeled for `monitor`.

## DATA ANALYSIS
*   Used matplotlib.pylot and seaborn for data visualization.
*   Calculated the total number of segments and risk categories.
*   Analyzed the distribution of segments across the four main risk labels, providing a high-level view of the most common flood risk factors in the dataset.
  
### FOCUS
* Focused on the factors that contributes the most in flood risk.
* **TOP CONTRIBUTORS ARE**: low elevation, drainage proximity accompanied by rainfall intensity, and hotspots (regions that geographically prone to heavy rains (tropical areas))

## RECOMMENDATIONS
* Prioritize Low-Elevation Hotspots for Mitigation
* Upgrade Drainage Infrastructure & Reduce Distance to Storm Drains
* Enable data-driven planning & community

## TECHNOLOGIES USED
*   **Python**
*   **Pandas** (Data Load, Cleaning, & Manipulation)
*   **NumPy** (Numerical Operations)
*   **Matplotlib** / **Seaborn** (Visualization - implied by import)
*   **Jupyter Notebook** (Environment)

## AUTHOR FT. DISCLAIMER
**KARYLL MAE O. SANIEL**
*por academic purposed onleh wews* 

# CESM Terrain and Snow Analysis

A comprehensive analysis of CESM (Community Earth System Model) terrain representation accuracy, comparing model elevation predictions with actual elevations for major mountain cities and passes across the western United States at multiple grid resolutions.

## Overview

This repository contains Jupyter notebooks that analyze how CESM grid resolution affects elevation representation at specific locations, highlighting the trade-offs between model resolution and computational cost for terrain-dependent climate studies.

### Key Features

- **Multi-resolution comparison**: Analyzes three CESM resolutions (coarse ~1.9°×2.5°, medium ~0.9°×1.25°, fine ~0.47°×0.63°)
- **Mountain city analysis**: Evaluates elevation accuracy for 21 major mountain cities
- **Mountain pass analysis**: Analyzes elevation representation at 12 critical mountain passes with SNOTEL stations
- **Statistical evaluation**: Provides comprehensive error metrics (MAE, RMSE, Bias, Max Error) for each resolution
- **Visualization**: Creates publication-quality maps and comparison tables

## Repository Structure

```
CESM_terrain_snow/
├── README.md                              # This file
├── LICENSE                                # MIT License
├── requirements.txt                       # Python dependencies
├── .gitignore                            # Git ignore rules
├── mountain_city_elevation_comparison.ipynb  # Main analysis notebook
├── us_terrain_plot.ipynb                 # US terrain visualization
├── terrain_plot.ipynb                    # North America terrain visualization
└── [CESM data files]                     # Not included (see Data Requirements)
```

## Getting Started

### Prerequisites

- Python 3.7 or higher
- Jupyter Notebook or JupyterLab
- Access to CESM topography files (see Data Requirements below)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Austfi/CESM_terrain_snow.git
   cd CESM_terrain_snow
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Obtain CESM data files**
   - Download the three required CESM topography NetCDF files using the curl commands provided in the [Data Requirements](#-data-requirements) section below
   - Place them in the same directory as the notebooks

5. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

## Notebooks

### 1. Mountain City and Pass Elevation Comparison

**File**: `mountain_city_elevation_comparison.ipynb`

This is the main analysis notebook that:
- Compares CESM model elevations with actual elevations for 33 locations
- Generates statistical summaries for each resolution
- Creates comprehensive visualizations including:
  - Geographic map showing location points colored by elevation error
  - Statistical summary table
  - Detailed comparison table with color-coded differences

**Locations Analyzed**:
- **Cities (21)**: Denver, Salt Lake City, Aspen, Telluride, Steamboat Springs, Vail, Breckenridge, Park City, Alta, Jackson, Bozeman, Taos, Bend, Mount Hood Village, Leavenworth, Winthrop, Sun Valley, Mammoth Lakes, Truckee, South Lake Tahoe, Big Bear Lake
- **Mountain Passes (12)**: Loveland Pass, Berthoud Pass, Monarch Pass, Vail Pass, Cameron Pass, Rabbit Ears Pass, Monument Pass, Snoqualmie Pass, Stevens Pass, White Pass, Donner Pass, Carson Pass

### 2. US Terrain Plot

**File**: `us_terrain_plot.ipynb`

Visualizes CESM terrain elevation over the United States at three different resolutions side-by-side for comparison.

### 3. Terrain Plot

**File**: `terrain_plot.ipynb`

Similar to US Terrain Plot but covers the entire North America region.

## Data Requirements

### CESM Topography Files

This repository requires three CESM topography NetCDF files (not included due to size limitations):

1. **Coarse Resolution**: `fv_1.9x2.5_nc3000_Nsw084_Nrs016_Co120_Fi001_ZR_GRNL_031819.nc`
2. **Medium Resolution**: `fv_0.9x1.25_nc3000_Nsw042_Nrs008_Co060_Fi001_ZR_160505.nc`
3. **Fine Resolution**: `fv_0.47x0.63_nc3000_Co030_Fi001_PF_nullRR_Nsw021_20171023.nc`

**Download Instructions**:

These files can be downloaded directly from the CESM input data repository using the following commands:

```bash
# Coarse resolution (~1.9°×2.5°)
curl -O https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/atm/cam/topo/fv_1.9x2.5_nc3000_Nsw084_Nrs016_Co120_Fi001_ZR_GRNL_031819.nc

# Medium resolution (~0.9°×1.25°)
curl -O https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/atm/cam/topo/fv_0.9x1.25_nc3000_Nsw042_Nrs008_Co060_Fi001_ZR_160505.nc

# Fine resolution (~0.47°×0.63°)
curl -O https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/atm/cam/topo/fv_0.47x0.63_nc3000_Co030_Fi001_PF_nullRR_Nsw021_20171023.nc
```

**Note**: These files are large (>50MB, with the fine resolution file being ~390MB) and exceed GitHub's file size limits. Ensure you have sufficient disk space and a stable internet connection for downloading.

### Elevation Data Sources

Real-world elevation data used in this analysis is verified from:
- USGS National Elevation Dataset (NED)
- NOAA National Weather Service
- State Department of Transportation records
- Official city/municipal records
- SNOTEL station metadata (NRCS)

## Understanding Geopotential vs. Geometric Elevation

When working with CESM data, you'll notice that elevation is stored as **geopotential** (PHIS) rather than geometric height in meters. This section explains why and how we convert between these two representations.

### What is Geopotential?

**Geopotential** (denoted as Φ or PHIS in CESM files) represents the gravitational potential energy per unit mass at a given location. It has units of **m²/s²** (meters squared per second squared), which might seem strange at first!

Think of it this way: if you lift a mass from sea level to some height, you're doing work against gravity. Geopotential measures how much work per unit mass would be required to lift an object from sea level to that point. The higher you go, the more geopotential energy you have.

### Why Does CESM Use Geopotential?

Climate models like CESM use geopotential instead of geometric height for several important reasons:

1. **Physical accuracy**: Geopotential accounts for Earth's shape and gravity variations. Since Earth isn't a perfect sphere and gravity varies with latitude and elevation, geopotential provides a more physically meaningful measure for atmospheric dynamics.

2. **Model convenience**: Atmospheric models solve equations that directly involve geopotential. Gravity appears naturally in these equations, making geopotential the "natural" variable for the model's physics.

3. **Coordinate system**: CESM uses a pressure-based coordinate system where geopotential surfaces (surfaces of constant Φ) are more meaningful than surfaces of constant geometric height.

### Converting Geopotential to Elevation

To convert geopotential (PHIS) to geometric elevation in meters, we use the relationship:

```
Geometric Height = Geopotential / Standard Gravity
```

In mathematical notation:
```
h = Φ / g₀
```

Where:
- **h** = geometric height in meters
- **Φ** (PHIS) = geopotential in m²/s²
- **g₀** = standard gravity = 9.8065 m/s²

### Why Standard Gravity?

You might wonder: "If gravity varies, why use a constant value?"

Using standard gravity (g₀ = 9.8065 m/s²) is an approximation that works well for most purposes. The geopotential itself already accounts for gravity variations—that's built into its definition. By dividing by standard gravity, we're essentially asking: "If gravity were constant everywhere, what height would this geopotential correspond to?"

For visualization and comparison with datasets like SRTM (which use geometric height), this approximation is excellent—the errors are typically less than 1% and often much smaller.

### In Our Code

You'll see this conversion in all our notebooks:

```python
# Convert geopotential (PHIS) to elevation in meters
g0 = 9.8065  # Standard gravity in m/s²
elevation = PHIS / g0
```

This simple division transforms the geopotential values from CESM (which are in m²/s²) into geometric elevation values (in meters) that we can easily visualize and compare with real-world elevation data.

### Key Takeaway

- **CESM stores**: Geopotential (PHIS) in m²/s² - the "natural" variable for atmospheric physics
- **We convert to**: Geometric elevation in meters - the familiar unit for visualization and comparison
- **Conversion method**: Divide by standard gravity (9.8065 m/s²)
- **Result**: Elevation values that can be directly compared with SRTM and other elevation datasets

## Dependencies

See `requirements.txt` for the complete list. Key dependencies include:

- `xarray` - NetCDF data handling
- `netCDF4` - NetCDF file I/O
- `matplotlib` - Plotting and visualization
- `cartopy` - Geographic projections and features
- `numpy` - Numerical operations
- `pandas` - Data manipulation

## Key Findings

The analysis reveals:

- **Resolution matters**: Finer resolutions (F05) generally provide more accurate elevation estimates, with Mean Absolute Error (MAE) decreasing from ~658m (F19) to ~437m (F05)
- **Mountain passes are challenging**: Even the finest resolution struggles with high-elevation passes, with errors exceeding 1000m in some locations
- **Urban centers show better accuracy**: Major cities tend to have smaller elevation errors compared to remote mountain passes
- **Bias patterns**: CESM tends to underestimate elevations in mountainous terrain across all resolutions


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- CESM (Community Earth System Model) development team
- USGS, NOAA, and NRCS for elevation data sources
- The open-source scientific Python community

## Contact

For questions or issues, please open an issue on GitHub or contact the repository maintainer.

## Related Resources

- [CESM Website](https://www.cesm.ucar.edu/)
- [USGS National Elevation Dataset](https://www.usgs.gov/3d-elevation-program)
- [SNOTEL Network](https://www.nrcs.usda.gov/wps/portal/wcc/home/aboutUs/monitoringPrograms/automatedSnowMonitoring/)

---

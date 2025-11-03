# CESM Terrain and Snow Analysis

A comprehensive analysis of CESM (Community Earth System Model) terrain representation accuracy, comparing model elevation predictions with actual elevations for major mountain cities and passes across the western United States at multiple grid resolutions.

## 📋 Overview

This repository contains Jupyter notebooks that analyze how CESM grid resolution affects elevation representation at specific locations, highlighting the trade-offs between model resolution and computational cost for terrain-dependent climate studies.

### Key Features

- **Multi-resolution comparison**: Analyzes three CESM resolutions (coarse ~1.9°×2.5°, medium ~0.9°×1.25°, fine ~0.47°×0.63°)
- **Mountain city analysis**: Evaluates elevation accuracy for 21 major mountain cities
- **Mountain pass analysis**: Analyzes elevation representation at 12 critical mountain passes with SNOTEL stations
- **Statistical evaluation**: Provides comprehensive error metrics (MAE, RMSE, Bias, Max Error) for each resolution
- **Visualization**: Creates publication-quality maps and comparison tables

## 🗂️ Repository Structure

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

## 🚀 Getting Started

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
   - Download the three required CESM topography NetCDF files (see Data Requirements)
   - Place them in the same directory as the notebooks

5. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

## 📊 Notebooks

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

## 📁 Data Requirements

### CESM Topography Files

This repository requires three CESM topography NetCDF files (not included due to size limitations):

1. **Coarse Resolution**: `fv_1.9x2.5_nc3000_Nsw084_Nrs016_Co120_Fi001_ZR_GRNL_031819.nc`
2. **Medium Resolution**: `fv_0.9x1.25_nc3000_Nsw042_Nrs008_Co060_Fi001_ZR_160505.nc`
3. **Fine Resolution**: `fv_0.47x0.63_nc3000_Co030_Fi001_PF_nullRR_Nsw021_20171023.nc`

**Note**: These files are large (>50MB) and exceed GitHub's file size limits. Users must obtain these files separately. Check the CESM project website or contact the CESM Data Management Group for access.

### Elevation Data Sources

Real-world elevation data used in this analysis is verified from:
- USGS National Elevation Dataset (NED)
- NOAA National Weather Service
- State Department of Transportation records
- Official city/municipal records
- SNOTEL station metadata (NRCS)

## 🔧 Dependencies

See `requirements.txt` for the complete list. Key dependencies include:

- `xarray` - NetCDF data handling
- `netCDF4` - NetCDF file I/O
- `matplotlib` - Plotting and visualization
- `cartopy` - Geographic projections and features
- `numpy` - Numerical operations
- `pandas` - Data manipulation

## 📈 Key Findings

The analysis reveals:

- **Resolution matters**: Finer resolutions (F05) generally provide more accurate elevation estimates, with Mean Absolute Error (MAE) decreasing from ~658m (F19) to ~437m (F05)
- **Mountain passes are challenging**: Even the finest resolution struggles with high-elevation passes, with errors exceeding 1000m in some locations
- **Urban centers show better accuracy**: Major cities tend to have smaller elevation errors compared to remote mountain passes
- **Bias patterns**: CESM tends to underestimate elevations in mountainous terrain across all resolutions

## 🤝 Contributing

Contributions are welcome! Please feel free to:
- Report bugs or issues
- Suggest improvements
- Submit pull requests
- Add additional analysis locations

## 📝 Citation

If you use this code or analysis in your research, please cite appropriately:

```bibtex
@software{cesm_terrain_snow,
  title = {CESM Terrain and Snow Analysis},
  author = {Your Name},
  year = {2024},
  url = {https://github.com/Austfi/CESM_terrain_snow}
}
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- CESM (Community Earth System Model) development team
- USGS, NOAA, and NRCS for elevation data sources
- The open-source scientific Python community

## 📧 Contact

For questions or issues, please open an issue on GitHub or contact the repository maintainer.

## 🔗 Related Resources

- [CESM Website](https://www.cesm.ucar.edu/)
- [USGS National Elevation Dataset](https://www.usgs.gov/3d-elevation-program)
- [SNOTEL Network](https://www.nrcs.usda.gov/wps/portal/wcc/home/aboutUs/monitoringPrograms/automatedSnowMonitoring/)

---

**Last Updated**: December 2024


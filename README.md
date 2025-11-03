# CESM Terrain and Snow Analysis

Analysis of CESM terrain representation accuracy comparing model elevation predictions with actual elevations for mountain cities and passes across the western United States at multiple grid resolutions.

## Features

- Multi-resolution comparison: Three CESM resolutions (coarse ~1.9°×2.5°, medium ~0.9°×1.25°, fine ~0.47°×0.63°)
- 21 mountain cities and 12 mountain passes analyzed
- Statistical evaluation: MAE, RMSE, Bias, Max Error
- Publication-quality visualizations

## Getting Started

### Prerequisites

- Python 3.7+
- Jupyter Notebook or JupyterLab

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Austfi/CESM_terrain_snow.git
   cd CESM_terrain_snow
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Download CESM topography files (see [Data Requirements](#data-requirements)) and place them in the repository root.

4. Launch Jupyter:
   ```bash
   jupyter notebook
   ```

## Notebooks

### Mountain City and Pass Elevation Comparison
Main analysis comparing CESM elevations with actual elevations for 33 locations (21 cities, 12 passes). Generates statistical summaries and visualizations.

**Cities**: Denver, Salt Lake City, Aspen, Telluride, Steamboat Springs, Vail, Breckenridge, Park City, Alta, Jackson, Bozeman, Taos, Bend, Mount Hood Village, Leavenworth, Winthrop, Sun Valley, Mammoth Lakes, Truckee, South Lake Tahoe, Big Bear Lake

**Passes**: Loveland Pass, Berthoud Pass, Monarch Pass, Vail Pass, Cameron Pass, Rabbit Ears Pass, Monument Pass, Snoqualmie Pass, Stevens Pass, White Pass, Donner Pass, Carson Pass

### US Terrain Plot
Visualizes CESM terrain elevation over the United States at three resolutions side-by-side.

### Terrain Plot
Same as US Terrain Plot but covers North America.

## Data Requirements

### CESM Topography Files

Three CESM topography NetCDF files are required (not included due to size):

1. Coarse: `fv_1.9x2.5_nc3000_Nsw084_Nrs016_Co120_Fi001_ZR_GRNL_031819.nc`
2. Medium: `fv_0.9x1.25_nc3000_Nsw042_Nrs008_Co060_Fi001_ZR_160505.nc`
3. Fine: `fv_0.47x0.63_nc3000_Co030_Fi001_PF_nullRR_Nsw021_20171023.nc`

Download from CESM input data repository:

```bash
curl -O https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/atm/cam/topo/fv_1.9x2.5_nc3000_Nsw084_Nrs016_Co120_Fi001_ZR_GRNL_031819.nc
curl -O https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/atm/cam/topo/fv_0.9x1.25_nc3000_Nsw042_Nrs008_Co060_Fi001_ZR_160505.nc
curl -O https://svn-ccsm-inputdata.cgd.ucar.edu/trunk/inputdata/atm/cam/topo/fv_0.47x0.63_nc3000_Co030_Fi001_PF_nullRR_Nsw021_20171023.nc
```

**Note**: Files are large (>50MB, fine resolution ~390MB).

### Elevation Data Sources

Real-world elevation data verified from USGS NED, NOAA NWS, state DOT records, city records, and SNOTEL station metadata.

## Understanding Geopotential vs. Geometric Elevation

CESM stores elevation as **geopotential** (PHIS) in m²/s² rather than geometric height in meters. Geopotential represents gravitational potential energy per unit mass and is the natural variable for atmospheric dynamics.

### Conversion

Convert geopotential to geometric elevation:

```
h = Φ / g₀
```

Where:
- **h** = geometric height (meters)
- **Φ** (PHIS) = geopotential (m²/s²)
- **g₀** = standard gravity = 9.8065 m/s²

In code:
```python
g0 = 9.8065  # Standard gravity in m/s²
elevation = PHIS / g0
```

Using standard gravity is an approximation (errors <1%) that works well for visualization and comparison with datasets like SRTM.

## Dependencies

- `xarray` - NetCDF data handling
- `netCDF4` - NetCDF file I/O
- `matplotlib` - Plotting and visualization
- `cartopy` - Geographic projections
- `numpy` - Numerical operations
- `pandas` - Data manipulation

See `requirements.txt` for complete list.

## Key Findings

- Finer resolutions improve accuracy: MAE decreases from ~658m (F19) to ~437m (F05)
- Mountain passes are challenging: errors exceed 1000m even at finest resolution
- Urban centers show better accuracy than remote mountain passes
- CESM tends to underestimate elevations in mountainous terrain

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Related Resources

- [CESM Website](https://www.cesm.ucar.edu/)
- [USGS National Elevation Dataset](https://www.usgs.gov/3d-elevation-program)
- [SNOTEL Network](https://www.nrcs.usda.gov/wps/portal/wcc/home/aboutUs/monitoringPrograms/automatedSnowMonitoring/)

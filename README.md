# Padma River Erosion & Accretion Analysis (2020–2025)

Quantifying riverbank erosion, accretion and in-channel bar change on the lower Padma River near Faridpur, Bangladesh, using Landsat imagery, NDWI and ArcGIS.

## Overview

Rivers like the Padma continuously erode one bank and deposit sediment on the other. This project measures how a reach of the Padma changed between **December 2020** and **2025** by extracting the river boundary from satellite imagery in both years and comparing them.

## Maps

| Accretion | Erosion |
|---|---|
| ![Accretion map](images/accretion_map.jpg) | ![Erosion map](images/erosion_map.jpg) |

## Key Results

| Metric | Area (ha) |
|---|---|
| River area, 2020 | 76,976.35 |
| River area, 2025 | 70,616.61 |
| Unchanged area | 58,249.41 |
| Erosion (land → river) | 12,367.20 |
| Accretion (river → land) | 18,726.94 |
| **Net change in active channel** | **≈ −6,360 (channel shrank)** |

Five in-channel bars were also digitised and compared:

| Bar | 2020 (ha) | 2025 (ha) |
|---|---|---|
| 1 | 102.46 | 218.28 |
| 2 | 48.06 | 27.38 |
| 3 | 17.85 | 7.29 |
| 4 | 43.14 | 19.07 |
| 5 | 9.58 | 21.34 |
| **Total** | **221.08** | **293.36** (+≈73 ha) |

**Finding:** accretion outweighed erosion, so the reach was net depositional. Total bar area grew, driven mainly by Bar 1 (more than doubled) and Bar 5, while Bars 2–4 shrank, which points to local reworking of sediment within the channel.

## Methodology

1. Load Landsat 8 Collection 2 Level-2 surface reflectance scenes (path 138, row 043; the 2020 scene is dated 15 Dec 2020) for 2020 and 2025.
2. Compute **NDWI** = (Green − NIR) / (Green + NIR) with Raster Calculator (bands B3 and B5).
3. Clip to the study area with **Extract by Mask**.
4. **Reclassify** into two classes (water / non-water) and convert the raster to polygons.
5. Export the river polygon for each year (`River2020`, `River2025`) and calculate areas in hectares.
6. **Intersect** the two years to get the unchanged area.
7. Use **Erase** to produce the erosion and accretion layers:
   - Erosion = River 2025 − Unchanged
   - Accretion = River 2020 − Unchanged
8. Manually digitise five bars for each year and compare their areas in Excel.

## Tools

ArcGIS (ArcMap), Landsat 8 OLI imagery (USGS), Microsoft Excel

## Repository Structure

```
├── images/    # Erosion and accretion maps
├── data/      # river_area.xlsx (area calculations)
├── report/    # Full written report (.docx)
└── README.md
```

## Limitations

- Results depend on the NDWI threshold chosen in the 2-class reclassification, and no formal accuracy assessment was done.
- Differences in image acquisition date and river water level between the two years can affect the extracted river boundary.
- Only five bars were sampled, so bar results should not be generalised to the whole reach.

## Author

Kaif Al Shahriar Qais Shurid · Department of Environmental, Water Resources and Coastal Engineering

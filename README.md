# Vertical-Delineation-of-Total-Petroleum-Hydrocarbon-TPH-Soil-Contamination-in-a-Refinery
The primary objective of this project is to create a high-resolution 3D visualization of Total Petroleum Hydrocarbon (TPH) distribution across the refinery site. By categorizing data into five distinct depth intervals, the project aims to:

**Delineate the Plume:** Identify the horizontal and vertical boundaries of soil contamination.

**Identify Source Zones:** Locate the highest concentrations (hot spots) to guide remediation efforts.

**Assess Risk:** Determine if contamination is migrating toward the deep aquifer (46–70 ft range).

**Integrate Historical & Modern Data:** Combine diverse sampling methods into a single, unified site model.

# 2. Data Sources
Historical Site Maps: 1993 and 2004 PDF figures showing Soil Boring (SB) and Monitoring Well (MW) locations.

Analytical Datasets: Excel spreadsheets containing TPH concentration data for CP, SB, and MW locations across multiple depths.

Base Map: SMRC Site Map (MAX RES) used as the spatial anchor for the refinery layout.

Tool: QGIS was used for this project

# 3. Step-by-Step Technical Approach
**Phase I:** Georeferencing & Spatial Alignment
Map Transformation: Imported historical PDF maps (1993/2004) into the QGIS Georeferencer.

Control Points: Assigned Ground Control Points (GCPs) based on permanent refinery structures to align historical figures with the modern coordinate system (EPSG:3310).

Raster Rectification: Warped the historical images to ensure that the Soil Boring locations shown on paper matched their real-world coordinates.

**Phase II:** Vectorization & Feature Creation
Shapefile Generation: Created new Point Shapefiles (Boring_Locations.shp) to digitize the physical locations of CP, SB, and MW points.

Digitization: Manually plotted points over the georeferenced maps, assigning a unique ID (e.g., CP-11, MW-1) to every feature to facilitate data linking.

**Phase III:** Data Integration (The Join)
Database Linking: Performed a Vector Join between the Shapefile attribute table and the cleaned Excel CSV datasets using the ID field as the common key.

One-to-Many Resolution: Because locations have multiple samples at different depths, the data was filtered into five separate layers (0–5ft, 6–15ft, etc.) to ensure each point on the map represented the correct depth-specific TPH value.

Data Type Conversion: Used the QGIS Field Calculator and to_real() functions to convert TPH "String" data into "Decimal/Real" numbers for mathematical processing.

**Phase IV:** Spatial Interpolation & Symbology
IDW Analysis: Conducted Inverse Distance Weighted (IDW) interpolation for each depth interval to create a continuous surface of contamination.

Standardized Symbology:

Color Ramp: Applied a consistent "Green-to-Red" pseudocolor scale across all maps (0 to 35,000 ppm).

Point Markers: Used distinct geometric shapes to identify data sources: Circles (CP), Squares (SB), and Triangles (MW).

ND Handling: Treated "Non-Detect" (ND) results as 0 to act as boundary anchors, preventing the plume from "bleeding" into clean areas.

# 4. Final Output
The final deliverable is a 5-Pane Unified Layout providing a horizontal "x-ray" of the refinery at five depths. This layout allows for immediate visual comparison of plume intensity, showing the core contamination at 6–15 ft and the subsequent attenuation in deeper soil layers.

---
title: "Overview"
weight: 1
menu:
  main:
    parent: "elevation_api"
    weight: 1
---

The Elevation API provides point/line/area elevation lookups and raster tiles for bathymetry visualization and digital elevation models (DEMs).

## Lookup endpoints

Query elevation at coordinates, along lines, or over areas:

- [Look Up Points]({{< relref "lookup-points.md" >}}) — elevation at discrete coordinates
- [Look Up Polylines]({{< relref "lookup-polylines.md" >}}) — elevation sampled along lines
- [Look Up Polygons]({{< relref "lookup-polygons.md" >}}) — elevation sampled over areas

## Tile endpoints

- [S-102 Bathymetry Gradient]({{< relref "s102-bathymetry-gradient.md" >}}) — colorized or depth-encoded S-102 bathymetry for map overlays
- [S-102 Bathymetry DEM]({{< relref "s102-bathymetry-dem.md" >}}) — Terrain-RGB DEM from S-102 depth (seafloor only)
- [Unified DEM]({{< relref "unified-dem.md" >}}) — Terrain-RGB DEM combining basemap elevation with chart bathymetry (land + sea)


## Terrain and altitude references

<!-- TODO: Expand this section -->

*Placeholder.* Details on how elevation values are defined (for example mean sea level), how bathymetric depth relates to seafloor height, and how to interpret Terrain-RGB encoding will be documented here.

## Choosing an endpoint

<!-- TODO: Expand this section -->

*Placeholder.* Guidance on when to use the bathymetry gradient vs. the S-102 DEM vs. the unified DEM will be documented here.

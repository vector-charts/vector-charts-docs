---
title: "Get Shoreline Tile"
weight: 3.1
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/data-shoreline-v1/<z>/<x>/<y>.json?token=<token string>" title="Get GeoJSON Tile" request=`GET https://api.vectorcharts.com/api/v2/tiles/data-shoreline-v1/12/1240/1515.json?token=299ce9bf4f244300a96f3926240f9c0d` response=`{
    "type": "MultiPolygon",
    "coordinates": [
        [
            [
                [
                    -122.388793945,
                    37.790630481
                ],
                [
                    -122.3887009,
                    37.790452
                ],
                ...` %}}

<span style="color:#9e6c2e">Enterprise Plan Only: This endpoint is restricted to enterprise customers.</span>

Returns the shoreline geometry (boundary between "land" and "water" features) for an area defined by the tile X/Y/Z as a GeoJSON document.

The returned GeoJSON will contain one or more polygons (as a `Polygon` or `MultiPolygon`) representing the area inside the tile which consists of land. 

This data is sourced from all ENCs in the area, along with low-resolution background data in areas without ENCs.

At zoom levels below 4, the data will exclusively consist of low-resolution background data.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Z coordinate of tile.
- **x** <span style="color:red;">(Required)</span>: X coordinate of tile.
- **y** <span style="color:red;">(Required)</span>: Y coordinate of tile. 

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.

{{% /apiEndpointCard %}}
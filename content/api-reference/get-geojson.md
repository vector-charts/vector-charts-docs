---
title: "Get GeoJSON Tile"
weight: 3
menu:
  main:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/data-geojson-v1/<z>/<x>/<y>.json?token=<token string>" title="Get GeoJSON Tile" request=`GET https://api.vectorcharts.com/api/v2/tiles/data-geojson-v1/12/1240/1515.json?token=f73f12ed4a4f4b6d878bb305d66deea3` response=`{"type":"FeatureCollection","features":[{"type":"Feature","geometry":{"type":"Point","coordinates":[]},"properties":{"layerId":"LNDARE","attributes":{"agen":550,"fidn":529328420,"fids":5578,"grup":2...` %}}

<span style="color:#9e6c2e">Enterprise Plan Only: This endpoint is restricted to enterprise customers.</span>

Returns the raw nautical chart data for an area defined by the tile X/Y/Z as a GeoJSON document.

The returned data is reconciled and combined: It contains the merged data from all ENCs in the area. Higher-resolution local ENCs cover & clip data from lower-resolution summary ENCs.

<b>Path Parameters</b>

- **z** <span style="color:red;">(Required)</span>: Z coordinate of tile. Must be 12 or higher, because this endpoint restricts the maximum size for a single raw data query.
- **x** <span style="color:red;">(Required)</span>: X coordinate of tile.
- **y** <span style="color:red;">(Required)</span>: Y coordinate of tile. 

<b>Query Parameters</b>

- **token** <span style="color:red;">(Required)</span>: Vector Charts API token.

{{% /apiEndpointCard %}}
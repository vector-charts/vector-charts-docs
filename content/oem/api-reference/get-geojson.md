---
title: "Get GeoJSON Tile"
weight: 5
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/data-geojson-v1/{z}/{x}/{y}.json" title="Get GeoJSON Tile" request=`GET https://<your-host>:9909/api/v2/tiles/data-geojson-v1/12/1240/1515.json
Authorization: Bearer <token>` response=`Status Code: 200 OK
Content-Type: application/json

{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "geometry": {
                "type": "Point",
                "coordinates": [-122.388, 37.790]
            },
            "properties": {
                "layerId": "LNDARE",
                "attributes": { ... }
            }
        },
        ...
    ]
}` %}}

Returns the raw nautical chart data for the given XYZ tile as a GeoJSON `FeatureCollection`. Use this endpoint to consume chart features programmatically (for example, to overlay them in a custom renderer, run spatial queries, or feed them into a navigation app).

The features are reconciled across all ENC cells overlapping the tile: higher-resolution local cells cover and clip data from lower-resolution summary cells. Each feature's `properties` include a `layerId` (the S-57 layer name, such as `LNDARE` or `DEPCNT`) and an `attributes` object with the S-57 attributes for that feature.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Path Parameters</b>

- **z**: Zoom level. Must be `10` or higher to keep the response size bounded.
- **x**: Tile column.
- **y**: Tile row.

<b>Response</b>

On success, returns a GeoJSON `FeatureCollection`. If no chart data overlaps the tile, the endpoint returns `404 Not Found` rather than an empty collection.

<b>Error Responses</b>

- **400 Bad Request**: `z` is below `10`.
- **401 Unauthorized**: The token is missing or not valid.
- **404 Not Found**: No chart data overlaps the requested tile.

{{% /apiEndpointCard %}}

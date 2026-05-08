---
title: "Get Shoreline Tile"
weight: 6
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v2/tiles/data-shoreline-v1/{z}/{x}/{y}.json" title="Get Shoreline Tile" request=`GET https://<your-host>:9909/api/v2/tiles/data-shoreline-v1/12/1240/1515.json
Authorization: Bearer <token>` response=`Status Code: 200 OK
Content-Type: application/json

{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "properties": {},
            "geometry": {
                "type": "MultiPolygon",
                "coordinates": [
                    [
                        [
                            [-122.388793945, 37.790630481],
                            [-122.3887009, 37.790452],
                            ...
                        ]
                    ]
                ]
            }
        }
    ]
}` %}}

Returns the shoreline geometry inside the given XYZ tile as a GeoJSON `FeatureCollection`. The single feature in the collection has a `Polygon` or `MultiPolygon` geometry whose interior is land.

The shoreline is stitched from all ENC cells overlapping the tile, with low-resolution background data filling areas without ENC coverage. Below zoom level `4`, the response is exclusively low-resolution background data.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Path Parameters</b>

- **z**: Zoom level.
- **x**: Tile column.
- **y**: Tile row.

<b>Response</b>

On success, returns a GeoJSON `FeatureCollection` with at most one feature. When the tile is entirely water, the `features` array is empty.

<b>Error Responses</b>

- **400 Bad Request**: The tile coordinates are invalid or no shoreline data could be generated.
- **401 Unauthorized**: The token is missing or not valid.

{{% /apiEndpointCard %}}

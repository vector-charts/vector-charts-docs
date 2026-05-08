---
title: "Query ENC Features"
weight: 7
menu:
  oem:
    parent: "api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v1/enc_query" title="Query ENC Features" request=`POST https://<your-host>:9909/api/v1/enc_query
Authorization: Bearer <token>
Content-Type: application/json

{
    "position": {
        "longitude": -122.388,
        "latitude": 37.790
    },
    "radius": 200,
    "zoom": 14
}` response=`Status Code: 200 OK
Response Body:
{
    "results": [
        {
            "id": "f1a2b3c4-d5e6-7890-abcd-ef1234567890",
            "parentId": "5e37b9c1-a4c2-4b8e-9f3a-72d3f4a5b8e1",
            "parentCellName": "US5CA12M",
            "layerId": "BOYLAT",
            "layerName": "Buoy, lateral",
            "position": [37.7901, -122.3884],
            "geometry": {
                "type": "Polygon",
                "coordinates": [...]
            },
            "attributes": {
                "objectName": "1NM"
            },
            "rawAttributes": {
                "objnam": "1NM",
                "boyshp": 2,
                "colour": [3]
            },
            "bbox": [
                [-122.3886, 37.7900],
                [-122.3882, 37.7902]
            ]
        }
    ]
}` %}}

Returns the ENC features near a point. Use this to look up which chart objects (buoys, lighthouses, depth contours, etc.) are at a given location.

The query is scoped by `zoom`: higher zoom levels return more detailed features by selecting a finer S-57 usage band, matching what the vector tile renderer would show at the same zoom. Meta layers (`M_NSYS`, `M_QUAL`, `M_NPUB`, `MAGVAR`) are always excluded, and at zoom levels of `12` and below, depth contours and soundings (`DEPCNT`, `SOUNDG`) are excluded as well.

<b>Authentication</b>

This endpoint accepts a Bearer token in the `Authorization` header or a `token` query parameter. See [Authentication](/oem/api-reference/) for details.

<b>Request Body</b>

The request body should be JSON-encoded.

- **position**: An object with `longitude` and `latitude` fields, in WGS84 decimal degrees.
- **radius**: Search radius around `position`, in meters.
- **zoom**: Zoom level used to select the S-57 usage band for the search.

<b>Response Schema</b>

The endpoint returns a `results` array. Each entry describes one ENC feature.

- `id`: The unique identifier for the feature.
- `parentId`: The unique identifier for the ENC chart cell that contains the feature.
- `parentCellName`: The S-57 cell name of the parent chart (for example, `US5CA12M`).
- `layerId`: The S-57 layer acronym (for example, `BOYLAT` for a lateral buoy or `LNDARE` for land area).
- `layerName`: The human-readable name of the layer.
- `position`: The feature's centroid as `[latitude, longitude]`, or `null` for non-point features.
- `geometry`: The feature's geometry as a GeoJSON object, in WGS84 coordinates.
- `attributes`: A summary object. Currently contains only `objectName`, which mirrors the S-57 `objnam` attribute.
- `rawAttributes`: The full set of S-57 attributes for the feature, keyed by S-57 attribute acronym.
- `bbox`: The feature's bounding box as `[[minLongitude, minLatitude], [maxLongitude, maxLatitude]]`.

<b>Error Responses</b>

- **400 Bad Request**: The `radius` field is missing or not a number.
- **401 Unauthorized**: The token is missing or not valid.

{{% /apiEndpointCard %}}

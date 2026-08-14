---
title: "Get Reports (GeoJSON)"
weight: 7
menu:
  crowdsourced:
    parent: "user_report_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/tiles/{z}/{x}/{y}.json" title="Get Reports (GeoJSON)" request=`GET https://api.vectorcharts.com/api/v1/user-reports/tiles/12/1240/1515.json?token=<token>` response=`Status Code: 200 OK
Response Body:
{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "geometry": {
                "type": "Point",
                "coordinates": [-71.05, 42.36]
            },
            "properties": {
                "id": "550e8400-e29b-41d4-a716-446655440000",
                "reportType": "hazard",
                "upvoteCount": 3,
                "downvoteCount": 1,
                "isOwner": false,
                "label": "Hazard - 8/14 15:20",
                "properties": {
                    "description": "Shallow area reported"
                }
            }
        }
    ]
}` %}}

Returns active (non-deleted, non-expired) user reports intersecting the given slippy-map tile as a GeoJSON FeatureCollection. Useful for clients that prefer GeoJSON over MVT.

Each feature includes an `isOwner` flag for the calling token.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Path Parameters</b>

- **z**: Tile zoom level.
- **x**: Tile column.
- **y**: Tile row.

<b>Response</b>

A GeoJSON FeatureCollection where each feature is a Point geometry. Feature `properties` include the report id, type, vote counts, label, and nested report `properties`.

<b>Error Responses</b>

- **400 Bad Request**: Invalid tile coordinates.
- **401 Unauthorized**: Token is missing or invalid.

{{% /apiEndpointCard %}}

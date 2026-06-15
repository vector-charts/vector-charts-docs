---
title: "Get User Reports Tile"
weight: 4
menu:
  crowdsourced:
    parent: "user_report_api_reference"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-success\">GET</div>"
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/tiles/{z}/{x}/{y}.json" title="Get User Reports Tile" request=`GET https://api.vectorcharts.com/api/v1/user-reports/tiles/12/1240/1515.json?token=<token>` response=`Status Code: 200 OK
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
                "properties": {},
                "validVoteCount": 3,
                "invalidVoteCount": 1,
                "externalUserId": "app-user-abc123",
                "createdAt": 1718380800000,
                "updatedAt": 1718380900000,
                "expiresAt": 1718467200000,
                "isExpired": false,
                "isDeleted": false
            }
        }
    ]
}` %}}

Returns active (non-deleted, non-expired) user reports intersecting the given slippy-map tile as a GeoJSON FeatureCollection.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Path Parameters</b>

- **z**: Tile zoom level.
- **x**: Tile column.
- **y**: Tile row.

<b>Response</b>

A GeoJSON FeatureCollection where each feature is a Point geometry. Feature `properties` include the report id, type, vote counts, timestamps, and client metadata.

<b>Error Responses</b>

- **400 Bad Request**: Invalid tile coordinates.
- **401 Unauthorized**: Token is missing or invalid.

{{% /apiEndpointCard %}}

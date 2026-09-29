---
title: "Get Bathymetry Tracks"
weight: 9
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/bathymetry" title="Get Bathymetry Tracks" request=`GET https://api.vectorcharts.com/api/v1/user-reports/bathymetry?limit=50&offset=0
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
{
    "tracks": [
        {
            "id": "018f2c3a-7b9e-7c1d-8e2f-3a4b5c6d7e8f",
            "platform": {
                "uniqueId": "VESSEL-123",
                "name": "Example Vessel",
                "type": "Ship"
            },
            "metadata": {
                "providerContactPoint": {
                    "orgName": "Example Org",
                    "logger": "example-logger",
                    "loggerVersion": "1.0"
                },
                "depthUnits": "meters",
                "timeUnits": "ISO 8601",
                "convention": "CSB 2.0",
                "min_depth": 11.8,
                "max_depth": 12.5,
                "length_m": 142.3
            },
            "externalUserId": "app-user-abc123",
            "namespace": "public",
            "pointCount": 2,
            "startTime": 1718380800000,
            "endTime": 1718380860000,
            "createdAt": 1718380900000,
            "updatedAt": 1718380900000
        }
    ],
    "total": 1,
    "limit": 50,
    "offset": 0
}` %}}

List bathymetry tracks globally, ordered most recent first. Returns metadata only — soundings and geometry are not included. Use [Get Bathymetry Track]({{< relref "get-bathymetry.md" >}}) to fetch full sounding data for a single track.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Query Parameters</b>

- **limit** (Optional): Maximum number of tracks to return. Defaults to `50`. Capped at `200`.
- **offset** (Optional): Number of tracks to skip. Defaults to `0`.

<b>Response Schema</b>

- **tracks**: Array of bathymetry track metadata objects. Each includes `id`, `platform`, `metadata` (including `min_depth`, `max_depth`, and `length_m`), `pointCount`, `startTime`, `endTime`, `namespace`, and related ownership fields.
- **total**: Total number of tracks.
- **limit**: Applied page size.
- **offset**: Applied offset.

<b>Error Responses</b>

- **401 Unauthorized**: Token is missing or invalid.

{{% /apiEndpointCard %}}

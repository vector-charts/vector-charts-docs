---
title: "Get Bathymetry Track"
weight: 10
---

{{% apiEndpointCard method="GET" path="/api/v1/user-reports/bathymetry/{id}" title="Get Bathymetry Track" request=`GET https://api.vectorcharts.com/api/v1/user-reports/bathymetry/018f2c3a-7b9e-7c1d-8e2f-3a4b5c6d7e8f
Authorization: Bearer <token>` response=`Status Code: 200 OK
Response Body:
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
    "updatedAt": 1718380900000,
    "soundings": [
        {
            "latitude": 42.36,
            "longitude": -71.05,
            "depth": 12.5,
            "time": 1718380800000
        },
        {
            "latitude": 42.361,
            "longitude": -71.049,
            "depth": 11.8,
            "time": 1718380860000
        }
    ]
}` %}}

Fetch a single bathymetry track, including its full sounding series.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Path Parameters</b>

- **id**: UUID of the bathymetry track.

<b>Response Schema</b>

Returns the track metadata plus a `soundings` array. Each sounding includes `latitude`, `longitude`, `depth` (meters), and `time` (epoch milliseconds).

<b>Error Responses</b>

- **400 Bad Request**: Invalid track id.
- **401 Unauthorized**: Token is missing or invalid.
- **404 Not Found**: Track does not exist.

{{% /apiEndpointCard %}}

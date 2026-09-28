---
title: "Upload Bathymetry"
weight: 8
---

{{% apiEndpointCard method="POST" path="/api/v1/user-reports/bathymetry" title="Upload Bathymetry" request=`POST https://api.vectorcharts.com/api/v1/user-reports/bathymetry
Authorization: Bearer <token>
Content-Type: application/json

{
    "platform": {
        "uniqueId": "VESSEL-123",
        "name": "Example Vessel",
        "type": "Ship"
    },
    "providerContactPoint": {
        "orgName": "Example Org",
        "logger": "example-logger",
        "loggerVersion": "1.0"
    },
    "depthUnits": "meters",
    "timeUnits": "ISO 8601",
    "convention": "CSB 2.0",
    "externalUserId": "app-user-abc123",
    "soundings": [
        {
            "latitude": 42.36,
            "longitude": -71.05,
            "depth": 12.5,
            "time": "2024-06-14T15:30:00.000Z"
        },
        {
            "latitude": 42.361,
            "longitude": -71.049,
            "depth": 11.8,
            "time": 1718380860000
        }
    ]
}` response=`Status Code: 201 Created
Response Body:
{
    "tracks": [
        {
            "id": "018f2c3a-7b9e-7c1d-8e2f-3a4b5c6d7e8f",
            "pointCount": 2,
            "startTime": 1718380800000,
            "endTime": 1718380860000,
            "merged": false
        }
    ],
    "totalPoints": 2
}` %}}

Upload crowdsourced bathymetry soundings. The server sorts soundings by time, splits them into tracks, and may append to an existing open track for the same platform.

<b>Authentication</b>

Requires a Bearer token in the `Authorization` header or a `token` query parameter.

<b>Request Body</b>

- **soundings** <span style="color:red;">(Required)</span>: Non-empty array of sounding objects. Each sounding must include:
  - **latitude** / **longitude**: WGS84 coordinates.
  - **depth**: Depth in meters.
  - **time**: ISO 8601 timestamp string or epoch milliseconds (number or numeric string).
- **platform** (Optional): Platform metadata. `uniqueId` is used to decide whether new soundings may merge onto an existing open track for the same reporter.
- **providerContactPoint** (Optional): Provider / logger contact metadata stored on the track.
- **depthUnits** (Optional): If set, must be `meters`. Defaults to `meters`.
- **timeUnits** (Optional): Descriptive time unit label (for example `ISO 8601`). Defaults to `ISO 8601`.
- **convention** (Optional): Data convention label (for example `CSB 2.0`).
- **externalUserId** (Optional): Opaque user identifier from your application.

<b>Behavior</b>

- Soundings are sorted by time before track assignment.
- Consecutive soundings are split into separate tracks when the time gap exceeds the track gap (default **5 minutes** / `300000` ms).
- Tracks are also split when appending would exceed the max track size (default **256 KiB**).
- The first segment of a request may merge onto an open track for the same platform `uniqueId` when it falls within the gap window.
- Track IDs are server-generated UUIDv7 values.

On Vector Charts OEM, `trackGapMs`, `maxSoundingsPerRequest`, and `maxTrackBytes` are configurable via environment variables.

<b>Response Schema</b>

- **tracks**: Array of track summaries created or updated by this request.
  - **id**: Track UUID.
  - **pointCount**: Total points on the track after the write.
  - **startTime** / **endTime**: Track time range in epoch milliseconds.
  - **merged**: `true` when soundings were appended to an existing track; `false` for a newly created track.
- **totalPoints**: Number of soundings accepted in this request.

<b>Error Responses</b>

- **400 Bad Request**: Missing or invalid soundings, invalid coordinates/depth/time, or unsupported `depthUnits`.
- **401 Unauthorized**: Token is missing or invalid.
- **413 Payload Too Large**: Too many soundings in one request (default max **50000**).

{{% /apiEndpointCard %}}

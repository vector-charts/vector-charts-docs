---
title: "Look Up Polylines"
weight: 3
menu:
  main:
    parent: "elevation_api"
    weight: 3
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/lookup/polylines" title="Look Up Polylines" request=`POST https://api.vectorcharts.com/api/v2/elevation/lookup/polylines
Authorization: Bearer <token>
Content-Type: application/json

{
    "polylines": [
        {
            "coordinates": [
                { "latitude": 42.3601, "longitude": -71.0589 },
                { "latitude": 42.3650, "longitude": -71.0500 },
                { "latitude": 42.3700, "longitude": -71.0400 }
            ],
            "totalSamples": 50
        }
    ],
    "options": {
        "filterOutputReferences": ["MSL"],
        "outputUnit": "meters"
    }
}` response=`Status Code: 200 OK
{
    "metadata": {
        "unit": "meters"
    },
    "data": [
        {
            "locations": [
                { "latitude": 42.3601, "longitude": -71.0589 },
                ...
            ],
            "elevations": [
                {
                    "reference": "MSL",
                    "values": [12.4, 11.8, ...]
                }
            ],
            "failures": []
        }
    ]
}` %}}

Look up surface elevation sampled along one or more polylines (lines). Samples are spaced evenly along each line. Useful for profiles, routes, and clearance checks.

Each polyline produces one entry in the response `data` array. Failed samples appear in that entry's `failures` list and as `null` in `values`.

<b>Authentication</b>

Send a Bearer token in the `Authorization` header, or a `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<b>Request Body</b>

*The request body should be JSON-encoded.*

- **polylines** <span style="color:red;">(Required)</span>: Array of 1–1,000 polylines. Each polyline object has:
  - **coordinates** <span style="color:red;">(Required)</span>: Array of at least 2 `{ latitude, longitude }` vertices (no consecutive duplicates). Across the whole request, at most 10,000 coordinates.
  - **totalSamples** (Optional): Number of samples along the line (integer `2`–`10,000`). Defaults to `10`.
- **options** (Optional):
  - **filterOutputReferences**: Array of `"MSL"` and/or `"HAE"`. Defaults to both.
  - **tileZoom**: Integer `0`–`30`. Source tile zoom used for sampling. Defaults to `14`.
  - **outputUnit**: `"meters"` / `"m"` or `"feet"` / `"ft"`. Defaults to `"meters"`.

Total samples across all polylines must not exceed 100,000.

<b>Response Schema</b>

- **metadata.unit**: `"meters"` or `"feet"`.
- **data**: Array with one elevation result per polyline (same order as the request). Each entry includes:
  - **locations**: Sample coordinates along the line.
  - **elevations**: One entry per requested reference, with `values` aligned to `locations`.
  - **failures**: Per-sample failures with `index`, `location`, `code`, and `message`.

<b>Error Responses</b>

- **400 Bad Request**: Invalid polylines or options.
- **413 Payload Too Large**: Request exceeds supported coordinate or sampling limits.
- **502 Bad Gateway**: Elevation provider failure.
- **503 Service Unavailable**: Elevation service is unavailable.

{{% /apiEndpointCard %}}

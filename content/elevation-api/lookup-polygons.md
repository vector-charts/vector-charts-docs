---
title: "Look Up Polygons"
weight: 4
menu:
  main:
    parent: "elevation_api"
    weight: 4
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/lookup/polygons" title="Look Up Polygons" request=`POST https://api.vectorcharts.com/api/v2/elevation/lookup/polygons
Authorization: Bearer <token>
Content-Type: application/json

{
    "polygons": [
        {
            "coordinates": [
                { "latitude": 42.3600, "longitude": -71.0600 },
                { "latitude": 42.3600, "longitude": -71.0500 },
                { "latitude": 42.3700, "longitude": -71.0500 },
                { "latitude": 42.3700, "longitude": -71.0600 }
            ],
            "xSamples": 20,
            "ySamples": 20
        }
    ],
    "options": {
        "filterOutputReferences": ["MSL", "HAE"],
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
                { "latitude": 42.3600, "longitude": -71.0600 },
                ...
            ],
            "elevations": [
                {
                    "reference": "MSL",
                    "values": [12.4, ...]
                },
                {
                    "reference": "HAE",
                    "values": [-15.2, ...]
                }
            ],
            "failures": []
        }
    ]
}` %}}

Look up surface elevation sampled over one or more polygons (areas). Samples are taken on a grid inside each polygon. Useful for area clearance, coverage analysis, and statistics over a region.

Each polygon produces one entry in the response `data` array. Failed samples appear in that entry's `failures` list and as `null` in `values`.

Polygons must be simple rings. Do not repeat the first coordinate as a closing point.

<b>Authentication</b>

Send a Bearer token in the `Authorization` header, or a `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<b>Request Body</b>

*The request body should be JSON-encoded.*

- **polygons** <span style="color:red;">(Required)</span>: Array of 1–1,000 polygons. Each polygon object has:
  - **coordinates** <span style="color:red;">(Required)</span>: Array of at least 3 `{ latitude, longitude }` ring vertices (simple ring; do not repeat the first point). Across the whole request, at most 10,000 coordinates.
  - **xSamples** (Optional): Number of samples along the X axis of the sampling grid (integer `2`–`10,000`). Defaults to `10`.
  - **ySamples** (Optional): Number of samples along the Y axis of the sampling grid (integer `2`–`10,000`). Defaults to `10`.
- **options** (Optional):
  - **filterOutputReferences**: Array of `"MSL"` and/or `"HAE"`. Defaults to both.
  - **tileZoom**: Integer `0`–`30`. Source tile zoom used for sampling. Defaults to `14`.
  - **outputUnit**: `"meters"` / `"m"` or `"feet"` / `"ft"`. Defaults to `"meters"`.

For each polygon, the sample count is `xSamples × ySamples` (using defaults of `10` when omitted). Total samples across all polygons must not exceed 100,000.

<b>Response Schema</b>

- **metadata.unit**: `"meters"` or `"feet"`.
- **data**: Array with one elevation result per polygon (same order as the request). Each entry includes:
  - **locations**: Sample coordinates in the area.
  - **elevations**: One entry per requested reference, with `values` aligned to `locations`.
  - **failures**: Per-sample failures with `index`, `location`, `code`, and `message`.

<b>Error Responses</b>

- **400 Bad Request**: Invalid polygons or options.
- **413 Payload Too Large**: Request exceeds supported coordinate or sampling limits.
- **502 Bad Gateway**: Elevation provider failure.
- **503 Service Unavailable**: Elevation service is unavailable.

{{% /apiEndpointCard %}}

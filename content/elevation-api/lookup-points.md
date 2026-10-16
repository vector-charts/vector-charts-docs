---
title: "Look Up Points"
weight: 2
menu:
  main:
    parent: "elevation_api"
    weight: 2
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/lookup/points" title="Look Up Points" request=`POST https://api.vectorcharts.com/api/v2/elevation/lookup/points
Authorization: Bearer <token>
Content-Type: application/json

{
    "coordinates": [
        { "latitude": 42.3601, "longitude": -71.0589 },
        { "latitude": 37.7749, "longitude": -122.4194 }
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
    "data": {
        "locations": [
            { "latitude": 42.3601, "longitude": -71.0589 },
            { "latitude": 37.7749, "longitude": -122.4194 }
        ],
        "elevations": [
            {
                "reference": "MSL",
                "values": [12.4, 16.1]
            },
            {
                "reference": "HAE",
                "values": [-15.2, -16.8]
            }
        ],
        "failures": []
    }
}` %}}

Look up surface elevation at one or more coordinates. Returns mean sea level (MSL) and/or height above ellipsoid (HAE) values from the Vector Charts elevation dataset (basemap terrain combined with chart bathymetry where available).

Failed samples appear in `failures` and as `null` in the corresponding `values` entry; other samples in the same request still succeed.

<b>Authentication</b>

Send a Bearer token in the `Authorization` header, or a `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<b>Request Body</b>

*The request body should be JSON-encoded.*

- **coordinates** <span style="color:red;">(Required)</span>: Array of 1–10,000 `{ latitude, longitude }` points. Latitude must be in `[-90, 90]`; longitude in `[-180, 180]`.
- **options** (Optional):
  - **filterOutputReferences**: Array of `"MSL"` and/or `"HAE"`. Defaults to both.
  - **tileZoom**: Integer `0`–`30`. Source tile zoom used for sampling. Defaults to `14`.
  - **outputUnit**: `"meters"` / `"m"` or `"feet"` / `"ft"`. Defaults to `"meters"`.

<b>Response Schema</b>

- **metadata.unit**: `"meters"` or `"feet"`.
- **data.locations**: Sample coordinates (same order as the request).
- **data.elevations**: One entry per requested reference, each with a `values` array aligned to `locations`. Failed samples are `null`.
- **data.failures**: Per-sample failures with `index`, `location`, `code`, and `message`.

<b>Error Responses</b>

- **400 Bad Request**: Invalid coordinates or options.
- **413 Payload Too Large**: Request exceeds supported coordinate or sampling limits.
- **502 Bad Gateway**: Elevation provider failure.
- **503 Service Unavailable**: Elevation service is unavailable.

{{% /apiEndpointCard %}}

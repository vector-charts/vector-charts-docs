---
title: "Lookup Elevation along Polylines"
weight: 5.2
menu:
  main:
    parent: "api_reference"
    name: "Lookup polylines"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/lookup/polylines" title="Lookup Elevation along Polylines" request=`POST https://api.vectorcharts.com/api/v2/elevation/lookup/polylines
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json

{
  "polylines": [
    {
      "coordinates": [
        { "latitude": 37.808, "longitude": -122.476 },
        { "latitude": 37.826, "longitude": -122.480 }
      ],
      "totalSamples": 4
    }
  ],
  "options": {
    "outputUnit": "meters",
    "filterOutputReferences": ["MSL"]
  }
}` response=`Status Code: 200 OK
Content-Type: application/json

{
  "metadata": { "unit": "meters" },
  "data": [
    {
      "locations": [
        { "latitude": 37.808, "longitude": -122.476 },
        { "latitude": 37.814, "longitude": -122.4773 },
        { "latitude": 37.820, "longitude": -122.4787 },
        { "latitude": 37.826, "longitude": -122.480 }
      ],
      "elevations": [
        { "reference": "MSL", "values": [6.0, -4.2, -15.0, 3.5] }
      ],
      "failures": []
    }
  ]
}` %}}

Samples one or more polylines. `data` is an array with one entry per polyline, in request order. Intermediate locations are spaced by great-circle distance and are not the input vertices, except the first and last sample.

See [Elevation](/api-reference/query-elevation/) for units, depth sign, limits, and errors. The numbers above show the JSON shape.

<b>Authentication</b>

Bearer token or `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<b>Request Body</b>

- **polylines** <span style="color:red;">(Required)</span>: 1 to 1000 shapes.
  - **coordinates**: At least two positions. No two consecutive positions may be the same. The whole request may contain at most 10000 coordinates.
  - **totalSamples** (Optional): Integer from 2 through 10000. Default 10. Includes both endpoints.
- **options**: Same fields as [Lookup points](/api-reference/elevation-lookup-points/).

The sample budget for the request is at most 100000. An omitted `totalSamples` counts as 10.

<b>Response</b>

`metadata.unit` is `meters` or `feet`. Each `data[]` entry has `locations`, `elevations`, and `failures`, aligned by index. `locations.length` equals `totalSamples` for that polyline.

{{% /apiEndpointCard %}}

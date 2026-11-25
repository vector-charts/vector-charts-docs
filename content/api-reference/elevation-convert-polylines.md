---
title: "Convert Altitude along Polylines"
weight: 5.5
menu:
  main:
    parent: "api_reference"
    name: "Convert polylines"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/convert/polylines" title="Convert Altitude along Polylines" request=`POST https://api.vectorcharts.com/api/v2/elevation/convert/polylines
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json

{
  "initialAltitude": {
    "value": 50,
    "unit": "feet",
    "reference": "MSL"
  },
  "targetPolylines": [
    {
      "coordinates": [
        { "latitude": 37.808, "longitude": -122.476 },
        { "latitude": 37.826, "longitude": -122.480 }
      ],
      "totalSamples": 2
    }
  ],
  "options": {
    "outputUnit": "meters",
    "filterOutputReferences": ["MSL", "AGL"]
  }
}` response=`Status Code: 200 OK
Content-Type: application/json

{
  "metadata": {
    "unit": "meters",
    "constantAltitude": {
      "value": 15.24,
      "unit": "meters",
      "reference": "MSL"
    }
  },
  "data": [
    {
      "locations": [
        { "latitude": 37.808, "longitude": -122.476 },
        { "latitude": 37.826, "longitude": -122.480 }
      ],
      "altitudes": [
        { "reference": "MSL", "values": [15.24, 15.24] },
        { "reference": "AGL", "values": [9.2, 15.24] }
      ],
      "failures": []
    }
  ]
}` %}}

Holds one altitude and converts it along each polyline. `data` is an array with one entry per polyline. Sampling matches [Lookup polylines](/api-reference/elevation-lookup-polylines/): `totalSamples` defaults to 10 and includes both endpoints.

`metadata.constantAltitude.value` is the held altitude in `outputUnit`. 50 feet is 15.24 meters. Because the held reference is `MSL`, that band does not sample the surface and both samples stay 15.24. `AGL` does sample.

See [Convert points](/api-reference/elevation-convert-points/) for `initialAltitude`, `constantAltitude`, and the altitude references. See [Elevation](/api-reference/query-elevation/) for limits and errors. The numbers above show the JSON shape.

<b>Authentication</b>

Bearer token or `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<b>Request Body</b>

- **initialAltitude** <span style="color:red;">(Required)</span>: `{ value, unit, reference }`.
- **targetPolylines** <span style="color:red;">(Required)</span>: 1 to 1000 polylines. Each needs at least two coordinates and an optional `totalSamples` from 2 through 10000.
- **options**: Same as [Convert points](/api-reference/elevation-convert-points/).

{{% /apiEndpointCard %}}

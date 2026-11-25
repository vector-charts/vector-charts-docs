---
title: "Lookup Elevation at Points"
weight: 5.1
menu:
  main:
    parent: "api_reference"
    name: "Lookup points"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/lookup/points" title="Lookup Elevation at Points" request=`POST https://api.vectorcharts.com/api/v2/elevation/lookup/points
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json

{
  "coordinates": [
    { "latitude": 37.8199, "longitude": -122.4783 },
    { "latitude": 37.8324, "longitude": -122.4795 }
  ],
  "options": {
    "tileZoom": 14,
    "outputUnit": "meters",
    "filterOutputReferences": ["MSL", "HAE"]
  }
}` response=`Status Code: 200 OK
Content-Type: application/json

{
  "metadata": { "unit": "meters" },
  "data": {
    "locations": [
      { "latitude": 37.8199, "longitude": -122.4783 },
      { "latitude": 37.8324, "longitude": -122.4795 }
    ],
    "elevations": [
      { "reference": "MSL", "values": [-18.4, 12.0] },
      { "reference": "HAE", "values": [-50.6, -20.2] }
    ],
    "failures": []
  }
}` %}}

Returns the elevation at each coordinate. `data` is one result object, not an array.

Units, the sign of depths, sampling limits, and error bodies are in [Elevation](/api-reference/query-elevation/). The numbers above show the JSON shape.

<b>Authentication</b>

Bearer token or `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<b>Request Body</b>

- **coordinates** <span style="color:red;">(Required)</span>: One to 10000 objects with finite `latitude` and `longitude`.
- **options** (Optional):
  - **tileZoom**: Integer 0 through 30. Default 14. Bathymetry is available at 14.
  - **outputUnit**: `meters`, `m`, `feet`, or `ft`. Default `meters`.
  - **filterOutputReferences**: `MSL` and/or `HAE`. Default both.
  - **clamp**: `none` (default), `terrain`, or `ocean`.
  - **refreshCache**: `true` refetches source tiles.

<b>Response</b>

- **metadata.unit**: `meters` or `feet`.
- **data.locations**: The requested coordinates, in order.
- **data.elevations**: One band per reference. `values[i]` matches `locations[i]` and is `null` when that sample failed.
- **data.failures**: `{ index, location, code, message }` for samples that failed. Empty when every sample succeeded.

A negative `MSL` value is below mean sea level (seafloor). A positive value is terrain above mean sea level.

{{% /apiEndpointCard %}}

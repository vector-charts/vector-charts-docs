---
title: "Convert Altitude at Points"
weight: 9.4
menu:
  oem:
    parent: "api_reference"
    name: "Convert points"
    pre: "<div class=\"bp3-tag bp3-minimal bp3-intent-primary\">POST</div>"
---

{{% apiEndpointCard method="POST" path="/api/v2/elevation/convert/points" title="Convert Altitude at Points" request=`POST https://<your-host>:9909/api/v2/elevation/convert/points
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json

{
  "initialAltitude": {
    "value": 30,
    "unit": "meters",
    "reference": "AGL"
  },
  "targetPoints": [
    { "latitude": 37.8199, "longitude": -122.4783 }
  ],
  "options": {
    "outputUnit": "meters",
    "filterOutputReferences": ["MSL", "HAE", "AGL", "AboveSeafloor"]
  }
}` response=`Status Code: 200 OK
Content-Type: application/json

{
  "metadata": {
    "unit": "meters",
    "constantAltitude": {
      "value": 30,
      "unit": "meters",
      "reference": "AGL"
    }
  },
  "data": {
    "locations": [
      { "latitude": 37.8199, "longitude": -122.4783 }
    ],
    "altitudes": [
      { "reference": "MSL", "values": [11.6] },
      { "reference": "HAE", "values": [-20.6] },
      { "reference": "AGL", "values": [30] },
      { "reference": "AboveSeafloor", "values": [48.4] }
    ],
    "failures": []
  }
}` %}}

Holds `initialAltitude` and reports that same altitude in other references at each target point. `data` is one result object.

When `options.constantAltitude` is omitted, the held value is `initialAltitude` converted into `outputUnit`. Set `constantAltitude` to first convert `initialAltitude` into `constantReference` at `initialLocation`, then hold that anchored value for every target. `metadata.constantAltitude` is the held value in the output unit.

A band whose reference is the held reference does not sample the surface. In the example, `AGL` stays 30 because that is the held reference. `AGL` is height above terrain on land and above 0 m MSL on water. `AboveSeafloor` is height above terrain on land and above the seafloor on water.

See [Elevation](/oem/api-reference/elevation/) for datums, depth sign, limits, and errors. The numbers above show the JSON shape.

<b>Authentication</b>

Bearer token or `token` query parameter. See [Authentication](/oem/api-reference/).

<b>Request Body</b>

- **initialAltitude** <span style="color:red;">(Required)</span>:
  - **value**: Finite number.
  - **unit**: `meters`, `m`, `feet`, or `ft`.
  - **reference**: `MSL`, `HAE`, `AGL`, `AboveSeafloor`, or `above_seafloor`.
- **targetPoints** <span style="color:red;">(Required)</span>: One to 10000 coordinates.
- **options** (Optional): `tileZoom`, `outputUnit`, `filterOutputReferences`, `clamp`, and `refreshCache`, as on [Lookup points](/oem/api-reference/elevation-lookup-points/). Convert requests may also filter to `AGL` and `AboveSeafloor`. Default filter is all four references.
  - **constantAltitude** (Optional): `{ "constantReference", "initialLocation" }`. `constantReference` uses the same names as `initialAltitude.reference`. `initialLocation` is a coordinate.

<b>Response</b>

`data.altitudes` has one band per requested reference. `values[i]` is `null` when that sample failed. `failures` uses `{ index, location, code, message }`.

{{% /apiEndpointCard %}}

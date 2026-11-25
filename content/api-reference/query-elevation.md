---
title: "Elevation"
weight: 5
menu:
  main:
    parent: "api_reference"
    name: "Elevation"
---

The elevation API samples a combined terrain and bathymetry surface, and it can convert a held altitude into other altitude references. Positions are WGS84. Heights are positive upward.

These routes are served by the Cloud API at `https://api.vectorcharts.com`. The same routes are available on an [OEM](/oem/api-reference/elevation/) instance.

| Method | Path | Page |
| --- | --- | --- |
| POST | `/api/v2/elevation/lookup/points` | [Lookup points](/api-reference/elevation-lookup-points/) |
| POST | `/api/v2/elevation/lookup/polylines` | [Lookup polylines](/api-reference/elevation-lookup-polylines/) |
| POST | `/api/v2/elevation/lookup/polygons` | [Lookup polygons](/api-reference/elevation-lookup-polygons/) |
| POST | `/api/v2/elevation/convert/points` | [Convert points](/api-reference/elevation-convert-points/) |
| POST | `/api/v2/elevation/convert/polylines` | [Convert polylines](/api-reference/elevation-convert-polylines/) |
| POST | `/api/v2/elevation/convert/polygons` | [Convert polygons](/api-reference/elevation-convert-polygons/) |
| GET | `/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png` | [Elevation tiles](/api-reference/elevation-tiles/) |
| GET | `/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.webp` | [Elevation tiles](/api-reference/elevation-tiles/) |

Send JSON lookup and convert bodies with `Content-Type: application/json`. The JSON parser accepts bodies up to 10MB.

## Authentication

Every elevation route requires an API token, either as a bearer token or as a `token` query parameter. See [Authentication](/api-reference/api-authentication/).

<pre>
Authorization: Bearer YOUR_API_TOKEN
</pre>

An `endUserId` query parameter or `X-Vector-Charts-End-User` header attributes the call to one end user. The header wins when both are set. The value is at most 256 characters. See [Authentication](/api-reference/api-authentication/).

Elevation lookup, convert, and tiles are not on the enterprise-only path list. A token whose account has valid payment can call them. Cloud still counts each call toward account usage. See [Limits](#limits).

## Elevation surface

The default surface (`options.clamp` omitted or `"none"`) is a sign composite:

- A sample **greater than 0** comes from the terrain source.
- A sample **less than 0** comes from bathymetry when that source has a negative value.
- A sample of **0** is mean sea level. Bathymetry is not used for that pixel, because only a strictly negative bathymetry sample replaces terrain.

`options.clamp` selects a different surface. The server forwards `clamp` to the elevation engine. Allowed values are `none`, `terrain`, and `ocean`.

- `none`: land terrain and seafloor, as above.
- `terrain`: land elevations are kept. Ocean is set to 0 m mean sea level.
- `ocean`: bathymetry is kept and capped at 0. Land is set to 0 m mean sea level.

`terrain` and `ocean` use a MapTiler land polygon as the shoreline mask. The default `none` surface does not.

### Data sources and resolution

Terrain is a Terrarium raster from the Zydro elevation tile service (`elevation-tile-api.zydro.net`). Its native maximum zoom is 12. The server bilinear-overzooms it through zoom 14.

Bathymetry is current S-102 coverage visible to the token's account. The server renders that coverage to Mapbox Terrain-RGB and only serves it at zoom 14. Charted depth is stored positive-down in the S-102 grid. The raster converts it to elevation with `min(-0.01, -depth)`, so seafloor samples are negative and never reach 0. A charted drying height (a negative depth) is flattened to -0.01 m and does not appear above the sea surface. The code does not apply a further shift from the chart sounding datum onto the geoid; the negated depth is what the API reports as MSL.

`options.tileZoom` chooses the raster zoom used to sample. It is an integer from 0 through 30. The default is 14.

- Below zoom 14 the bathymetry source is out of range. A missing bathymetry tile is ignored and the terrain sample is kept, so those queries do not return S-102 seafloor.
- Above zoom 14 the composite is bilinear-overzoomed. Finer zooms do not add source detail.
- Terrain-RGB values are quantized to 0.1 m.

There is no per-request rate limit on these routes. A bathymetry failure that is coverage, transport, decode, forbidden, or a missing resource does not fail the whole sample: the terrain value is kept. A terrain failure fails that sample.

## Altitude references

Input names are case-insensitive. Responses use the canonical spelling.

| Response value | Accepted input | Meaning |
| --- | --- | --- |
| `MSL` | `msl` | Orthometric height relative to the EGM2008 geoid (`egm2008-1`). Mean sea level. |
| `HAE` | `hae` | Height above the WGS84 ellipsoid. It differs from `MSL` by the EGM2008 geoid undulation and does not read the terrain surface. |
| `AGL` | `agl` | Height above ground. On land this is above the terrain. On water it is above 0 m MSL, not above the seafloor. Convert requests only. |
| `AboveSeafloor` | `aboveseafloor`, `above_seafloor` | Height above the normal surface: terrain on land and seafloor on water. Convert requests only. |

Lookup requests can ask for `MSL` and `HAE`. Convert requests can ask for all four.

`options.outputUnit` accepts `meters`, `m`, `feet`, or `ft` (any case). The default is meters. The response `metadata.unit` is `meters` or `feet`.

`options.filterOutputReferences` limits which bands are returned. Lookup defaults to `MSL` and `HAE`. Convert defaults to all four references. `options.refreshCache` set to `true` skips cached tiles and fetches sources again.

## Sampling

Coordinates are objects with finite `latitude` and `longitude` in decimal degrees. Latitude must be from -90 through 90. Longitude must be from -180 through 180.

- **Points.** Each coordinate is one sample.
- **Polylines.** At least two coordinates, with no consecutive duplicates. `totalSamples` is an integer from 2 through 10000. The default is 10. Samples include both endpoints and are spaced evenly by great-circle distance.
- **Polygons.** At least three coordinates forming a simple ring with non-zero area. Do not repeat the first coordinate at the end, and do not repeat a coordinate twice in a row. `xSamples` and `ySamples` are integers from 2 through 10000. Each defaults to 10. The server builds an `xSamples` by `ySamples` grid of cell centers over the ring's longitude/latitude bounding box, then keeps centers that fall strictly inside the ring. Points on the boundary are dropped, so the result can be shorter than `xSamples * ySamples`. Spacing is even in degrees, not meters.

One request may contain at most 1000 shapes and 10000 coordinates in total. The sample budget is at most 10000 per shape and 100000 for the request. Omitted polyline and polygon sample counts count as 10 toward that budget.

## Response shape

A successful lookup returns HTTP 200 and JSON:

<pre>
{
  "metadata": { "unit": "meters" },
  "data": {
    "locations": [ { "latitude": 0, "longitude": 0 } ],
    "elevations": [
      { "reference": "MSL", "values": [0] },
      { "reference": "HAE", "values": [0] }
    ],
    "failures": []
  }
}
</pre>

`elevations[].values[i]` is the height at `locations[i]`, or `null` when that sample failed. `failures[]` entries are `{ "index", "location", "code", "message" }`. `message` is engine text and is not a stable catalog. `code` is one of `no_coverage`, `transport_failure`, `decode_failure`, `missing_resource`, `cancelled`, `configuration_failure`, `internal_failure`, `clamp_unsupported`, `invalid_request`, or `forbidden`.

Point lookup and point convert return one result object in `data`. Polyline and polygon routes return `data` as an array with one entry per shape, in request order. Convert responses use `altitudes` instead of `elevations`, and `metadata` also includes `constantAltitude` (the held altitude, in the output unit).

Numbers in the endpoint examples illustrate this shape. They are not captured measurements.

## Limits

The controller rejects a body that exceeds the coordinate or sample budget with HTTP 413:

<pre>
{
  "statusCode": 413,
  "message": "Elevation request exceeds supported coordinate or sampling limits.",
  "timestamp": "2026-01-01T00:00:00.000Z"
}
</pre>

There is no elevation-specific request-rate limit in the route or in nginx. On Cloud, each authenticated call increments the account usage counter. When the account is not in good standing and that counter is at least 24900 for the billing period, the call is rejected with HTTP 403 and `{ "success": false, "timestamp": <epoch milliseconds> }`. See [Usage & Billing](/getting-started/billing/). OEM does not apply this check.

## Errors

Validation errors use this JSON object. `timestamp` is ISO-8601.

<pre>
{ "statusCode": 400, "message": "...", "timestamp": "2026-01-01T00:00:00.000Z" }
</pre>

Typical validation messages:

- `coordinates must contain between 1 and 10000 coordinates.` (and the same form for `polylines`, `polygons`, `targetPoints`, `targetPolylines`, `targetPolygons`, and `coordinates` inside a shape)
- `coordinate must include finite latitude and longitude values.`
- `coordinate is outside valid latitude/longitude bounds.`
- `totalSamples must be an integer between 2 and 10000.` (`xSamples` and `ySamples` use the same sentence)
- `options.tileZoom must be an integer between 0 and 30.`
- `options.outputUnit is invalid.`
- `options.filterOutputReferences is invalid.` for a lookup reference other than MSL or HAE
- `initialAltitude must include a finite value.`
- `initialAltitude.unit is invalid.`
- `initialAltitude.reference is invalid.`

A polyline or polygon that the engine rejects (duplicate vertices, a self-intersecting ring, a zero-area ring) becomes HTTP 400 with message `Elevation request is not valid.`

Authentication failures use a different object. `timestamp` is epoch milliseconds, and a missing or unknown token has no `message`:

| Status | When | Body |
| --- | --- | --- |
| 401 | Missing or unknown token | `{ "success": false, "timestamp": 0 }` |
| 401 | Token host restriction failed | `{ "success": false, "timestamp": 0, "message": "Origin ... is not in scope for this token." }` |
| 403 | Cloud billing block described above | `{ "success": false, "timestamp": 0 }` |

When the elevation engine rejects the whole call, the HTTP status is mapped as follows. Per-sample failures stay HTTP 200 and are listed in `failures`.

| Status | Engine condition | `message` |
| --- | --- | --- |
| 400 | `invalid_argument` | `Elevation request is not valid.` |
| 500 | `internal_failure` | `Elevation request failed.` |
| 502 | `no_coverage`, `transport_failure`, or `decode_failure` | `Elevation provider is unavailable.` |
| 503 | `missing_resource` or `configuration_failure` | `Elevation service is not configured correctly.` |
| 503 | `cancelled` or `not_running` | `Elevation service is unavailable.` |

Tile routes that reject the tile index return HTTP 400 with an empty body. See [Elevation tiles](/api-reference/elevation-tiles/).

---
title: "Elevation"
weight: 9
menu:
  oem:
    parent: "api_reference"
    name: "Elevation"
---

The elevation API samples a combined terrain and bathymetry surface, and it can convert a held altitude into other altitude references. OEM serves the same routes as Cloud. Nginx on port 9909 proxies `/api/v2/elevation/` and `/api/v2/tiles/` to the chart server. The base URL is:

<pre>
https://&lt;your-host&gt;:9909
</pre>

| Method | Path | Page |
| --- | --- | --- |
| POST | `/api/v2/elevation/lookup/points` | [Lookup points](/oem/api-reference/elevation-lookup-points/) |
| POST | `/api/v2/elevation/lookup/polylines` | [Lookup polylines](/oem/api-reference/elevation-lookup-polylines/) |
| POST | `/api/v2/elevation/lookup/polygons` | [Lookup polygons](/oem/api-reference/elevation-lookup-polygons/) |
| POST | `/api/v2/elevation/convert/points` | [Convert points](/oem/api-reference/elevation-convert-points/) |
| POST | `/api/v2/elevation/convert/polylines` | [Convert polylines](/oem/api-reference/elevation-convert-polylines/) |
| POST | `/api/v2/elevation/convert/polygons` | [Convert polygons](/oem/api-reference/elevation-convert-polygons/) |
| GET | `/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.png` | [Elevation tiles](/oem/api-reference/elevation-tiles/) |
| GET | `/api/v2/tiles/elevation-unified-v1/{z}/{x}/{y}.webp` | [Elevation tiles](/oem/api-reference/elevation-tiles/) |

Request fields, response JSON, units, sampling, and error bodies match the [Cloud elevation reference](/api-reference/query-elevation/). This page covers how OEM exposes that API and where the data comes from. Numbers in the endpoint examples illustrate the JSON shape. They are not captured measurements.

## Authentication

Core API tokens work the same way as the rest of the OEM Core API: `Authorization: Bearer` or a `token` query parameter. Create tokens with the [Portal API](/oem/portal-api-reference/api-tokens/). See [Core API Overview](/oem/api-reference/).

`endUserId` or `X-Vector-Charts-End-User` is accepted, the same as on other Core API routes.

OEM runs with `DEPLOYMENT_MODE=oem`. In that mode the server does not apply the Cloud free-tier usage cap, and it does not increment the Cloud usage counter. A valid OEM token is enough. There is still no separate per-route rate limit.

The portal process on port 9904 does not implement elevation. Calls belong on the Core API paths above, not under `/api/portal/`.

## What is bundled

The OEM image does not contain a digital elevation model. It runs the chart server's elevation configuration. Seafloor and terrain are loaded from different places:

- **Bathymetry** is current S-102 data loaded into that instance and visible to the token's account. Upload those charts through the OEM chart workflow. With no S-102 coverage, samples stay on the terrain surface.
- **Terrain** is fetched at request time from `https://elevation-tile-api.zydro.net` (Terrarium tiles, native through zoom 12). The container needs outbound HTTPS to that host. The tiles are not stored in the image.
- **Shoreline masking** for `options.clamp` of `terrain` or `ocean` uses MapTiler land tiles and the server `ENGINE_MAPTILER_KEY`. The default clamp, `none`, does not call MapTiler.

`HAE` uses the EGM2008 geoid file `egm2008-1`, which the chart server image installs. OEM does not need a separate geoid setting.

To point the process at a different elevation configuration file, set `ELEVATION_CONFIG_PATH` to that file. Leave it unset to use the configuration shipped in the image. See [Configuration](/oem/configuration/#elevation).

## Surface, units, and sampling

Heights are positive upward, in meters unless `options.outputUnit` is `feet` or `ft`.

The default surface keeps terrain where the sample is above 0 m mean sea level and uses bathymetry where the bathymetry sample is below 0. S-102 depth is negated and then capped at -0.01 m, so seafloor values are negative and charted drying heights do not rise above the sea surface. That negated depth is reported as `MSL`. The server does not apply an extra chart-datum to geoid shift.

`MSL` is the EGM2008 geoid. `HAE` is WGS84 ellipsoidal height. Convert routes also return `AGL` (terrain on land, 0 m MSL on water) and `AboveSeafloor` (terrain on land, seafloor on water).

`options.tileZoom` defaults to 14 and must be an integer from 0 through 30. S-102 is sampled only at zoom 14. Lower zooms keep the terrain sample. Higher zooms bilinear-overzoom the zoom-14 composite.

Sampling limits, the `clamp` values `none`, `terrain`, and `ocean`, and the validation and auth error bodies are listed in the [Cloud elevation reference](/api-reference/query-elevation/). The paths and JSON are the same on OEM; only the host changes.

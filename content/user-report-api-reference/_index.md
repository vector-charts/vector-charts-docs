---
title: "Overview"
weight: 1
---

The User Report API allows your end users to share location-based feedback (for example uncharted hazards, accidents, weather, and wildlife). 

Vector Charts runs the infrastructure, allowing you to build rich user-feedback into your application without needing backend infrastructure.

For an example of user reports in action, try out user reports in our [Vector Charts Demo App](https://app.vectorcharts.com/).

![User reports on the chart](/img/reports-2.png)

## Types of reports

The User Reports API supports two kinds of data:

- **Point reports**: Latitude/longitude reports tagged with a category and optional description (for example hazards, accidents, weather, and wildlife).
- **Bathymetry tracks**: Time-series latitude/longitude/depth soundings stored as tracks. When user reports are enabled on the style, tracks are shown as depth-colored lines.

## Report reputation

We expose two ways of evaluating report reputation and relevance:
- Time: Older reports eventually expire. On Vector Charts OEM, this value is configurable.
- User Votes: We expose an API to upvote or downvote user reports, which you can embed in your application.

## Displaying reports on the map

Enable the built-in user-report layers by adding `showUserReports=true` to the [Get Vector Style]({{< docsStyleDocs >}}) request:

<pre class="light">
const map = new mapboxgl.Map({
    style: "{{< docsApiHost >}}/api/v1/styles/base.json?token=&lt;token&gt;&showUserReports=true"
});
</pre>

When enabled, the style includes point report layers (icons and text) and bathymetry track layers (depth-banded line colors). The style requests bathymetry tiles by setting `includeBathymetry=true` on the MVT source.

## Querying reports directly

If you prefer not to use the built-in style layers, or need reports outside a map viewport, query the REST and tile endpoints directly:

- **[List Reports]({{< relref "list.md" >}})** - paginated JSON feed of all reports
- **[Get Reports (MVT)]({{< relref "tile-mvt.md" >}})** - Mapbox vector tiles with reports as point features
- **[Get Reports (GeoJSON)]({{< relref "tile-geojson.md" >}})** - GeoJSON tiles with reports as point features
- **[Upload Bathymetry]({{< relref "create-bathymetry.md" >}})** - upload depth soundings as tracks
- **[List Bathymetry Tracks]({{< relref "list-bathymetry.md" >}})** - paginated JSON feed of bathymetry track metadata
- **[Get Bathymetry Track]({{< relref "get-bathymetry.md" >}})** - full track including soundings

## Authentication

All user report endpoints are authenticated similarly to other API endpoints. To authenticate, provide a valid API token, either as a header or query parameter:

- `Authorization: Bearer <token>` header
- `?token=<token>` query parameter

<br/>
<hr/>
<br/>

## We Want Your Feedback

User Reports are a new feature. If you need any help, or have suggestions for how to improve the feature, please [Contact us](https://vectorcharts.com/contact-us/).

<br/>
<hr/>
<br/>
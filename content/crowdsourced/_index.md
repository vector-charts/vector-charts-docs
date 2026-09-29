---
title: "Overview"
weight: 1
---

![Crowdsourced bathymetry layer with reported depth details](/img/crowdsourced/2.png)

Official charts can be out of date in changing harbors, rivers, and creeks which are not mapped often. Crowdsourced reports help to fill those gaps and help make navigation safer.

The **Vector Charts Crowdsourced Data** program gives you a managed API to submit and display user reports in your application.

## How it works

1. Submit hazard and depth reports from your app via the Crowdsourced Data API.
2. We process the data and make it available back to your users (and the hydrographic community).
3. Show crowdsourced layers on any Vector Charts map using our API.

**Submission and display are both opt-in**. Try a live example in the [Vector Charts Demo App](https://app.vectorcharts.com/).

## Types of data

### Hazard reports

The [Hazard Report API](/crowdsourced/create/) lets users report ephemeral hazards such as debris, wrecks, or marine wildlife. Reports are displayed in Vector Charts as map points and can be upvoted or downvoted.

![Hazard report popup on a nautical chart](/img/crowdsourced/13.png)

### Bathymetry tracks

The [Bathymetry Report API](/crowdsourced/create-bathymetry/) accepts position and depth from sonar or similar devices. Soundings are displayed in Vector Charts as depth-shaded tracks.

![Depth soundings on a nautical chart](/img/crowdsourced/6.png)

## Displaying crowdsourced data on the map

Enable built-in layers with `showUserReports=true` on the [Get Vector Style]({{< docsStyleDocs >}}) request:

<pre class="light">
const map = new mapboxgl.Map({
    style: "{{< docsApiHost >}}/api/v1/styles/base.json?token=&lt;token&gt;&showUserReports=true"
});
</pre>

This adds hazard point layers and bathymetry track layers. You can also use the REST and tile endpoints directly (see the [Hazard Report API](/crowdsourced/create/) and [Bathymetry Report API](/crowdsourced/create-bathymetry/)).

## Getting started

1. Authenticate with a Vector Charts API token. See [Authentication](/crowdsourced/authentication/).
2. Submit hazard reports and/or depth soundings through the APIs.

<br/>
<hr/>
<br/>

## We Want Your Feedback

Crowdsourced Data is an evolving feature set. If you need any help, or have suggestions for how to improve it, please [Contact us](https://vectorcharts.com/contact-us/).

<br/>
<hr/>
<br/>

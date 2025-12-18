---
title: "Cloud API Overview"
weight: 1
menu:
  main:
    title: "Overview"
    parent: "getting_started"
---

![header](/img/13.png)

Welcome! The Vector Charts Cloud API provides nautical charts as vector tiles for display in modern web applications.

This documentation will walk you through how to setup your account, create an API token, and start using Vector Charts in your app.

## Prerequisites

We assume a basic familiarity with the concepts underlying web maps. A few topics you should be familiar with:
- [Tiled web map (Wikipedia)](https://en.wikipedia.org/wiki/Tiled_web_map) - Basic overview of how web map tiles are structured
- [Slippy map tilenames (OSM Wiki)](https://wiki.openstreetmap.org/wiki/Slippy_map_tilenames) - More explanation on tile coordinates
- [Vector tiles introduction (Mapbox)](https://docs.mapbox.com/data/tilesets/guides/vector-tiles-introduction/) - Overview of Vector Tiles as a modern format for transmitting map tiles as resolution-independent vector data.

Additionally, we assume that you have an application with an existing map SDK capable of rendering vector tiles.

If you are just experimenting, see our [Example Applications](/examples).

<br/>
<hr/>
<br/>

## Quick Start Guide

### 1. Create an Account

Follow the steps in [Creating an Account](/getting-started/creating-account/) to sign up for a Vector Charts account.

### 2. Create an API Token

Follow the steps in [API Tokens](/getting-started/tokens/) to create a token.

### 3. Add VectorCharts to your App

Use the vector tile URL in your map client:

<pre>
https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;token string&gt;
</pre>

For example, in Mapbox GL JS:
<pre>
const map = new mapboxgl.Map({
    ...
    style: "https://api.vectorcharts.com/api/v1/styles/base.json?token=&lt;token string&gt;"
});
</pre>

For more information on authentication and API endpoints, see the [API Reference](/api-reference/api-authentication/).

<br/>
<hr/>
<br/>

## Need Help?

If you need any help, or there's an issue with our docs, [Contact us](https://vectorcharts.com/contact-us/) or [Suggest an Edit](https://github.com/fullhexventures/vector-charts-docs/issues/new).

<br/>
<hr/>
<br/>
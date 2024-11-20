---
title: "Vector Charts Docs"
weight: 1
menu:
  main:
    title: "Overview"
    parent: "getting_started"
---

Welcome! 

VectorCharts is a web API for rendering Nautical Charts in web applications. 

Vector Charts uses Mapbox Vector Tiles technology to render beautiful, high resolution nautical chart data.

To get started, follow these links or the quickstart guide:

## 1. Create an Account

## 2. Create a Token

Create a token in your dashboard.

## 3. Add VectorCharts to your App

Use the vector URL in your client:

<pre>
https://vectorcharts.com/api/v1/tiles/{z}/{x}/{y}.png?token=<YOUR TOKEN HERE>
</pre>

Or, for older clients that only support raster tiles:

<pre>
https://vectorcharts.com/api/v1/tiles/{z}/{x}/{y}.png?token=<YOUR TOKEN HERE>
</pre>
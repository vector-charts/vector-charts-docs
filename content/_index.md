---
title: "Vector Charts Docs"
weight: 1
menu:
  main:
    title: "Overview"
    parent: "getting_started"
---

The Vector Charts API provides Nautical Charts as tiles for display in web maps. 

## Quick Start Guide

### 1. Create an Account

### 2. Create a Token

Create a token in your dashboard.

### 3. Add VectorCharts to your App

Use the vector URL in your client:

<pre>
https://vectorcharts.com/api/v1/tiles/{z}/{x}/{y}.png?token=<YOUR TOKEN HERE>
</pre>

Or, for older clients that only support raster tiles:

<pre>
https://vectorcharts.com/api/v1/tiles/{z}/{x}/{y}.png?token=<YOUR TOKEN HERE>
</pre>
---
title: "Crowdsourced Data API"
weight: 1
menu:
  crowdsourced:
    title: "Overview"
    parent: "getting_started"
    weight: 1
---

Crowdsourced data lets end users contribute location-based observations that other users can discover, validate, and act on. Vector Charts currently supports this through **user reports**: spatially-defined suggestions about chart data submitted at a specific latitude and longitude.

User reports are available on both **Vector Charts Cloud** and **Vector Charts OEM**. The REST API and WebSocket event format are the same on both platforms; only the base URL differs.

Each deployment is configured with a **namespace** (default `public`). All reports created on that instance belong to its namespace. When replicating between OEM peers, only reports in matching namespaces are exchanged.

## Base URLs

| Platform | Base URL |
|----------|----------|
| Cloud | `https://api.vectorcharts.com` |
| OEM | `https://<your-host>:9909` |

All paths in the [User Report API](/crowdsourced-data/user-report-api-reference/) are relative to the base URL for your deployment.

## What You Can Build

- Let users flag hazards, data quality issues, incidents, closures, or SOS situations on the chart
- Display nearby reports as GeoJSON tile overlays on a slippy map
- Let users vote reports up or down to surface consensus
- Receive streaming updates when reports are created, updated, deleted, or expired

## Next Steps

- [Submitting User Data](/crowdsourced-data/getting-started/submitting-user-data/) — integration patterns for client applications
- [Streaming Events](/crowdsourced-data/getting-started/streaming-events/) — WebSocket event format
- [User Report API](/crowdsourced-data/user-report-api-reference/) — endpoint reference

## Authentication

User report endpoints require a valid API token on both Cloud and OEM. See [Cloud authentication](/api-reference/api-authentication/) or the [OEM Core API overview](/oem/api-reference/) for how to pass tokens in headers or query parameters.

---
title: "Submitting User Data"
weight: 2
menu:
  crowdsourced:
    title: "Submitting User Data"
    parent: "getting_started"
    weight: 2
---

This guide covers the typical client workflow for crowdsourced user reports on Cloud and OEM.

## 1. Create a Report

When a user marks a location on the chart, call [Create User Report](/crowdsourced-data/user-report-api-reference/create/) with:

- **reportType** — category string (for example `hazard`)
- **position** — `{ latitude, longitude }` in WGS84 decimal degrees (request body only)
- **properties** (optional) — free-form JSON such as a description or heading
- **externalUserId** (optional) — your app's user identifier (not used for authorization)
- **id** (optional) — a client-generated UUID version 4 for offline-first sync

The server returns the report with vote counts initialized to zero. Reports expire after the configured `expirationAgeMs` (default 24 hours).

## 2. Display Reports on the Map

Fetch reports for the current viewport using [Get User Reports MVT Tile](/crowdsourced-data/user-report-api-reference/tile-mvt/). The vector chart style includes this source automatically and renders reports with an alert icon. Each point feature carries the full report attributes for popups and inspection.

For GeoJSON polling without the built-in style layer, use [Get User Reports Tile (GeoJSON)](/crowdsourced-data/user-report-api-reference/tile-geojson/).

For a global or paginated feed, use [List User Reports](/crowdsourced-data/user-report-api-reference/list/).

## 3. Vote on Reports

When a user confirms or disputes a report, call [Vote on User Report](/crowdsourced-data/user-report-api-reference/vote/) with `vote` set to `valid` or `invalid`. Each authenticated user may have at most one vote per report; submitting again updates the existing vote.

## 4. Delete Reports

The user who created a report (or an admin) can [Delete User Report](/crowdsourced-data/user-report-api-reference/delete/) to soft-delete it. Deleted reports are excluded from default list and tile queries.

## 5. Streaming Updates

Subscribe to [Streaming Events](/crowdsourced-data/getting-started/streaming-events/) at `/api/v1/realtime?token=<token>` to receive `event_user_report` messages when reports change, instead of polling list or tile endpoints.

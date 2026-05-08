---
title: "Styles"
weight: 5
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_styles"
---

A style is a named, reusable set of rendering parameters applied when generating chart tiles. Styles are referenced by ID through the [Core API](/oem/api-reference/) when fetching vector or raster tiles, allowing client applications to use a custom color palette or display settings without rebuilding the underlying chart data.

## Themes

Each style is created from a base theme that determines the default color palette. Three themes are available:

- `day`: Light palette intended for use in daylight conditions.
- `dusk`: Mid-tone palette intended for use at dusk or in low-light conditions.
- `night`: Dark palette intended for use at night.

The theme is set on creation. The resulting style's color palette and display settings can then be customized by updating the style's `parameters` object.

## Parameters

The `parameters` field is an object describing how the style renders. It contains two keys:

- `colors`: An object mapping color slot names to hex strings. Slot names are determined by the rendering engine.
- `settings`: An object containing display toggles, including:
    - `iconSet`: The name of the symbol set to use for chart features.
    - `soundingOpacity`: Opacity of depth soundings, between `0` and `1`.
    - `showLightSectors`: Whether to draw light sector arcs around lighthouses.

Other display settings may be added over time. Unknown keys in the `parameters` object are preserved.

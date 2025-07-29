---
title: "Theming"
weight: 5
menu:
  main:
    title: "Theming"
    parent: "getting_started"
---

The map style can be customized in a number of ways to fit into your branding & use case, or to set vehicle-specific parameters such as safety contour values.

There are two types of theming in the Vector Charts APIs:

- **Query Parameters**: Change user-specific options such as safety contours and day/night mode.
- **Custom Style**: Complete customization of all layers and color schemes to match your branding and choose which data is relevant to your use case.

## Query Parameters

The style returned using the [Get Vector Style](/api-reference/get-mvt/) endpoint has a limited set of options designed to change the style of the map at runtime.

The [Get Vector Style](/api-reference/get-mvt/) API page has a complete list of parameters.

### Depth Units

To change units for depth soundings, use the `depthUnits` parameter. The available options are `meters`, `feet`, and `fathoms`, and the default is `meters`. Depth soundings will update accordingly:

`
units=meters
`
![depth1](/img/units3.png)

`
units=feet
`
![depth2](/img/units4.png)

### Depth Limit

The `depthLimit` parameter controls the ENC safety contour and should be set to the depth considered safe for navigation by your vehicle.

For example, changing `depthLimit` to `1`, `3`, and `10`:

`
https://api.vectorcharts.com/api/v1/styles/base.json?token=<token>&depthLimit=1
`
![theming1](/img/14.png)


`
https://api.vectorcharts.com/api/v1/styles/base.json?token=<token>&depthLimit=3
`
![theming1](/img/15.png)

`
https://api.vectorcharts.com/api/v1/styles/base.json?token=<token>&depthLimit=10
`
![theming1](/img/16.png)

### Day & Night Theme

The `theme` parameter determines which color palette to use. Each stylesheet has a day, dusk and night color palette.

`
https://api.vectorcharts.com/api/v1/styles/base.json?token=<token>&theme=day
`
![theming1](/img/17.png)


`
https://api.vectorcharts.com/api/v1/styles/base.json?token=<token>&theme=dusk
`
![theming1](/img/18.png)

`
https://api.vectorcharts.com/api/v1/styles/base.json?token=<token>&theme=night
`
![theming1](/img/19.png)


## Custom Styles

Enterprise customers gain access to the Style Editor, which gives complete control over map layers & color palettes.

[Contact Us](https://vectorcharts.com/contact-us/) to learn more about custom styles.
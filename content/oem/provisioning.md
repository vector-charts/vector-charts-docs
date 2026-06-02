---
title: "Provisioning"
menu:
  oem:
    title: "Provisioning"
    parent: "getting_started"
    weight: 5
---

Some resources in Vector Charts, such as custom styles, would be typically be created interactively via the UI. It is possible to edit these resources using the APIs, documented later in this section.

Sometimes it is more convenient to set up these resources as static files, loaded and provisioned as the server starts up.

We refer to provisioning a resource in this manner as "provisioning".

## Setup

To provision resources, create folder named `provisioning` and bind-mount it the the container at the path `/home/vector-charts/provisioning`. For example, with Docker Compose:

## Provisioning Styles

To provision a style, add a style JSON file to `provisioning/styles/<style name>.json`. 

To obtain this style JSON, from the Style Editor tool (in either Cloud or OEM) go to Tools > Export Style JSON. The editor will export a JSON document which can be renamed and placed in the provisioning folder.

![Style Export](/img/style-export-1.png)

At startup, this style will be loaded. The style ID is dynamic, so to use this style, use the `styleName` query parameter, which looks up a style by name.
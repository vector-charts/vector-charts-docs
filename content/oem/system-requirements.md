---
title: "System Requirements"
menu:
  oem:
    title: "System Requirements"
    parent: "getting_started"
    weight: 2
---

Vector Charts OEM is designed to run on any desktop-tier computer.

**The primary requirement at this time is a container runtime** - OEM is distributed as a single Docker image.

The OEM software can run on both `x86-64` or `aarch64` architectures.

## Requirements

- *Required*: Modern desktop 64-bit CPU architecture (`x86-64` or `aarch64`)
- *Required*: 2GB or more of RAM
- *Required*: Docker or other container runtime
  - Tested: Linux w/ native Docker
  - Tested: Windows w/ Docker via WSL
  - Tested: MacOS w/ Docker Desktop
- *Required*: At least 20Gb of free disk space
  - *Recommended*: 50Gb of free disk space allocated for Vector Charts
- *Optional*: USB port available (For USB delivery of S-63 nautical charts)

## Limitations

At this time, Vector Charts cannot run on mobile devices or withour a container runtime environment. Vector Charts OEM is shipped as a monolithic container which combines several services (API, geospatial database) and can't be distributed to Android or iOS devices directly.

If this sounds like you, [contact our team](https://vectorcharts.com/contact-us) and we can discuss technical solutions.


<br/>

---

<br/>

[Next: Installation](/oem/installation)
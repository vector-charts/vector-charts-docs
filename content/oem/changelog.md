---
title: "Vector Charts OEM Changelog"
menu:
  oem:
    title: "Changelog"
    parent: "changelog"
    weight: 99
---

_History of latest OEM releases._

## Version 0.5.0
_Released June 2nd, 2026_

- x86_64 artifact: `402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.5.0-924f2b3-x86_64`
- aarch64 artifact: `402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.5.0-924f2b388-aarch64`

Various bugfixes and improvements to the OEM server.

- Exposed more [Administration APIs](/oem/portal-api-reference/admin/) for use in multitenant deployments: Create tokens for accounts, list tokens for accounts.
- Fixed encoding format of S-63 User Permit strings
- Updated license management to use more secure public/private key encryption
- Added ability to activate licenses while offline
- Added ability to remove a license from a server


## Version 0.4.1
_Released May 31st, 2026_

- x86_64 artifact: `402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.4.1-ead25fb-x86_64`
- aarch64 artifact: `402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.4.1-ead25fb6-aarch64`

This is the first public beta release of the Vector Charts OEM server. This release includes improved license management, an Administration API for multi-tenancy in the OEM server, and more.
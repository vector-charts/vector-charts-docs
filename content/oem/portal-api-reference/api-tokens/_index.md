---
title: "API Tokens"
weight: 3
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_api_tokens"
---

API tokens are long-lived bearer tokens used to authenticate Vector Charts API requests. They are typically issued to scripts, services, or front-end applications that need to call the Vector Charts API without a user logging in.

## Restrictions

A token may be created with optional restrictions that limit how it can be used. The restrictions schema currently supports a single field:

- **hosts**: An array of hostnames the token is allowed to be used from. The hostname is matched exactly against the `Origin` header of incoming requests. Useful for tokens embedded in a public web page where you want to limit where the token can be used.

A token without restrictions can be used from any origin.

## Endpoints

- [List API Tokens](/oem/portal-api-reference/api-tokens/list/)
- [Create API Token](/oem/portal-api-reference/api-tokens/create/)
- [Update API Token](/oem/portal-api-reference/api-tokens/update/)
- [Delete API Token](/oem/portal-api-reference/api-tokens/delete/)

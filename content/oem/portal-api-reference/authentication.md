---
title: "Authentication"
weight: 2
menu:
  oem:
    parent: "portal_api_reference"
    identifier: "portal_api_reference_authentication"
---

The Portal API accepts two kinds of bearer tokens, both sent in the `Authorization` header.

<pre>
Authorization: Bearer &lt;token string&gt;
</pre>

Either token type works on every Portal API endpoint.

## Session Tokens

A session token is obtained by exchanging a username and password at the [login endpoint](/oem/portal-api-reference/auth-login/). Session tokens are intended for the admin UI and short-lived scripts.

<pre>
POST https://&lt;your-host&gt;:9909/api/portal/v1/auth/login
Content-Type: application/json

{
    "username": "admin",
    "password": "admin"
}
</pre>

The response includes a `token` object whose `id` field is the bearer string:

<pre>
{
    "token": {
        "id": "f3a1c0d4e5b6a7c8d9e0f1a2b3c4d5e6",
        "userId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
    },
    "user": {
        "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "email": "admin",
        "isAdmin": true,
        "isAccountOwner": false,
        "account": {
            "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
            "name": "Default"
        }
    }
}
</pre>

Session tokens remain valid until they are explicitly invalidated via the [logout endpoint](/oem/portal-api-reference/auth-logout/).

## API Tokens

API tokens are long-lived tokens managed through the [API Tokens endpoints](/oem/portal-api-reference/). They are intended for headless integrations and CI/CD systems where storing user credentials is not appropriate.

The same API token can be used to authenticate against both the Portal API and the [Core API](/oem/api-reference/).

## Default Credentials

A new OEM instance is provisioned with a default administrator account.

- **Username:** `admin`
- **Password:** `admin`

Both values can be overridden at first startup with the `INITIAL_ADMIN_USERNAME` and `INITIAL_ADMIN_PASSWORD` environment variables. See [Configuration](/oem/configuration/) for details.

<span style="color:#9e6c2e"><b>For production deployments, change the default password immediately after first login.</b></span>

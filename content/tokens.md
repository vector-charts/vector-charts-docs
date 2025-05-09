---
title: "API Tokens"
weight: 4
menu:
  main:
    title: "API Tokens"
    parent: "getting_started"
---

The Vector Charts API uses tokens to manage authentication and track usage for billing. Each request must have a token associated with it.

Tokens are managed from the [Vector Charts Cloud dashboard](https://cloud.vectorcharts.com/).

## Creating a Token

To create a token, use the Create Token button on the dashboard homepage:

![token 1](/img/token3.png)

A dialog will open asking you to set properties for your token.

![token 1](/img/token5.png)

- Token Name (required): A display name to identify the token in the dashboard
- Scope (optional): List of hostnames that can use this token, see below.

After setting these options, click Create. 

The token will be shown for you to copy into your codebase. (You can also copy the token later from the main list.)

### Restricting a Token's Scope

Since tokens deployed with web applications are public, it's important to restrict their usage to domains which you control. This prevents someone from taking your token and reusing it.

The "Scope" property on Vector Charts tokens defines a list of hosts which are allowed to use the token:

![token 4](/img/token4.png)

An empty scope means the token can be used from any requesting host.

For example, to restrict the token to be used on the site [app.vectorcharts.com](https://app.vectorcharts.com/), you would enter:
<pre>
app.vectorcharts.com
</pre>

We recommend you create separate Development/Test and Production tokens, and set your development token to be restricted to `localhost`.

## Editing a Token

![token 1](/img/token2.png)

To edit a token, use the pencil icon next to the token list. The token dialog will
open again, and you can change the name and scope.

## Deleting a Token

![token 1](/img/token2.png)

To delete a token, use the red trashcan icon in the token list. This will delete the token.

Once a token is deleted, it can no longer be used.
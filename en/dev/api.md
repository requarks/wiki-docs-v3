---
title: API
description: Build automations by using the Wiki.js REST API
published: true
date: '2026-08-22T21:54:42.672Z'
tags:
  - admin
  - dev
editor: markdown
dateCreated: '2026-08-14T02:30:27.000Z'
---

# Overview

Your Wiki.js installation exposes a REST API at path `/_api`.

Open `https://wiki.example.com/_api` in your browser to see the list of all available endpoints and their parameters.

# API Keys

In the **Administration Area** :mdi:arrow-right: **API Access** page, click the **Enable API** button in the top-right corner to allow API tokens to be used.

> [!NOTE]
> Disabling the API doesn't turn off the API endpoints. It only prevents API keys from being used.

## Create API Key

1. In the **Administration Area** :mdi:arrow-right: **API Access** page, click the **New API Key** button in the top-right corner.
2. Enter a **name**, **expiration** and select the **group(s)** the key will inherit the permissions from. It's recommended to create a group with permissions tailored to your use of the API.
3. Copy the key value.

> [!WARNING]
> Make sure to save the key value in a safe place. It will not be shown again!

## Revoke an API Key

1. In the **Administration Area** :mdi:arrow-right: **API Access** page, click the **Revoke** button next to the key to revoke.
2. Upon confirmation, the key will no longer be usable.

> [!TIP]
> - Revoked keys can be purged from the [Utilities](/admin/utilities) admin page.
> - All keys can be instantly invalidated from the [Utilities](/admin/utilities) admin page.

# Usage

To authenticate your requests, add a `X-API-Key` header with the key value. e.g.:

```yaml
X-API-Key: eyJhbGciOi...
```

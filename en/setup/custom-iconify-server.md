---
title: Custom Iconify Server
description: How to setup your own Iconify server
published: true
date: '2026-11-15T02:15:56.801Z'
tags: []
editor: markdown
dateCreated: '2026-11-15T02:15:56.801Z'
---

# Overview

You may want to run your own instance of the [Iconify API server](https://iconify.design/docs/api/hosting.html) in the following use cases:
- for use in an offline environment
- to use your own private icon sets

By default, Wiki.js calls the public `api.iconify.com` endpoint to search and fetch icons. You can override this endpoint by setting the `icons.apiUrl` parameter in your `config.yml` or using the `ICONIFY_API_URL` environment variable when using the docker image.

# Setup

There [multiple options](https://iconify.design/docs/api/hosting.html) for running an Iconify API server.

## Download Icon Sets

All public icon sets can be downloaded from:
https://github.com/iconify/icon-sets/tree/master/json

It's recommended to download at least the following sets:
- `la.json`
- `mdi.json`

## Example Docker Compose

The following example includes both Wiki.js and an Iconify server.

For the **iconify** container:
- The `ICONIFY_SOURCE` env var must be set to `none` in an offline environment.
- It assumes a folder at path `/wiki/icons` on the host, containing the necessary icon sets.

For the **wiki** container:
- The `ICONIFY_API_URL` env var is added to the `wiki` definition to point to the Iconify server.

```yaml title="compose.yaml" linesHighlight="13-19,31"
services:

  db:
    image: postgres:18
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql

  iconify:
    image: iconify/api:3.2.0
    environment:
      ICONIFY_SOURCE: none
    restart: unless-stopped
    volumes:
      - /wiki/icons:/data/iconify-api/icons

  wiki:
    image: ghcr.io/requarks/wiki:3.3.1
    depends_on:
      - db
      - iconify
    environment:
      DB_HOST: db
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
      ICONIFY_API_URL: http://iconify:3000
    restart: unless-stopped
    ports:
      - "80:3000"
    volumes:
      - /wiki/config.yml:/wiki/config.yml

volumes:
  db-data:
```


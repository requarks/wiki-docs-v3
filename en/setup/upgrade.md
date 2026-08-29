---
title: Upgrade
description: How to upgrade to the latest version
published: true
date: '2026-08-24T00:22:32.017Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-08-11T05:04:17.122Z'
---

> [!IMPORTANT]
> While upgrades are generally safe and it's very unlikely that it would result in data loss, **it's your responsibility to have a proper backup of your database before performing an upgrade**. Note that it's not possible to go back to a previous version of Wiki.js once the database schema has been upgraded.

# In-place upgrade

:::block-tabs
::block-tab{label="Docker" header="2"}
#### Standalone Container

Upgrading is simply a matter of recreating the container with the latest image version:

```bash
# Stop and remove container named "wiki"
docker stop wiki
docker rm wiki

# Pull latest image of Wiki.js
docker pull ghcr.io/requarks/wiki:3.0.0-alpha

# Create new container of Wiki.js based on latest image
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_HOST=db" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:3.0.0-alpha
```

Check out the [Docker installation guide](/setup/installation#environment-variables) for all the possible options when creating a Wiki.js container.

#### Docker Compose

The following commands will pull the latest image and recreate the containers defined in the [docker-compose](/setup/installation#docker-compose) file:

```bash
docker compose pull wiki
docker compose up --force-recreate -d
```
::

::block-tab{label="Kubernetes" header="2"}
*Coming soon*
::

::block-tab{label="Linux" header="2"}
*Coming soon*
::

::block-tab{label="macOS" header="2"}
*Coming soon*
::

::block-tab{label="Windows" header="2"}
*Coming soon*
::
:::

# Upgrade from 2.x

*Coming soon*

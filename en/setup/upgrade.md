---
title: Upgrade
description: How to upgrade to the latest version
published: true
date: '2026-09-23T17:51:18.189Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-08-11T05:04:17.122Z'
---

> [!IMPORTANT]
> While upgrades are generally safe and it's very unlikely that it would result in data loss, **it's your responsibility to have a proper backup of your database before performing an upgrade**. Note that it's not possible to go back to a previous version of Wiki.js once the database schema has been upgraded.

# In-place upgrade

:::block-tabs
::block-tab{label="Docker" header="2" icon="mdi:docker"}
#### Standalone Container

Upgrading is simply a matter of recreating the container with the latest image version:

```bash
# Stop and remove container named "wiki"
docker stop wiki
docker rm wiki

# Pull latest image of Wiki.js
docker pull ghcr.io/requarks/wiki:3.0.0-beta

# Create new container of Wiki.js based on latest image
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_HOST=db" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:3.0.0-beta
```

Check out the [Docker installation guide](/setup/installation#environment-variables) for all the possible options when creating a Wiki.js container.

#### Docker Compose

The following commands will pull the latest image and recreate the containers defined in the [docker-compose](/setup/installation#docker-compose) file:

```bash
docker compose pull wiki
docker compose up --force-recreate -d
```
::

::block-tab{label="Kubernetes" header="2" icon="mdi:kubernetes"}
*Coming soon*
::

::block-tab{label="Linux" header="2" icon="mdi:linux"}
*Coming soon*
::

::block-tab{label="macOS" header="2" icon="mdi:apple"}
*Coming soon*
::

::block-tab{label="Windows" header="2" icon="mdi:microsoft-windows"}
*Coming soon*
::
:::

# Upgrade from 2.x

Because of the major differences between 2.x and 3.x, an in-place upgrade is not possible. Instead, a migration process is provided to easily transfer all data between your old 2.x installation and a new 3.x installation.

::block-steps
1. **Create a .wkbackup migration package**
    1. Upgrade your Wiki.js 2.x installation to the latest version.
    2. Under **Administration Area** :la:arrow-right: **Utilities**, click the **Export for Wiki.js 3.x** tool.
    3. Leave all checkboxes checked and click the **Create Package** button.
    4. Download the package upon completion.

2. **Install Wiki.js 3.x**
    1. Install a new Wiki.js 3.x instance using the [installation instructions](/setup/installation).
    2. Login using the root administrator account.
    3. On the welcome screen, click the **Administration Area** button.
    4. Go to **Utilities** and click **Proceed** next to the **Import from Wiki.js 2.x** utility.

3. **Import the migration package**
    1. Leave all options to their defaults, and browse to your .wkbackup file you downloaded earlier by clicking the **Select archive...** button.
    2. Click the **Start Import** button to begin the import.
    3. Follow the progress on the right. Look out for any error.
    4. Review site settings and system configuration to ensure everything matches your expectations.

> [!IMPORTANT]
> Some settings are deliberatly **NOT** imported:
> - Module settings *(like storage, authentication, comments, analytics, etc.)* to avoid unwanted conflicts with your old Wiki.js 2.x installation.
> - Security settings because of potential differences in behavior.
> - Site logo, as it's uploaded rather than linked externally in 3.x.
> - Site hostname to avoid locking you out of your new installation by pointing to the 2.x installation hostname.

> [!TIP]
> The import is idempotent and can safely be performed multiple times. Existing items will be skipped unless the **Overwrite on conflict** option is checked.
::


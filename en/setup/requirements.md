---
title: Requirements
description: Prerequisites to install Wiki.js
published: true
date: '2026-08-25T05:27:57.400Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-08-10T07:51:02.986Z'
---

# Server

Wiki.js runs on virtually any system where Node.js is supported.
This means it runs on **Linux**, **macOS**, **Windows** as well as container solutions such as **Docker** / **Kubernetes**.

> [!TIP]
> It's highly recommended to run Wiki.js using **Docker**. It includes all necessary dependencies *(minus the database)* and provides the easiest ugprade path.

:::block-tabs
::block-tab{label="Recommended Specs" header="2"}

### CPU
Wiki.js runs perfectly fine on a single CPU core. However, **2 cores or more are recommended** to fully make use of the background workers. Workers are responsible for maintenance tasks, updates, webhooks, search index rebuild, final page render, etc.

### Memory
Linux systems should have **at least 1GB of RAM** to run Wiki.js. Windows and macOS systems usually require a bit more RAM.

### Disk
Storage requirements are based on the content you will enter. Wikis that consists almost exclusively of text are not likely to exceed a few megabytes. However, as soon as you upload images, videos or other files, you should plan your storage requirements accordingly.

**At least 1 GB of storage** dedicated to Wiki.js is recommended.

::

::block-tab{label="Internet Access" header="2"}

Wiki.js requires internet access to perform certain functions. If you block all connections by default via a firewall, you must ensure the following are allowlisted:

### Inbound Connections

Wiki.js listens over HTTP / WebSockets on the port you defined in the `config.yml` file (`3000` by default).

### Outbound Connections

The following endpoints called by Wiki.js for various functions:

| Endpoint | Port | Reason |
| :-- | :-- | :-- |
| `api.github.com` | `443` (HTTPS) | Check for new versions / updates |
| `github.com` | `443` (HTTPS) | Fetch locales metadata and strings |
| `api.iconify.design` | `443` (HTTPS) | Fetch and search icon sets |

> [!IMPORTANT]
> In addition to the endpoints above, you must also allow the endpoints required for the authentication and storage modules you enable. Refer the each module documentation for the endpoints to allow.
::
:::

# Hostname

Wiki.js requires a dedicated sub-domain / domain *(e.g. `wiki.example.com`)*.

> [!WARNING]
> You **CANNOT** install Wiki.js to a sub-folder *(e.g. `/wiki/` )* on an existing hostname. This use case is **NOT** supported and [will not be](/admin/faq#why-are-sub-folder-installations-not-supported).

# Database

Wiki.js requires a [PostgreSQL](https://www.postgresql.org) database. It is not part of Wiki.js and it will not be installed for you. You're expected to provide an empty database for Wiki.js to use, and preferably a unique user / pass to connect to it.

Supported versions:

- **PostgreSQL 18**
- **PostgreSQL 17**
- **PostgreSQL 16**

> [!NOTE]
> The `ltree` and `pg_trgm` extensions must be available in your PostgreSQL installation. These extensions are usually included by default in most installations. The official PostgreSQL docker image already includes them.

# Node.js

The [Node.js](https://nodejs.org/) runtime is required and must be installed on the system *(unless using the Docker container image, in which case it is already included)*.

Supported versions:

- **Node.js 26**

> [!WARNING]
> Earlier versions of Node.js are **NOT** compatible and will **NOT** work. It requires various features introduced in Node.js 26.

# Supported Browsers

The following browsers are supported:

- Google Chrome *(including Android version)*
- Mozilla Firefox
- Apple Safari *(including iOS version)*

> [!NOTE]
> Only the latest stable version of these browsers are supported.

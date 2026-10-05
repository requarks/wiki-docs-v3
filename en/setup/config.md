---
title: Configuration Reference
description: Detailed configuration options for Wiki.js
published: true
date: '2026-10-05T00:06:51.539Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-10-04T23:14:51.519Z'
---

Configuration parameters that are specific to a local instance are defined in a `config.yml` file. All other settings are defined via the [Administration Area](/admin/dashboard).

| Parameter | Description | Default Value |
| :-- | :-- | :-- |
| port | The port to listen on. | `3000` |
| db.host | Hostname or IP address of the PostgreSQL database. | `localhost` |
| db.port | Port of the PostgreSQL database. | `5432` |
| db.user | Username to connect to the PostgreSQL database. | `postgres` |
| db.pass | Password to connect to the PostgreSQL database | `postgres` |
| db.db | PostgreSQL database name to connect to. | `wiki` |
| db.schema | PostgreSQL schema to use. | `wiki` |
| db.ssl | Whether to use SSL to connect to the PostgreSQL database. | `false` |
| db.sslOptions | Any of the TLS options from https://nodejs.org/api/tls.html#tls_tls_createsecurecontext_options | `{ auto: true }` |
| bindIP | The network interface IP to listen on. Use 0.0.0.0 to listen on all. | `0.0.0.0` |
| logLevel | The severity level for logging (error, warn, info or debug) | `info` |
| logFormat | Output format for logging (default or json) | `default` |
| offline | Skips all automated internet calls (updates, locales and icons fetch) when true. | `false` |
| dataPath | Writable data path used for cache, temporary user uploads, etc.<br>**You should not backup this directory.** <br>Everything is stored in the database unless you explicitly use a local path for content storage via the **Administration Area** :la:arrow-right: **Storage** page. | `./data` |
| icons.apiUrl | Iconify API to use for icons lookup. | `https://api.iconify.design` |
| bodyParserLimit | Maximum size of API requests body that can be parsed, in bytes. Does not affect file uploads. | `5242880` *(5mb)* |
| scheduler.workers | Leave 'auto' for one fewer than the CPUs available to the process (if higher than 1). | `auto` |
| pool | Any PostgreSQL connection pool options from https://node-postgres.com/apis/pool | `{}` |
{.table-leading-col}


---
title: Configuration Reference
description: Detailed configuration options for Wiki.js
published: true
date: '2026-10-05T01:57:40.489Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-10-04T23:14:51.519Z'
---

Configuration parameters that are specific to a local instance are defined in a `config.yml` file. All other settings are defined via the [Administration Area](/admin/dashboard).

# Reference

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
| bindIP | The network interface IP to listen on. Use `0.0.0.0` to listen on all. | `0.0.0.0` |
| logLevel | The severity level for logging (`error`, `warn`, `info` or `debug`) | `info` |
| logFormat | Output format for logging (`default` or `json`) | `default` |
| offline | Skips all automated internet calls (updates, locales and icons fetch) when true. For use when your instance cannot connect to the internet. | `false` |
| dataPath | Writable data path used for cache, temporary user uploads, etc.<br>**You should not backup this directory.** <br>Everything is stored in the database unless you explicitly use a local path for content storage via the **Administration Area** :la:arrow-right: **Storage** page. | `./data` |
| icons.apiUrl | Iconify API to use for icons lookup. | `https://api.iconify.design` |
| bodyParserLimit | Maximum size of API requests body that can be parsed, in bytes. Does not affect file uploads. | `5242880` *(5mb)* |
| scheduler.workers | The maximum number of workers that can be used for background tasks. Use `auto` for one fewer than the CPUs available to the process (if higher than 1). | `auto` |
| pool | Any PostgreSQL connection pool options from https://node-postgres.com/apis/pool | `{}` |
{.table-leading-col}

# Env Variables Interpolation

Any value can be replaced with `$(ENV_NAME)` to be interpolated at runtime with an environment variable. A default value can also be provided using the `$(ENV_NAME:default_value)` syntax.

### Example

Using the following `config.yml` example:
```yaml
db:
  host: '$(DB_HOST)'
  port: $(DB_PORT)
  user: '$(DB_USER:wiki)'
  pass: '$(DB_PASS)'
```
and the following environment variables:
- DB_HOST=db.example.com
- DB_PORT=5432
- DB_PASS=secret
{.grid-list}

would result in the following config being used at runtime:
```yaml
db:
  host: 'db.example.com'
  port: 5432
  user: 'wiki'
  pass: 'secret'
```

# Sample Config File

The latest version of the complete sample config file can be found on [GitHub](https://github.com/requarks/wiki/blob/scarlett/config.sample.yml).

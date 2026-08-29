---
title: Icons
description: Choose which icon sets can be used across the wiki
published: true
date: '2026-08-20T07:07:07.691Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-14T08:07:53.354Z'
---

# Overview

# Icon Sets

# Storage

Content references an icon by name, e.g. `mdi:account-edit`. The first time an icon is used it is fetched from [Iconify](https://icon-sets.iconify.design) and saved to the database permanently. Once stored, an icon is served by the wiki, never from Iconify.

Users never connect to the Iconify API directly. All requests are made by the server.

Icons are cached in memory and on disk, both which can be purged at any time.

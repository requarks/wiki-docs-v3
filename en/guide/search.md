---
title: Search
description: Search across all pages and filter results
published: true
date: '2026-11-07T04:27:47.784Z'
tags: []
editor: markdown
dateCreated: '2026-08-27T06:17:53.011Z'
---

# Overview

*Documentation coming soon*

# Language-specific Configs

Some languages may require extra configuration / extensions to support full-text search.

## Chinese

::block-steps
1. Install [zhparser](https://github.com/amutu/zhparser). The official postgres image doesn't include it.
2. Create the config in your database:
    ```sql title="SQL"
    CREATE EXTENSION zhparser;
    CREATE TEXT SEARCH CONFIGURATION chinese (PARSER = zhparser);
    ALTER TEXT SEARCH CONFIGURATION chinese ADD MAPPING FOR n,v,a,i,e,l WITH simple;
    ```
3. In Wiki.js, under the **Administration Area** :la:arrow-right: **Search Engine** page, add the following to the **PostgreSQL Dictionary Mapping Overrides** field:
    ```json title="JSON"
    {"zh": "chinese"}
    ```
4. Click **Apply**.
5. Click **Rebuild Index**.
::


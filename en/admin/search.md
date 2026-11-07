---
title: Search Engine
description: Configure the search capabilities of your wiki
published: true
date: '2026-11-07T11:01:48.828Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-17T19:13:48.304Z'
---

# Overview

Wiki.js has a powerful search engine to quickly find what you're looking for across your wiki. It relies on PostgreSQL's pg_trgm extension for trigram text matching.

# Parameters

| Parameter | Description | Default |
| :-- | :-- | :-- |
| Enable Term Highlighting | Whether to show the highlighted terms in search results. There is a slight performance impact when enabled. | `True` |
| PostgreSQL Dictionary Mapping Overrides | JSON object of 2 letters locale codes and their PostgreSQL dictionary association to override. Built-in PostgreSQL languages do not need to be defined here and are automatically mapped. | `{}` |
{.table-leading-col}

# Operations

- Click the **Rebuild Index** button in the top-right corner to fully rebuild the search index. This should only be done for maintenance / fixing errors, as this is done automatically as content change.

# Additional Configs

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
    {
      "zh": "chinese"
    }
    ```
4. Click **Apply**.
5. Click **Rebuild Index**.
::


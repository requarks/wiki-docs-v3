---
title: Search Engine
description: Configure the search capabilities of your wiki
published: true
date: '2026-08-20T07:07:43.731Z'
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
| PostgreSQL Dictionary Mapping Overrides | JSON object of 2 letters locale codes and their PostgreSQL dictionary association. | `{ "en": "english" }` |
{.table-leading-col}

# Operations

- Click the **Rebuild Index** button in the top-right corner to fully rebuild the search index. This should only be done for maintenance / fixing errors, as this is done automatically as content change.

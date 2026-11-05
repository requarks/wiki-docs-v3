---
title: Support zhparser for improved Chinese full-text search
description: >-
  Wiki.js 3 uses PostgreSQL full-text search and selects a text search
  configuration based on each page’s locale. Chinese locales are not included in
  the default language mappings and fall back to Post…
published: true
date: '2026-11-05T09:44:10.101Z'
tags:
  - search
editor: markdown
dateCreated: '2026-11-05T02:36:43.457Z'
---

Wiki.js 3 uses PostgreSQL full-text search and selects a text search configuration based on each page’s locale. Chinese locales are not included in the default language mappings and fall back to PostgreSQL’s `simple` configuration, which does not provide Chinese word segmentation. This can make it difficult to find relevant pages by individual Chinese terms.

Support using a PostgreSQL text search configuration backed by [zhparser](https://github.com/amutu/zhparser) for Chinese locales, please.

Wiki.js already supports per-locale text search configuration overrides and rebuilding the search index. It would be helpful to verify that these features work correctly with zhparser and provide guidance on:

- Installing zhparser and creating a PostgreSQL text search configuration.
- Mapping Chinese locales to that configuration in Wiki.js.
- Rebuilding existing page search vectors after changing the mapping.
- Ensuring that both indexing and full-text queries use the selected configuration.

This could improve Chinese full-text search without requiring a separate search service.

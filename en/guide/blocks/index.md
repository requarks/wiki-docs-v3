---
title: Index
description: Displays a list of pages contained in a folder.
published: true
date: '2026-08-17T00:02:37.227Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:32:43.304Z'
---

# Description

Displays a list of pages contained in a folder.

# Demo

::block-index{path="guide/blocks" limit="4" showIcons="true"}
::

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `path` | `<none>` | Path without leading or trailing slashes, e.g. `foo/bar` |
| `tags` | `<none>` | Comma-separated list, e.g. `abc,xyz` |
| `limit` | `10` | `-` |
| `orderBy` | `title` | `title`, `fileName`, `createdAt`, `updatedAt` |
| `orderByDirection` | `asc` | `desc`, `asc` |
| `depth` | `0` | `-` |
| `showIcons` | `false` | `true`, `false` |
| `noResultMsg` | `No pages matching your query.` | `-` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-index
::
````

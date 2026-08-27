---
title: Include
description: Transclude the contents of another page inside this one.
published: true
date: '2026-08-17T00:01:10.287Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:33:50.203Z'
---

# Description

Transclude the contents of another page inside the current one.

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `path` | `<required>` | Path without leading or trailing slashes, e.g. `foo/bar` |
| `locale` | `<none>` | Locale code, e.g. `en` |
| `showTitle` | `true` | `true`, `false` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-include{path="foo/bar"}
::
````


---
title: Kroki
description: >-
  Draws a diagram through a Kroki server — Graphviz, D2, BPMN, Vega,
  Structurizr, TikZ and two dozen more.
published: true
date: '2026-08-16T23:58:05.201Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T18:59:13.175Z'
---

# Description

Draws a diagram through a Kroki server — Graphviz, D2, BPMN, Vega, Structurizr, TikZ and two dozen more.

# Demo

::block-kroki
```kroki
digraph G {
  Hello -> World
}
```
::

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `type` | `graphviz` | *see dropdown list* |
| `server` | `https://kroki.io` | `-` |
| `format` | `svg` | `svg`, `png` |
| `caption` | `<none>` | `-` |
| `align` | `left` | `left`, `center` |
{.table-leading-col .table-code-nohighlight}

# Body

The body consists of a **Kroki** code block.

Check out the [Kroki Reference](https://kroki.io/) for more details.

# Default Code

````md
::block-kroki
```kroki
digraph G {
  Hello -> World
}
```
::
````

---
title: KaTeX
description: >-
  Typesets a TeX formula with KaTeX, including chemical equations written with
  mhchem.
published: true
date: '2026-08-17T00:03:35.552Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:42:41.431Z'
---

# Description

Typesets a TeX formula with KaTeX, including chemical equations written with mhchem — `\ce{}` and `\pu{}`.

# Demo

::block-katex{align="left"}
```latex
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
```
::

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `caption` | `<none>` | `-` |
| `align` | `center` | `center`, `left` |
{.table-leading-col .table-code-nohighlight}

# Body

The body consists of a **latex** code block.

Check out the [KaTeX reference](https://katex.org/).

# Default Code

````markdown
::block-katex
```latex
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
```
::
````

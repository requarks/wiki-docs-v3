---
title: MathJax
description: Typesets a TeX formula, including chemical equations written with mhchem
published: true
date: '2026-08-17T00:05:19.831Z'
tags: []
editor: markdown
dateCreated: '2026-08-13T04:54:57.095Z'
---

# Description

Typesets a TeX formula, including chemical equations written with mhchem — `\ce{}` and `\pu{}`.

# Demo

::block-mathjax{align=left}
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

# Default Code

````md
::block-mathjax
```latex
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
```
::
````


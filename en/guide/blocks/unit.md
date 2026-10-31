---
title: Measurement
description: >-
  A distance, weight, volume, speed or temperature in a line of text, shown in
  the reader's own units.
published: true
date: '2026-10-31T07:21:25.635Z'
tags:
  - blocks
editor: markdown
dateCreated: '2026-10-31T07:21:25.635Z'
---

# Description

A distance, weight, volume, speed or temperature in a line of text, shown in the reader's own units.

# Demo

This :block-unit[10 km] measurement should be in your preferred unit. You can always mouse over to see the other unit system.

You can also show both :block-unit[450 F]{show="both"} at once!

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `show` | `reader` | `reader` or `both` |
| `system` | `auto` | `auto`, `metric` or `imperial` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
:block-unit[10 km]
````


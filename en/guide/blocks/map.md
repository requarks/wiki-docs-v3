---
title: Map
description: Shows a location on an OpenStreetMap map.
published: true
date: '2026-08-17T00:05:01.878Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:20:55.834Z'
---

# Description

Shows a location on an OpenStreetMap map.

# Demo

::block-map{lat="45.5019" lon="-73.5674" label="Montréal"}
::

# Parameters

| Parameter | Default Value | Example Value |
| :-- | :-- | :-- |
| `lat` | `<required>` | Latitude floating-point number, e.g. `45.5019` |
| `long` | `<required>` | Longitude floating-point number, e.g. `-73.5674` |
| `zoom` | `13` | `-` |
| `height` | `400` | Number of pixels |
| `label` | `<none>` | `-` |
| `theme` | `auto` | `auto`, `light`, `dark` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-map{lat="45.5019" lon="-73.5674"}
::
````


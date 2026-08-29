---
title: PlantUML
description: >-
  Draws a PlantUML diagram — sequence, class, state, activity, mindmap, gantt
  and the rest.
published: true
date: '2026-08-14T07:07:01.160Z'
tags: []
editor: markdown
dateCreated: '2026-08-13T04:48:57.463Z'
---

# Description

Draws a PlantUML diagram — sequence, class, state, activity, mindmap, gantt and the rest.

# Demo

::block-plantuml
```plantuml
@startuml
Alice -> Bob : hello
Bob --> Alice : hi
@enduml
```
::

# Parameters

| Parameter | Default Value | Example Value |
| :-- | :-- | :-- |
| `server` | `https://www.plantuml.com/plantuml` | `https://www.plantuml.com/plantuml` |
| `format` | `svg` | `svg` or `png` |
| `caption` | `<none>` | `Some caption` |
| `align` | `left` | `center` or `left` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-plantuml
```plantuml
@startuml
Alice -> Bob : hello
Bob --> Alice : hi
@enduml
```
::
````


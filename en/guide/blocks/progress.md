---
title: Progress
description: >-
  A small progress bar in a line of text, from a percentage or a count like
  7/10.
published: true
date: '2026-10-31T07:24:59.396Z'
tags:
  - blocks
editor: markdown
dateCreated: '2026-10-31T07:24:59.396Z'
---

# Description

A small progress bar in a line of text, from a percentage or a count like 7/10.

# Demo

- Project ABC is :block-progress[70%] completed.
- Project DEF is only :block-progress[30%]{color="warning"} done.

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `color` | `primary` | `primary`, `positive`, `negative`, `warning`, `info` or `grey` |
| `label` | `percentage` | `percentage`, `value` or `none` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
:block-progress[50%]
````


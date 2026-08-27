---
title: Terminal Recording
description: Plays an asciinema recording — a .cast file — in a terminal player.
published: true
date: '2026-08-14T07:08:42.705Z'
tags: []
editor: markdown
dateCreated: '2026-08-13T04:21:06.220Z'
---

# Description

Plays an asciinema recording — a .cast file — in a terminal player.

# Demo

::block-asciinema{src="https://asciinema.org/a/756853.cast"}
::

# Parameters

| Parameter | Default Value | Example Value |
| :-- | :-- | :-- |
| `src` | `<required>` | `https://asciinema.org/a/756853.cast` |
| `theme` | `asciinema` | `asciinema`, `dracula`, `gruvbox-dark`, `monokai`, `nord`, `seti`, `solarized-dark`, `solarized-light` or `tango` |
| `autoPlay` | `false` | `false` |
| `loop` | `false` | `false` |
| `speed` | `1` | `1` |
| `idleTimeLimit` | `<none>` | `60` |
{.table-leading-col .table-code-nohighlight}

# Default Code

```md
::block-asciinema{src="https://asciinema.org/a/756853.cast"}
::
```

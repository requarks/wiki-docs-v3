---
title: Keyboard Shortcut
description: >-
  A keyboard shortcut in a line of text, drawn as keys for the reader's own
  keyboard.
published: true
date: '2026-10-31T07:15:33.060Z'
tags:
  - blocks
editor: markdown
dateCreated: '2026-10-31T07:15:33.060Z'
---

# Description

A keyboard shortcut in a line of text, drawn as keys for the reader's own keyboard.

# Demo

This :block-kbd[Ctrl+Alt+S] keyboard shortcut will show in your system own keyboard layout, while :block-kbd[Ctrl+Alt+S]{platform="mac"} will always show the Mac layout and :block-kbd[Ctrl+Alt+S]{platform="pc"} the Windows/Linux PC layout.

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `platform` | `auto` | `auto` *(the reader's platform)*, `mac`, `pc`, or `none` *(as written)* |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
:block-kbd[Ctrl+S]
````


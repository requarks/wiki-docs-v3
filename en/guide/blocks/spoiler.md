---
title: Spoiler
description: Hides content behind a cover until it is clicked.
published: true
date: '2026-08-14T07:07:55.710Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:10:41.378Z'
---

# Description

The spoiler block hides content behind a "Spoiler" panel. The hidden content is shown upon clicking on the block.

# Demo

::block-spoiler
Super **secret** content that should never be seen!

:scream:
::

# Parameters

| Parameter | Default Value |
| :-- | :-- |
| `label` | `Spoiler` |
| `hint` | `Click to show content` |
{.table-leading-col .table-code-nohighlight}

# Body

The body should consists of standard Markdown content.

# Default Code

```markdown
::block-spoiler
The content to hide.
::
```


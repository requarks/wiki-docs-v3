---
title: Youtube Player
description: Embeds a YouTube video.
published: true
date: '2026-08-17T00:20:24.598Z'
tags: []
editor: markdown
dateCreated: '2026-08-17T00:14:21.473Z'
---

# Overview

Embeds a YouTube video.

# Demo

::block-youtube{url="https://youtu.be/RMveiKaXtQw" width="640"}
::

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `url` | `<required>` | Youtube URL (watch, youtu.be or shorts link)  |
| `width` | `<none>` | Number in pixels or empty to fill available page width |
| `height` | `<none>` | Number in pixels or empty to keep the video ratio |
| `autoplay` | `false` | `true`, `false`. Setting to `true` will automatically mute the video. |
| `controls` | `true` | `true`, `false` |
| `fs` | `true` | `true`, `false`. Whether to allow full screen or not. |
| `loop` | `false` | `true`, `false` |
| `start` | `0` | Seconds into the video to start at. `0` uses the time in the URL, if it carries one. |

{.table-leading-col .table-code-nohighlight}

# Default Code

```markdown
::block-youtube{url="https://youtu.be/RMveiKaXtQw"}
::
```


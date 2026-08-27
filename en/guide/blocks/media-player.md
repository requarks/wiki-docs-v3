---
title: Media Player
description: Plays an audio or video file inline.
published: true
date: '2026-08-17T00:07:16.479Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:48:32.294Z'
---

# Description

Plays an audio or video file inline.

## Supported URLs
- Video files (mp4, webm, etc.)
- Audio files (mp3, ogg, etc.)

> [!WARNING]
> **You CANNOT play Youtube videos using this block.** Use the [Youtube](youtube) content block instead.

# Demo

::block-media-player{src="https://github.com/bower-media-samples/big-buck-bunny-480p-30s/raw/refs/heads/master/video.mp4"}
::

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `src` | `<required>` | Path or URL to video/audio file, e.g. `https://example.com/video.mp4` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-media-player{src="https://example.com/video.mp4"}
::
````


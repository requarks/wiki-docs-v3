---
title: Image Gallery
description: Displays a grid of images, each opening full size in a lightbox.
published: true
date: '2026-08-17T00:00:03.276Z'
tags: []
editor: markdown
dateCreated: '2026-08-14T23:57:05.026Z'
---

# Overview

Displays a grid of images, each opening full size in a lightbox.

# Demo

::block-gallery
- /guide/images/wallpapers-demo/phil-desforges-tmc0w_lenge-unsplash.jpg
- /guide/images/wallpapers-demo/david-white-cmabvujdlms-unsplash.jpg
- /guide/images/wallpapers-demo/matthias-mullie-vaxchgjvz0g-unsplash.jpg
- /guide/images/wallpapers-demo/shayan-ghiasvand-k-zf0vbpcwg-unsplash.jpg
- /guide/images/wallpapers-demo/steven-wright-cbogtt3iltm-unsplash.jpg
- /guide/images/wallpapers-demo/the-bialons-8oazllgprso-unsplash.jpg
::

# Properties

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `thumbnailSize` | `180` | `-` |
| `fit` | `cover` | `cover`, `contain` |
{.table-leading-col .table-code-nohighlight}

# Body

The body consists of a list of image paths or URLs.

- Paths can be relative (e.g. `/images/photo.jpg`) or absolute URLs (e.g. `https://example.com/photo.jpg`).
- Paths can be optionally prefixed with a dash for code readability.

# Default Code

```md
::block-gallery
- https://example.com/photo-1.jpg
- https://example.com/photo-2.jpg
::
```


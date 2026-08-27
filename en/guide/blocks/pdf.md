---
title: PDF Viewer
description: Displays a PDF document in a viewer, page by page.
published: true
date: '2026-08-14T20:34:53.975Z'
tags: []
editor: markdown
dateCreated: '2026-08-14T20:15:33.222Z'
---

# Overview

Displays a PDF document in a viewer, page by page.

# Demo

::block-pdf{src="https://raw.githubusercontent.com/mozilla/pdf.js/ba2edeae/web/compressed.tracemonkey-pldi-09.pdf" height="620"}
::

# Parameters

| Parameter | Default Value | Example Value |
| :-- | :-- | :-- |
| `src` | `<required>` | e.g. `https://www.example.com/foo-bar.pdf` |
| `page` | `1` | e.g. `5` |
| `zoom` | `page-width` | `page-width`, `page-fit`, `50%`, `75%`, `100%`, `125%`, `150%`, `200%`, `300%` |
| `height` | `1024` | e.g. `620` or `0` lets it grow to the whole document instead. |
{.table-leading-col .table-code-nohighlight}

# Default Code

```md
::block-pdf{src="https://www.example.com/foo-bar.pdf"}
::
```


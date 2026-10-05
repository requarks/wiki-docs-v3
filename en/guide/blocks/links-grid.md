---
title: Links Grid
description: A custom grid of cards, each linking to a page or an external URL.
published: true
date: '2026-10-05T03:52:47.219Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-10-05T03:36:07.236Z'
---

# Description

A custom grid of cards, each linking to a page or an external URL.

While similar to the [Index](/guide/blocks/index) content block, it allows for more customization by manually declaring the links, their ordering and extra properties (like image, tags, color).

# Demo

::block-links-grid{minWidth="301px" maxWidth="2fr" maxHeight="2"}
```yaml
- title: Getting Started
  url: /guide/blocks/links-grid
  description: Everything you need on your first day.
  icon: 'mdi:rocket-launch-outline'
  color: blue
- title: Guides
  url: /guide/blocks/links-grid
  description: Step-by-step instructions for common tasks.
  icon: 'mdi:book-open-variant'
  color: amber
  tags:
    - How-to
    - Reference
- title: FAQ
  url: /guide/blocks/links-grid
  description: Frequenty Asked Questions
  icon: 'mdi:book-open-variant'
  color: lime
- title: Reference
  url: /guide/blocks/links-grid
  description: Detailed description of the workflow
  icon: 'mdi:book-open-variant'
  color: rose
  tags:
    - Advanced
    - Reference
```
::


# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `minWidth` | `300px` | Any value accepted by the [CSS minmax function](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/minmax). |
| `maxWidth` | `1fr` | Any value accepted by the [CSS minmax function](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/minmax). |
| `maxHeight` | `<none>` | The maximum height of a card when images are used. Leave empty for no limit. |
{.table-leading-col .table-code-nohighlight}

# Body

The body consists of a **YAML** list in a code block.

| Field | Description | Required |
| :-- | :-- | :-: |
| url | Path to a page or an external URL | :white_check_mark: |
| title | Title of the link |  |
| description | Short description of the link |  |
| icon | Any valid icon name from [Iconify](https://icon-sets.iconify.design/), e.g. `mdi:rocket-launch`. If `color` is provided, the icon will also use that color. |  |
| image | Path / URL to an image. The image will use a cover fill at the top of the card. |  |
| color | Any valid [TailwindCSS color](https://tailwindcss.com/docs/colors) name (in lowercase), e.g. `violet`. |  |
| tags | A list of tags to display (or a single string). If `color` is provided, the tags will be displayed using that color. |  |
{.table-leading-col}


# Default Code

````markdown
::block-links-grid
```yaml
- title: Getting Started
  url: /getting-started
  description: Everything you need on your first day.
  icon: 'mdi:rocket-launch-outline'
  color: blue
- title: Guides
  url: /guides
  description: Step-by-step instructions for common tasks.
  icon: 'mdi:book-open-variant'
  color: amber
  tags:
    - How-to
    - Reference
```
::
````


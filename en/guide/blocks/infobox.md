---
title: Infobox
description: A summary box beside the text, filled in from a list of facts.
published: true
date: '2026-08-17T00:03:18.163Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T02:53:17.092Z'
---

::block-infobox{name="Wiki.js" image="https://static.requarks.io/logo/wikijs-butterfly.svg"}
```yaml
City: Montreal
Country: Canada
Public Transport:
  Metro: true
  Bus: true
  Monorail: false
Website: https://montreal.ca
```
::

# Description

A summary box beside the text, filled in from a list of facts.

## Features

- Image with label
- Sub-sections
- Booleans
- Links

# Demo

See on the right!

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `name` | `<required>` | `-` |
| `image` | `<none>` | Path or URL to image, e.g. `https://www.example.org/image.png` |
| `imageCaption` | `<none>` | `-` |
{.table-leading-col .table-code-nohighlight}

# Body

The body consists of a **YAML** code block.

- Each key / value represents a row in the infobox.
- Children objects are displayed as a sub-section.
- Boolean values are displayed as :white_check_mark: (true) or :x: (false)
- URLs are automatically formatted as clickable links, without the protocol

# Default Code

````markdown
::block-infobox{name="Lorem ipsum"}
```yaml
City: Montreal
Country: Canada
Public Transport:
  Metro: true
  Bus: true
  Monorail: false
Website: https://montreal.ca
```
::
````


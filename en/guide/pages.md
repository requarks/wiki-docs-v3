---
title: Page Operations
description: Move, duplicate and delete pages
published: true
date: '2026-11-22T17:40:33.763Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-16T23:35:09.043Z'
---

# Duplicate

You can duplicate an existing page by clicking the <kbd>:la:copy:</kbd> button in the bottom-right corner of the page. You'll be prompted for the new page title and path.

> [!IMPORTANT]
> You must have the **Write Pages** (`write:pages`) permission to use this feature.

# Rename / Move

You can rename or move an existing page by clicking the <kbd>:la:share:</kbd> button in the bottom-right corner of the page. You'll be prompted for the updated page title and path.

> [!IMPORTANT]
> You must have the **Manage Pages** (`manage:pages`) permission to use this feature.

# Delete

You can delete a page by clicking the <kbd>:la:trash:</kbd> button in the bottom-right corner of the page. You'll be prompted to confirm the deletion.

![Page Delete Confirmation Dialog](/guide/images/page-delete-confirm.png =420x){.shadow-md}

The page can still be recovered from the history, unless the history has been purged by an administrator. Refer to the [File Manager](/guide/file-manager#recycle-bin) page on how to restore a page from the recycle bin.

> [!IMPORTANT]
> You must have the **Delete Pages** (`delete:pages`) permission to use this feature.

# Create via URL

You can prepopulate a new page editor, path, locale, title and template via the URL. This is useful for linking dynamically to future pages where the path is generated automatically.

```xml
/_create/<editor>?path=<path>&locale=<locale>&template=<template-uuid-or-path>&title=<title>
```

All parameters except `<editor>` are optional.

| Parameter | Description | Example |
| :-- | :-- | :-- |
| editor | The editor to use. *(e.g. `markdown`, `visual`, `asciidoc`, etc.)* | `markdown` |
| path | The path of the page to create. | `foo/bar` |
| locale | The locale of the page to create *(uses site default if not specified)* | `en` |
| template | The template to use as a starting point. Must be the UUID or path of the template. | `templates/abc` |
| title | The title of the page to create. | `My New Page` |
{.table-leading-col}


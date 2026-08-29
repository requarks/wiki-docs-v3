---
title: Markdown Editor
description: The flagship Markdown editor
published: true
date: '2026-08-26T08:00:37.303Z'
tags:
  - user-guide
  - editing
editor: markdown
dateCreated: '2026-08-13T18:41:42.507Z'
---

# Overview

The markdown editor is the flagship editor for writing pages. It is the recommended editor for most users.

> [!TIP]
> To learn about the Markdown syntax and the supported addons, check out the [Markdown Syntax](/guide/markdown) guide instead.

# Interface

::block-gallery{thumbnailSize="640" fit="contain" unlockAspectRatio="true"}
/guide/images/markdown-editor-ui.png
::

The editor is divided into 2 sections:
- the [Code Editor](#code-editor) on the left
- the [Render Preview](#render-preview) on the right

The right-most [Page Actions Bar](#actions-bar) also becomes orange :orange_square: in edit mode, with additional functions.

## Code Editor

Running on the powerful Monaco engine *(the same engine as VS Code)*, it provides everything an editor needs to quickly write content.

- The top toolbar (in blue :blue_square:) contains shortcuts to formatting (e.g. bold, italic, etc.). Select text in the code editor and click on one of the formatting buttons to apply that formatting to the selection.
- The left toolbar (in grey :black_large_square:) contains shortcuts for inserting content (e.g. links, images, blocks, etc.).
- On the right portion of the editor, a minimap is displayed to quickly locate and move around long pages.

### Edit existing elements

Some elements (e.g. tables, content blocks, etc.) can be edited visually by clicking the grey `Edit <...>` link above them.

### Command Palette

Press <kbd>F1</kbd> to show the **Command Palette**. It's a quick access dialog to all available commands and editor configurations.

> [!NOTE]
> The command palette may show keyboard shortcuts that are already registered by the browser / extensions and may not work as a result.

### Multi-cursor Tips

- With a text selection, press <kbd>Ctrl</kbd> + <kbd>D</kbd> to select the next instance.
- Hold <kbd>Alt</kbd> while clicking to insert multiple cursors.
- Press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Up/Down</kbd> to add a cursor above or below the current one.

## Render Preview

The Render Preview shows a preview of the Markdown content, as it will displayed once saved.

- The Render Preview can be toggled off/on by clicking the <kbd>:mdi:eye-off-outline:</kbd> icon at the top in order to use the full width as the code editor.
- The preview will automatically scroll to stay in sync with where you are in the code editor (cursor position). To disable the scroll sync, click the <kbd>:mdi:arrow-vertical-lock:</kbd> button to toggle it off.
- When using tabs, the tab matching the content where the cursor is will automatically be focused.

## Page Actions Bar

In addition to the usual buttons, the following buttons are available in the editor:

- <kbd>:mdi:image-sync-outline:</kbd> displays the pending uploads which will be stored upon save.

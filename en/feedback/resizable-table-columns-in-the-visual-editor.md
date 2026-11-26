---
title: Resizable table columns in the Visual editor
description: >-
  Tables in the Visual editor can't be resized by dragging a column edge.
  prosemirror-tables already ships columnResizing, and the comment above
  tableEditing() in frontend/src/editor/visual/index.js gi…
published: true
date: '2026-11-26T17:33:23.913Z'
tags: []
editor: markdown
dateCreated: '2026-11-26T17:33:23.913Z'
---

Tables in the Visual editor can't be resized by dragging a column edge. `prosemirror-tables` already ships `columnResizing`, and the comment above `tableEditing()` in `frontend/src/editor/visual/index.js` gives two reasons for leaving it out. A dragged width had no way into markdown and was lost on save. And the resize handle, being the cell's last child, gave the paragraph back the bottom margin `_page-contents.scss` takes off it, which doubled the height of every row the pointer crossed.

We need resizing for wide tables with a lot of text per cell (job descriptions, onboarding road maps), so we built it on top of 3.6.1 with both of those handled. The widths go into the attributes line a table already supports:

```
| A | B | C |
| --- | --- | --- |
| 1 | 2 | 3 |
{colwidths="120,,300"}
```

An empty entry is a column with no width. With `multimdTable` off the line goes after a blank line, since under GFM a line right under a table is one more row. The renderer turns it into a `<colgroup>`. A table with every column sized is drawn at the sum inside a scrolling wrapper, otherwise the `display: block` table box squeezes the inner table to the article width.

The row height is fixed in `_visual-editor.scss` by taking the bottom margin off the element right before the handle, `:has(+ .column-resize-handle)`. On the last column the handle sat past the table's edge, so it is moved inside there, otherwise a scrollbar came and went with the pointer.

When an edge is grabbed every column gets its on-screen width, so only the dragged column moves and the resize is one undo step. Without that, shrinking the first column of a two-column table widened the second one.

Would this format work for you? A working implementation on top of 3.6.1 is in https://github.com/kost-t-human/wiki/tree/table-column-widths.

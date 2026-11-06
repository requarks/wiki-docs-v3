---
title: Sort navigation menu items alphabetically
description: >-
  Category: Navigation Currently, navigation menu items can only be reordered
  manually by dragging each one with its handle in Edit Menu Items. On large
  wikis with many links and submenus, keeping menu…
published: true
date: '2026-11-06T12:58:30.440Z'
tags: []
editor: markdown
dateCreated: '2026-11-06T12:58:30.440Z'
---

**Category:** Navigation

Currently, navigation menu items can only be reordered manually by dragging each one with its handle in *Edit Menu Items*. On large wikis with many links and submenus, keeping menus in alphabetical order this way is slow and error-prone, and must be redone every time an item is added.

**Proposal**

- Add a **"Sort A → Z"** action in the *Edit Menu Items* overlay (e.g. in the ⋮ menu next to *Clear All Items*), and/or on right-click of a header/link to sort only its nested children.
- Sorting should respect the hierarchy: items stay within their header/submenu, and separators act as group boundaries.
- Add an **"Auto-sort alphabetically"** toggle per navigation menu, so new items are inserted in the right place automatically.
- Allow setting alphabetical sorting as the **default for the whole wiki** from **Administration → Site → Navigation**, so every menu is sorted automatically without having to enable it menu by menu (individual menus could still override it).

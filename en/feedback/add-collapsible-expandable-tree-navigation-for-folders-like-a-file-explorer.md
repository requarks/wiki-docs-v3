---
title: Add collapsible/expandable tree navigation for folders (like a file explorer)
description: >-
  Hello Wiki.js team and community, I'm using Wiki.js 3.3.0 and I've noticed
  that the page tree in the sidebar (and in any custom tree representation) does
  not support expand/collapse behavior for fold…
published: true
date: '2026-11-11T10:19:43.821Z'
tags: []
editor: markdown
dateCreated: '2026-11-11T10:19:43.821Z'
---

Hello Wiki.js team and community,
I'm using Wiki.js 3.3.0 and I've noticed that the page tree in the sidebar (and in any custom tree representation) does not support expand/collapse behavior for folders.
Current behavior:
Folders (pages with isFolder: true) are rendered as regular links.
Clicking a folder navigates into it, replacing the current view, instead of expanding its children in place.
There is no way to see the nested structure without navigating into each folder.
This makes it difficult to browse deep hierarchies quickly, especially when you want to jump between sibling pages.
Expected behavior:
Folders should be expandable/collapsible like in a file explorer.
Clicking a folder could either toggle its expansion or still navigate, but with a separate toggle icon (e.g., a triangle/chevron) to expand without leaving the current page.
The expanded state should persist while navigating between pages (optional but nice).
This would greatly improve usability for wikis with many nested pages.
Please consider adding a collapsible tree component to the default navigation
Thank you for your work on Wiki.js — it's a great product, and this small addition would make a big difference for documentation-heavy setups!

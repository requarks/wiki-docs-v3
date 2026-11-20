---
title: Configurable default icons for new pages and folders
description: >-
  Summary Every page and folder can have its own icon, but there is no way to
  set a default. A new page or folder always starts with the built-in icon, and
  has to be changed by hand in the page propert…
published: true
date: '2026-11-20T03:25:26.749Z'
tags:
  - navigation
  - misc
editor: markdown
dateCreated: '2026-11-19T10:57:01.078Z'
---

**Summary**
Every page and folder can have its own icon, but there is no way to set a default. A new page or folder always starts with the built-in icon, and has to be changed by hand in the page properties (or the navigation editor) to match the rest of the site. On a wiki with hundreds of pages this is easy to forget, and the menu ends up with a mix of styles.

**Current behaviour**
- New pages get the built-in page icon (`mdi:text-box-outline`), new folders the built-in folder icon (`mdi:folder-outline`).
- Changing them is a manual step per item, in the page properties or the navigation editor.
- Keeping a consistent look across the site requires a script against the API after the fact.

**Proposal**
1. **Site-wide defaults** under Admin → Theme or Navigation:
   - default icon for new pages
   - default icon for new folders
   - accepts both MDI names and custom images (`img:/_files/...`), like the icon picker does today.
2. **Defaults per path**, optional and evaluated by longest match, e.g.:
   - pages under `/section-a` → `img:/_files/icons/page-a.svg`
   - folders under `/section-b/customers` → `img:/_files/icons/customer.svg`
3. **Apply to existing items**: a one-off action ("Apply defaults to items still using the built-in icon"), with a preview of how many pages and folders it will change. Items with a manually chosen icon are left alone.
4. The page properties dialog shows the inherited default, with an option to override it.

**Why**
- Consistent navigation without manual work per page.
- Contributors don't need to know which icon to pick.
- No API scripts needed to keep the menu tidy.

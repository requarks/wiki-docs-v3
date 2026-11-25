---
title: >-
  Allow MCP to read and update site theme settings (custom CSS, colors, code
  injection)
description: >-
  Summary The built-in MCP server currently has no administration tools ("There
  are no tools for users, groups, settings, storage or sites"). I'd like an
  optional, off-by-default set of tools that lets…
published: true
date: '2026-11-25T15:28:37.986Z'
tags: []
editor: markdown
dateCreated: '2026-11-25T15:28:37.986Z'
---

**Summary**

The built-in MCP server currently has no administration tools ("There are no tools for users, groups, settings, storage or sites"). I'd like an optional, off-by-default set of tools that lets an assistant read and update the site's theme settings: colors, dark mode, custom CSS and, separately, head/body code injection.

**Use case**

Iterating on a site's look and feel (custom CSS overrides, color palette, layout tweaks) is repetitive work an assistant handles well: read the current CSS, propose a change, apply it, check the result. Today this has to be copy-pasted by hand in the admin area.

**Proposal**

- `get_theme` / `update_theme` tools, disabled by default like move/delete pages.
- Gated by a dedicated toggle in Administration > MCP, and by the token owner holding the matching admin permission (e.g. `manage:sites` / `manage:theme`).
- Requires Read & Write on the MCP token scope.
- Head/body HTML injection behind its own separate toggle, since it allows script injection.
- Changes recorded in the audit log with the token identity.

**Why not just the admin UI**

It works, but it keeps the assistant out of the loop for a task that is mostly text editing, and the MCP already handles comparable write operations on content.

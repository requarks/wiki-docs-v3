---
title: >-
  Restoring Wiki.js 2.x capability of opening the editor pre-filled from an
  existing page via URL
description: >-
  Title: Open the editor pre-filled from an existing page via URL
  (/create/<editor?path=…&from=<pageId) Hi Wiki.js team! I'm a big fan of
  Wiki.js and really grateful for all your work. I've been testin…
published: true
date: '2026-11-19T06:35:37.897Z'
tags: []
editor: markdown
dateCreated: '2026-11-19T05:49:44.174Z'
---

**Title:** Open the editor pre-filled from an existing page via URL (`/_create/<editor>?path=…&from=<pageId>`)

Hi Wiki.js team!

I'm a big fan of Wiki.js and really grateful for all your work.

I've been testing a migration of our 2.x instance to 3.4.0, and it's going smoothly. We're planning to make it the central documentation platform for our developer teams.

I have one suggestion. Wiki.js 2.x could open the editor for a new page, pre-filled with the content of an existing page, using only a URL:

    /e/<locale>/<path>?from=<pageId>

As far as I can tell, this is no longer possible in 3.x.

### How we use it

We use this to keep our documentation in step with our issue tracker. Each new issue automatically gets a link like this:

    /e/en/docs/feature-notes/PROJ-123?from=242

Clicking it opens the editor at the right path, already filled with our feature-note template (page ID 242). Writers start from a consistent structure without copying anything by hand.

### What I found in 3.4.0

- `/_edit/:pagePath` only opens existing pages.
- `/_create/:editor` opens the editor for a new page, but its route handler only reads the `path` and `locale` query parameters, so the editor starts empty.
- Duplicate Page does exactly what we need. It is a client-side store action (`pageDuplicate({ sourcePageId, title, path, locale })`) that reads the source through the API and then calls `pageCreate` with its content.
- The duplicated content lives in client state, not in the URL, so no link can reach it. Reloading `/_create/<editor>` after a duplicate opens an empty editor.
- As a result, an external system can't link to "create this page from that template".

### Suggestion

In the `/_create` route handler, when a `from` query parameter (a page ID) is present, call `pageDuplicate({ sourcePageId: from, path, locale })` instead of `pageCreate({ editor, path, locale })`:

    /_create/<editor>?path=docs/feature-notes/proj-123&locale=en&from=<pageId>

- **Editor:** The editor could come from the source page, as Duplicate Page already does. The `<editor>` segment could then be ignored or used as a fallback.
- **Permissions:** These would stay as they are. Reading the source already goes through the API with the caller's own rights, and saving is checked at the destination.
- **Optional:** A way to skip copying tags (for example `&tags=0`) would be nice. Template pages often carry a marker tag such as `template` that new pages shouldn't inherit.

Since `pageDuplicate` already does the work, I'd expect the change to be small and limited to the route handler.

### Our workaround for now

A Code Injection script detects `<path>?from=<pageId>` on a page that doesn't exist yet and calls `pageDuplicate` itself. It works, but it relies on internal store names and could break with any upgrade. Built-in support would let us remove it.

Would you consider adding this? It would mean a lot to us.

Thank you so much for Wiki.js 3!

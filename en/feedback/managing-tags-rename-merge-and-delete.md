---
title: 'Managing tags: Rename, Merge, and Delete'
description: >-
  Problem Free-form tagging leads to duplicates and outdated naming (e.g.,
  network, networks, networking). Right now, fixing or updating these requires
  manually editing every individual page. Proposed…
published: true
date: '2026-11-17T18:38:48.876Z'
tags: []
editor: markdown
dateCreated: '2026-11-17T18:26:22.860Z'
---

**Problem**
Free-form tagging leads to duplicates and outdated naming (e.g., `network`, `networks`, `networking`). Right now, fixing or updating these requires manually editing every individual page.

**Proposed Solution**
Adding basic tag hygiene tools to the Admin panel would solve this immediately:

- **Rename Tags:** Edit a tag's name globally, automatically updating all linked pages without breaking references or requiring manual page edits.
- **Merge Tags:** Select duplicate tags and merge them into a single master tag, automatically updating and deduplicating all linked pages.
- **Delete Tags:** Deleting a tag globally removes it from all linked pages.

**Optional Formatting Rules (Admin Settings)**
To prevent formatting duplicates before they happen, it would also be helpful to have optional global enforcement toggles in the Admin panel:
- **Force Lowercase:** Automatically convert all tags to lowercase on save (e.g., `Network` → `network`).
- **Spacing Normalization:** Choose between forcing **kebab-case** (converting spaces to hyphens, e.g., `network security` → `network-security`) or stripping spaces completely (`networksecurity`).


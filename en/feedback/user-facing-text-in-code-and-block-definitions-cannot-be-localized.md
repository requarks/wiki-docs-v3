---
title: User-facing text in code and block definitions cannot be localized
description: >-
  What Four kinds of user-visible text never reach the translation files, so
  they stay English while the surrounding UI is translated. Permission names and
  descriptions — hard-coded in frontend/src/com…
published: true
date: '2026-11-14T08:03:54.598Z'
tags: []
editor: markdown
dateCreated: '2026-11-14T08:03:54.598Z'
---

**What**
Four kinds of user-visible text never reach the translation files, so they stay English while the surrounding UI is translated.

1. Permission names and descriptions — hard-coded in `frontend/src/components/GroupEditOverlay.vue` (`permissionCards` from ~line 900, `rules` from ~line 1034). The section headings above them are already keys, so the screen shows translated headings with English descriptions. ~40 strings.

2. Storage target actions — `backend/modules/storage/git/definition.yml`, the `actions:` block from line 142. `label`, `hint` and `warn` are plain strings. 8 strings.

3. File manager context menu — `frontend/src/components/FileManager.vue` lines 711, 725, 739, 748, 754 (`Duplicate...`, `Rename / Move Page...`, `Rename / Move To...`, `Rename...`, `Move To...`). The Delete entry beside them uses `common.actions.delete`, so one menu mixes two languages. Similar labels are hard-coded in `PageActionsCol.vue`.

4. Content blocks — every block's `name`, `description` and each field's `label` / `hint` are in `blocks/block-*/component.js` under `static definition`: 28 blocks, roughly 280 strings. The comment there notes the values must be plain literals because the build collects them into `compiled/blocks.manifest.json`. The Blocks admin page is fully translated around them, which makes the gap easy to see.

**Why it matters**
These are not edge cases. Permissions and the file manager are the screens an administrator uses to grant access and move content, and the storage actions include destructive ones (Import Everything, Purge Local Repository) whose warnings are read at the moment a mistake is expensive.

**Suggestion**
- Move the permission and file-manager strings into `backend/locales/en.json` and render them with `t()`, as the neighbouring keys already are.
- Allow a `labelKey` in storage module `definition.yml` entries.
- For blocks, either emit keys in the manifest or keep a `nameKey` beside the literal so the build still works.

**Environment**
Wiki.js 3.2.0, zh-CN locale.


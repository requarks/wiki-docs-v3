---
title: File Manager
description: Manage assets and pages
published: true
date: '2026-09-25T20:51:48.595Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-20T07:53:30.407Z'
---

# Overview

# Folders

# Upload Assets

# View Options

# Recycle Bin

Deleted pages can be restored from the **Recycle Bin**.

> [!IMPORTANT]
> You must have the `manage:pages` or `delete:pages` permission at the path where the page was prior to deletion in order to restore it.

## Restore a page

::block-steps
1. From the **File Manager**, click on **:la:recycle: Recycle Bin** in the lower-left corner.
2. Right-click on the desired page and select **Restore**.
3. Confirm the restore.

> [!NOTE]
> - If a page already exists at the path the page previously was, you'll be prompted to choose another location to restore it to.
> - A page can be restored as long as the page history has not been purged up to the page deletion timestamp. The page history can be purged from the **Administration Area** :la:arrow-right: **Utilities** page.
> - You cannot empty the recycle bin. Unlike a traditional file system, the recycle bin simply shows entries of type "page deletion" from the page history ledger. Purge the page history from the Administration Area to permanently destroy a page *(see previous point)*.
::

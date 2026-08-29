---
title: Page History
description: View, compare and restore revisions of a page
published: true
date: '2026-08-24T00:07:40.775Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-16T23:10:06.840Z'
---

# Overview

Click the <kbd>:la:history:</kbd> button on the right-most column of a page to view all the past edits. The source code will be displayed in a dialog.

# Usage

::block-gallery{thumbnailSize="380" fit="contain" unlockAspectRatio="true"}
![Page History Sidebar](/guide/images/page-history-sidebar.png)
::

## Timeline

A timeline of all past edits are shown on the left, in most recent to oldest order. The following info is shown:

- **Action**: e.g. Created, Updated, Renamed, etc.
- **Timestamp**: When was the edit made
- **Author**: Who made the edit
- **Change**: What changed. Sometimes a page edit may have identical content because only its metadata was changed (e.g. icon or title).

## Operations

Click the <kbd>:la:ellipsis-h:</kbd> button on the desired timeline item to access its available actions.

- **Set as Differencing Source**: Used for comparison. Same as clicking the <kbd>A</kbd> button.
- **Set as Differencing Target**: Used for comparison. Same as clicking the <kbd>B</kbd> button.
- **View Source**: View the page source at this point in time.
- **Download Version**: Download the page source at this point in time.
- **Restore**: Restore the page to this revision. It will be added as a new revision at the top of the timeline, keeping all existing revisions in place.
- **Branch off from here**: Use this revision contents to create a new page at a new location.

## Compare

You can compare 2 revisions from the timeline by clicking the <kbd>A</kbd> (source) and <kbd>B</kbd> (target) buttons.

You can switch between Side-by-side and Inline diff view by clicking the corresponding toggle in the top-right corner.

# Permissions

You must have the **View Page History** (`read:history`) permission in order to use this feature.


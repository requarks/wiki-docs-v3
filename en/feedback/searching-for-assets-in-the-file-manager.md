---
title: Searching for assets in the file manager
description: >-
  Currently, searching for assets in Wiki.js appears to be limited to the
  currently selected folder. It does not search through nested folders, making
  it difficult to locate files and images when asset…
published: true
date: '2026-11-05T09:44:19.671Z'
tags:
  - file-manager
editor: markdown
dateCreated: '2026-11-05T05:20:51.360Z'
---

Currently, searching for assets in Wiki.js appears to be limited to the currently selected folder. It does not search through nested folders, making it difficult to locate files and images when assets are organized into multiple levels of directories.

I would like to request an improvement that allows asset searches to include all nested folders, rather than being restricted to the current directory.

**Requested Functionality:**
Implement recursive asset searching across the folder structure in all areas where assets can be selected or uploaded, including:

- File Manager: Allow users to search for files and images across all folders and subfolders, regardless of the currently selected directory.
- Image Upload / Selection: Allow users to search for existing assets across the entire folder structure when selecting an image.
- Icon Selection: Allow users to search for icons across all folders and nested directories when choosing a custom image icon.

**Expected Behavior:**
When performing a search, Wiki.js should look through the current folder and all of its descendants, returning matching assets regardless of their directory depth.

Ideally, search results should also display the folder path or location of each matching asset so users can identify where the file is stored.

This would make asset management significantly easier, especially for installations with large asset libraries and deeply nested folder structures.

---
title: Extensions
description: Install extensions for extra functionality
published: true
date: '2026-08-20T07:07:01.130Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-14T07:55:02.119Z'
---

# Overview

Extensions are optional dependencies you can install to enable more features on your wiki. They are usually OS/platform-specific binaries that cannot be bundled with Wiki.js.

> [!TIP]
> The docker image includes all the extensions by default.

# Available Extensions

## Git

Distributed version control system.

**Required for...**

- The Git storage module to synchronize content with a remote repository.

## Pandoc

Converts between markup formats.

**Required for...**

- Importing content from other wikis and formats such as MediaWiki, AsciiDoc, Textile or DocBook.

## Puppeteer

Headless Chromium browser.

> [!WARNING]
> Installing it downloads a Chromium build of a few hundred megabytes, unless the server already provides one through `PUPPETEER_EXECUTABLE_PATH`.

**Required for...**

- Exporting pages as PDF.
- Rendering content elements on the server, such as Mermaid or PlantUML diagrams.
- Re-rendering pages on the server

## Sharp

Processes and transforms images.

**Required for...**

- Cropping/resizing user avatars.
- Generating thumbnails of uploaded images.
- Optimizing site assets such as logos and background images.


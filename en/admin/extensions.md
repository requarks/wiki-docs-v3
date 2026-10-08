---
title: Extensions
description: Install extensions for extra functionality
published: true
date: '2026-10-08T05:41:48.186Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-14T07:55:02.119Z'
---

# Overview

Extensions are optional dependencies you can install to enable more features on your wiki. They are usually OS/platform-specific binaries that cannot be bundled with Wiki.js.

> [!TIP]
> The docker image includes all the extensions by default.

| Extension | Description | Used For | Importance |
| :-- | :-- | :-- | :-- |
| Git | Distributed version control system. | The Git storage module to synchronize content with a remote repository. | :orange_circle: **Optional**<br>*Only if you're using the Git storage module*{.text-sm} |
| Pandoc | Converts text between markup formats. | Importing content from other wikis and formats such as MediaWiki, Textile or DocBook. | :orange_circle: **Optional**<br>*Only if you're importing non-markdown / asciidoc content*{.text-sm} |
| Puppeteer | Headless chromium browser. | Rendering pages on the server (e.g. importing content via storage modules / other wikis, re-rendering pages in the background). *Note that installing it downloads a Chromium build of a few hundred megabytes.* | :green_circle: **Highly recommended** |
| Sharp | Processes and transforms images. | Rendering image thumbnails, resizing images, optimizing site assets (logos/backgrounds), etc. | :green_circle: **Highly recommended** |
{.table-leading-col}


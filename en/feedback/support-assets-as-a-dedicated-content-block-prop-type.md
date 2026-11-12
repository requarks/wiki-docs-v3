---
title: Support assets as a dedicated content block prop type
description: >-
  Currently, content blocks like PDF and media player only accept the asset as a
  path/url string, since that is the only appropriate prop type. It is quite
  inconvenient to add these blocks for assets w…
published: true
date: '2026-11-12T05:55:55.504Z'
tags: []
editor: markdown
dateCreated: '2026-11-12T05:55:01.678Z'
---

Currently, content blocks like PDF and media player only accept the asset as a path/url string, since that is the only appropriate prop type. It is quite inconvenient to add these blocks for assets within the wiki, since you have to upload the asset first, obtain its path, then use the insert block menu.

My suggestion is that a new type of prop should be added that have the 3 options of accepting a url (like before), support uploading a new asset and auto resolving to its path, or use a proper file picker to choose an existing asset. Visually it could just be a normal text box with a upload and browse button on the side.

For the uploading, it should probably integrate into the existing pending upload system.

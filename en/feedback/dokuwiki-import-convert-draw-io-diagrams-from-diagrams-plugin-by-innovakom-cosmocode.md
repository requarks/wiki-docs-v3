---
title: >-
  DokuWiki import: convert draw.io diagrams from "Diagrams plugin by Innovakom +
  CosmoCode"
description: >-
  Is it possible to automatically convert draw.io diagrams from the DokuWiki
  plugin "Diagrams plugin by Innovakom + CosmoCode" during the DokuWiki import
  into Wiki.js? The plugin stores diagrams in Dok…
published: true
date: '2026-11-25T14:56:27.289Z'
tags: []
editor: markdown
dateCreated: '2026-11-25T14:56:27.289Z'
---

Is it possible to automatically convert draw.io diagrams from the DokuWiki plugin "Diagrams plugin by Innovakom + CosmoCode" during the DokuWiki import into Wiki.js?

The plugin stores diagrams in DokuWiki like this:
```
<diagram><svg xmlns="http://www.w3.org/2000/svg" ... content="&lt;mxfile ...&gt;...&lt;/mxfile&gt;" ...>...</svg></diagram>
```
In Wiki.js, the draw.io block uses this syntax:
```
::block-drawio
<svg xmlns="http://www.w3.org/2000/svg" ... content="&lt;mxfile ...&gt;...&lt;/mxfile&gt;" ...>...</svg>
::
```

The conversion would be a simple text replacement:
DokuWiki > Wiki.js 

<diagram>  to ::block-drawio + code fence (```) 

</diagram> to code fence (```) + :: 


---
title: Fill info on page from a csv / json / spreadsheet dynamically
description: >-
  I run Wiki.JS for a school. Each subject has a page that is run by the head of
  the department. Currently, their job entails updating their respective pages
  whenver people join or leave the school. Th…
published: true
date: '2026-11-04T08:25:48.357Z'
tags: []
editor: markdown
dateCreated: '2026-11-04T08:25:48.357Z'
---

I run Wiki.JS for a school. Each subject has a page that is run by the head of the department. 

Currently, their job entails updating their respective pages whenver people join or leave the school. This happens regularly and is boring work which they tend to forget. Having the names on the wiki page is helpful but also creates a secondary source of truth.

The main source of truth is a school software which creates a lot of CSV-files, so whenever people in the school change, one "import"-flow is run which updates all apps.

I would love it, if I could just add to that flow that a csv / json / yaml / spreadsheet in the wiki-git or even in the wiki volumes in docker is updated and the wiki then just recreates the pages with the new info. 

In the editor this could be a content block, that just displays a table where one picks a file and the columns and then a column and values to filter. This way I could say "Display Full Name and Mail of all with Group `math`". 

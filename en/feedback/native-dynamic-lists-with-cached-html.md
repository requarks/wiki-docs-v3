---
title: Native dynamic lists with cached HTML
description: >-
  We have built a solution for dynamic lists in the Midgard Wiki using custom
  Wiki.js blocks and n8n. I think similar functionality could be useful to other
  Wiki.js users as a native feature. A list is…
published: true
date: '2026-11-09T09:30:05.361Z'
tags:
  - blocks
editor: markdown
dateCreated: '2026-11-09T09:13:08.827Z'
---

We have built a solution for dynamic lists in the Midgard Wiki using custom Wiki.js blocks and n8n. I think similar functionality could be useful to other Wiki.js users as a native feature.

A list is defined by filters such as tags, exclusions and tag groups. The results can be sorted, grouped under headings and displayed in different formats, including inline lists, tables and cover galleries. A saved list can be reused on multiple pages. For ordered content such as campaigns, an article can have a different position in each campaign.

To improve performance, n8n builds the results in the background and stores the generated HTML as a dedicated Wiki.js page with a stable ID. Our article blocks then load that stored result instead of running the full selection, sorting and grouping on every page view. The stored results are currently rebuilt hourly. Changes to list definitions are also processed when their source page changes.

This has made page loading noticeably faster in our wiki. It also gives search engines a way to discover the entries: the result page contains ordinary HTML links without requiring JavaScript, and articles link to that result page. One limitation of our current implementation is that the list embedded in an article is loaded by the browser, rather than expanded into the article’s initial HTML. A native implementation could improve on that by rendering the list directly on the server.

It would be great to have native support for:
- Reusable dynamic lists based on tags, including exclusions and tag-group hierarchies
- Group headings and configurable ordering, including ordering within a series or campaign
- Different display formats, including galleries
- Background generation and cached results, with updates when relevant pages or tags change
- Server-rendered HTML links and results that respect the visitor’s permissions

We have documented our current solution here:
- [Dynamic lists](https://midgard-wiki.de/redaktion/hilfe/listen)
- [Tag groups](https://midgard-wiki.de/redaktion/hilfe/taggruppen)
- [Example cover gallery](https://midgard-wiki.de/redaktion/hilfe/beispiele/covergalerie)

Sorry, the documentation is currently only available in German! 🙂

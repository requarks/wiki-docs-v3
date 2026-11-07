---
title: Add custom tags/events to the Microsoft Clarity integration
description: >-
  I would like to see the Wiki.js 3 Microsoft Clarity integration expanded to
  optionally send Wiki.js-specific context through Clarity's custom tags and
  events. Wiki.js already has useful information s…
published: true
date: '2026-11-07T03:58:51.655Z'
tags:
  - analytics
editor: markdown
dateCreated: '2026-11-06T17:09:16.703Z'
---

I would like to see the Wiki.js 3 Microsoft Clarity integration expanded to optionally send Wiki.js-specific context through Clarity's custom tags and events.

Wiki.js already has useful information such as:

- Current page ID and path
- Authentication state
- Page locale
- User groups
- "Rate this page" interactions

Making selected values available to Clarity would make session recordings significantly easier to analyze.

For example:

```javascript
clarity("set", "wikiPageId", "123");
clarity("set", "wikiAuthenticated", "true");
clarity("set", "wikiPageRating", "2");
clarity("event", "WikiPageRated");
clarity("identify", "custom-id", "custom-session-id", "custom-page-id", "friendly-name")
```

This would help administrators answer questions such as:

- What happened before a user rated a page poorly?
- Which pages produce the most problematic user journeys?
- Do authenticated and anonymous users behave differently?
- Are particular groups having difficulty with specific documentation?

Ideally, the Clarity configuration could expose an optional list of metadata that administrators can choose to send. Potentially identifying information, such as user ID and group membership, should be disabled/optional by default and enabled by the administrator.
The goal isn't to replace Wiki.js analytics or feedback features. It is to give Clarity enough Wiki.js context to make its recordings, heatmaps, filters, and events substantially more actionable.

https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-api

---
title: login-status / group-specific content block visibility
description: >-
  I run Wiki.JS for a school. On v2.5 i have implemented (with javascript) a tag
  {.sensitiveinfo} that applies to a heading. Before the page is displayed the
  javascript will check whether the user is l…
published: true
date: '2026-11-04T08:07:57.283Z'
tags: []
editor: markdown
dateCreated: '2026-11-04T08:07:57.283Z'
---

I run Wiki.JS for a school. On v2.5 i have implemented (with javascript) a tag {.sensitive_info} that applies to a heading. Before the page is displayed the javascript will check whether the user is logged in and delete the block if the user is not. 

Use Case: If a page describes a team in my school then info about what the team does is open to the public. Names of teammembers, however, should not be public to all visitors. Only other teachers should be able to see that info, yet it would be unhelpful if that information would be spread on other pages.

Basically, I would love a native way to specifiy (per content block?) if this is something only logged-in users oder specific groups of users can see. 

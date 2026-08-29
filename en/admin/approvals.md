---
title: Approvals
description: >-
  Define which pages accept edit suggestions from read-only users, and who
  reviews them
published: true
date: '2026-08-21T04:58:05.794Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-12T00:02:28.716Z'
---

# Overview

The **Approvals** page (in the **Administration Area**) is where rules are defined; which specifies which pages are eligible for submissions, who can submit and who can review them.

> [!TIP]
> For the user workflow, check out the [Suggest Edits](/guide/suggest-edits) page instead.

# New Rule

To create a rule, click the **New Rule** button in the top-right corner of the page.

::block-gallery{thumbnailSize="640" fit="contain" unlockAspectRatio="true"}
![admin-approvals-new.png](/admin/images/admin-approvals-new.png)
::

| Field | Description |
| :-- | :-- |
| Rule Name | A name for this rule *(not shown to users)* |
| Applies To | The page matching filter to use. |
| Path / Tags | The path or tags for the matching filter selected above. |
| Can submit edits | One or more user groups that can submit edits. |
| Reviews submissions | One or more user groups that can review submissions. |
{.table-leading-col}

# Manage Rules

- You can temporarily disable a rule by changing the "**Enabled**" toggle.
- Click the **Edit** button to change any aspect of the rule.
- Click the **Delete** button to delete the rule.

> [!WARNING]
> Make sure to approve or reject pending submissions **before** deleting a rule, as you won't be able to review them once no rule covers them.

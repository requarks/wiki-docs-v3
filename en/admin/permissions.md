---
title: Permissions
description: Manage access to your pages
published: true
date: '2026-09-14T01:38:35.093Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-09-14T01:38:35.093Z'
---

# Overview

Wiki.js has a powerful permission system with fine grained control over what your users can see and do.

Permissions are managed at the [group](/admin/groups) level.

- Until a user is assigned to a group, that user is not allowed to view or do anything.
- A user can be part of **one or more** groups.
- A group can have multiple [page rules](#page-rules) and a set of [global permissions](#global-permissions).

# Page Rules

Page rules specify what a user can do on one or more pages, whether it's viewing a page, making edits, upload assets or posting comments. They are optionally tied to specific sites and locales.

A page rule consists of the following elements:
- [Enforcement Mode](#enforcement-mode)
- [Permissions](#permissions)
- [Site Filter](#site-filter)
- [Locale Filter](#locale-filter)
- [Matching Pattern](#matching-pattern)

##  Enforcement Mode

The enformement mode determines whether the rule grants or deny permissions.

- :white_check_mark: **Allow**: Grant the ability to perform the selected actions unless overriden by a **Deny** rule of the same specificity. *(lowest specificity)*
- :red_square: **Deny**: Deny the ability to perform the selected actions. This overrides an **Allow** rule of the same specificity.
- :blue_square: **Force Allow**: Grant the ability to perform the selected actions, bypassing any **Deny** rule of the same specificity. (highest specificity)

## Permissions

One or more permissions can be selected for a page rule:

- **Read Pages** (`read:pages`): Can view and search pages.
- **Write Pages** (`write:pages`): Can create and edit pages.
- **Review Pages** (`review:pages`): Can review and approve edits submitted by users.
- **Manage Pages** (`manage:pages`): Can move existing pages to other locations the user has write access to.
- **Delete Pages** (`delete:pages`): Can delete existing pages.
- **Use CSS** (`write:styles`): Can insert CSS styles in pages.
- **Use JavaScript** (`write:scripts`): Can insert JavaScript in pages. :warning: **Use with caution as users could inject malicious scripts.**
- **View Page Source** (`read:source`): Can view the pages source.
- **View Page History** (`read:history`): Can view previous versions of pages.
- **View Assets** (`read:assets`): Can view / use assets (such as images and files) in pages.
- **Upload Assets** (`write:assets`): Can upload new assets (such as images and files).
- **Manage Assets** (`manage:assets`): Can edit and delete existing assets (such as images and files).
- **Read Comments** (`read:comments`): Can view page comments.
- **Write Comments** (`write:comments`): Can post new comments on pages, edit and delete their own comments.
- **Manage Comments** (`manage:comments`): Can edit and delete any existing page comments.

## Site Filter

A site filter can be applied to limit the page rule to only specific sites instead of all sites.

## Locale Filter

A locale filter can be applied to limit the page rule to only specific locales instead of all locales.

## Matching Pattern

Select how this page rule will match pages:

- **Path Starts With...** (lowest specificity)
- **Path Ends With...**
- **Path Matches Regex...**
- **Has Any Tag...**
- **Has All Tags...**
- **Path is Exactly** (highest specificity)

## Specificity

Rule specificity specifies which rule wins over another when they apply to the same page. The page with the highest specificity always win.

The specificity is determined by:
- **Enforcement Mode** *(lowest specificity)*
- **Matching Pattern**
- **Path** *(highest specificity)*

> [!TIP] Example 1 - Path
> Assuming you have 2 rules:
> | :-- | :-- | :-- |
> | Rule 1 | :red_square: Deny | Path starts with `foo` |
> | Rule 2 | :white_check_mark: Allow | Path starts with `foo/bar` |
> {.table-leading-col}
> 
> **Rule 2** wins because the path is more specific than Rule 1.

> [!TIP] Example 2 - Pattern Matching
> Assuming you have 2 rules:
> | :-- | :-- | :-- |
> | Rule 1 | :red_square: Deny | Path starts with `foo/bar` |
> | Rule 2 | :white_check_mark: Allow | Path is Exactly `foo/bar` |
> 
> **Rule 2** wins because the matching pattern is more specific than Rule 1.

> [!TIP] Example 3 - Enforcement Mode
> Assuming you have 2 rules:
> | :-- | :-- | :-- |
> | Rule 1 | :red_square: Deny | Path starts with `foo/bar` |
> | Rule 2 | :white_check_mark: Allow | Path starts with `foo/bar` |
> 
> **Rule 1** wins because a **Deny** overrides an **Allow** when everything else is the same.
> This use case mostly happens when a user is part of 2 groups, where one has **Allow** and another has **Deny** on the same path.

# Global Permissions

Global permissions represents administrative actions a user can perform. They are not tied to specific pages or sites.

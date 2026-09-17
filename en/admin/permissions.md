---
title: Permissions
description: Manage access to your pages
published: true
date: '2026-09-17T04:17:52.902Z'
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
- A group without any page rule isn't allowed to view or do anything.

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

- :white_check_mark: **Allow**: Grant the ability to perform the selected actions unless overriden by a **Deny** rule of the same specificity. *(lowest priority)*
- :red_square: **Deny**: Deny the ability to perform the selected actions. This overrides an **Allow** rule of the same specificity.
- :blue_square: **Force Allow**: Grant the ability to perform the selected actions, bypassing any **Deny** rule of the same specificity. (highest priority)

## Permissions

One or more permissions can be selected for a page rule:

| Name | Key | Description | Note |
| :-- | :-- | :-- | :-- |
| Read Pages | `read:pages` | Can view and search pages. | |
| Write Pages | `write:pages` | Can create and edit pages. | |
| Review Pages | `review:pages` | Can review and approve edits submitted by users. | |
| Manage Pages | `manage:pages` | Can move existing pages to other locations the user has write access to. | |
| Delete Pages | `delete:pages` | Can delete existing pages. | |
| Assign Tags | `write:tags` | Can assign / unassign tags on pages. | |
| Use CSS | `write:styles` | Can insert CSS styles in pages. | |
| Use JavaScript | `write:scripts` | Can insert JavaScript in pages. | :warning: **Use with caution as users could inject malicious scripts.** |
| View Page Source | `read:source` | Can view the pages source. | |
| View Page History | `read:history` | Can view previous versions of pages. | |
| View Assets | `read:assets` | Can view / use assets *(such as images and files)* in pages. | |
| Upload Assets | `write:assets` | Can upload new assets *(such as images and files)*. | |
| Manage Assets | `manage:assets` | Can edit and delete existing assets *(such as images and files)*. | |
| Read Comments | `read:comments` | Can view page comments. | |
| Write Comments | `write:comments` | Can post new comments on pages, edit and delete their own comments. | |
| Manage Comments | `manage:comments` | Can edit and delete any existing page comments. | |
{.table-leading-col}

## Site Filter

A site filter can be applied to limit the page rule to only specific sites instead of all sites.

## Locale Filter

A locale filter can be applied to limit the page rule to only specific locales instead of all locales.

## Matching Pattern

Select how this page rule will match pages:

| Pattern | Description | Priority |
| :-- | :-- | :-: |
| Path Starts With... | Matches any path that starts with the entered value. Do **NOT** include a leading slash `/`. | Lowest |
| Path Ends With... | Matches any path that ends with the entered value. Do **NOT** include a trailing slash `/`. | :la:chevron-down: |
| Path is Exactly... + Children | Matches both an exact path and its children (e.g. `foo/bar` and `foo/bar/*`, but not `foo/bard`). Do **NOT** include a leading and trailing slash `/`. | :la:chevron-down: |
| Path Matches Regex... | Matches any path matching a regular expression. Do **NOT** include a leading and trailing slash `/`. | :la:chevron-down: |
| Has Any Tag... | Matches any page that has at least one of the selected tag(s). | :la:chevron-down: |
| Has All Tags... | Matches any page that has all of the tags selected. | :la:chevron-down: |
| Path is Exactly | Matches an exact path. Do **NOT** include a leading slash `/`. | Highest |
{.table-leading-col}

## Specificity

Rule specificity specifies which rule wins over another when they apply to the same page. The page with the highest specificity always win.

The specificity is determined in order by:
- **Path** *(highest specificity)*
- **Matching Pattern**
- **Enforcement Mode** *(lowest specificity)*

In other terms,
::block-steps
1. A longer path takes precedence over a shorter path.
2. If the 2 rules match the same path, the priority is given based on the [matching pattern](#matching-pattern).
3. If 2 rules match the same path and use the same matching pattern, the [enforcement mode](#enforcement-mode) with the highest priority wins.
::

### Examples

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
> {.table-leading-col}
> 
> **Rule 2** wins because the matching pattern is more specific than Rule 1.

> [!TIP] Example 3 - Enforcement Mode
> Assuming you have 2 rules:
> | :-- | :-- | :-- |
> | Rule 1 | :red_square: Deny | Path starts with `foo/bar` |
> | Rule 2 | :white_check_mark: Allow | Path starts with `foo/bar` |
> {.table-leading-col}
> 
> **Rule 1** wins because a **Deny** overrides an **Allow** when everything else is the same.
> This use case mostly happens when a user is part of 2 groups, where one has **Allow** and another has **Deny** on the same path.

# Global Permissions

Global permissions represents administrative actions a user can perform. They are not tied to specific pages or sites.

| Name |Description | Note |
| :-- | :-- | :-- |
| `access:admin` | Can access the administration area. | This permission should be granted to anyone with one or more of the permissions below. |
| `read:users` | Can view users, but not create or modify. | |
| `manage:users` | Can create / manage users. | Cannot modify users with `manage:system` permissions. |
| `read:groups` | Can view groups and their permissions, but not create or modify them. | |
| `manage:groups` | Can create / manage groups and assign permissions / page rules. | Cannot modify groups with `manage:system` permissions. |
| `read:audit` | Can read the audit log, i.e. the record of what everybody on this wiki has done. | Usually granted for security auditors. |
| `read:metrics` | Can scrape the Prometheus metrics endpoint from an address it is not open to anonymously. | Usually for use by APIs and automations. |
| `manage:navigation` | Can manage site navigation | |
| `manage:theme` | Can modify site theme settings | |
| `manage:sites` | Can create / manage sites | |
| `manage:system` | Can manage and access everything. Root administrator. | :warning: **Use with caution when assigning this permission. This should normally not be assigned to anything other than the system administrator.** |
{.table-leading-col}

| Action / Group | read:users | write:users | manage:users | read:groups | write:groups | manage:groups | manage:system |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| View user info | :green_circle: | :green_circle: | :green_circle: |  |  |  | :green_circle: |
| Create new user |  | :green_circle: | :green_circle: |  |  |  | :green_circle: |
| Edit user info^1^ |  |  | :green_circle: |  |  |  | :green_circle: |
| Delete user^2^ |  |  | :green_circle: |  |  |  | :green_circle: |
| Assign user to normal groups |  | :green_circle: | :green_circle: |  | :green_circle: | :green_circle: | :green_circle: |
| Assign user to elevated groups |  |  | :green_circle: |  |  | :green_circle: | :green_circle: |
| Assign user to root admin groups |  |  |  |  |  |  | :green_circle: |
| View groups |  |  |  | :green_circle: | :green_circle: | :green_circle: | :green_circle: |
| Create new group |  |  |  |  | :green_circle: | :green_circle: | :green_circle: |
| Edit group |  |  |  |  | :green_circle: | :green_circle: | :green_circle: |
| Set rules |  |  |  |  | :green_circle: | :green_circle: | :green_circle: |
| Set permissions^3^ |  |  |  |  |  | :green_circle: | :green_circle: |
| Delete group^4^ |  |  |  |  |  | :green_circle: | :green_circle: |
{.table-leading-col}

1. Unless the user is part of any group with the `manage:system` (root admin) permission.
2. Unless the user is part of any group with elevated admin permissions.
3. Unless the group has any elevated admin permissions.
4. Unless the group has the `manage:system` (root admin) permission.


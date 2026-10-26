---
title: Page Properties
description: Edit page metadata and configuration
published: true
date: '2026-10-26T01:31:38.370Z'
tags:
  - user-guide
  - editing
editor: markdown
dateCreated: '2026-08-24T08:13:47.973Z'
---

# Overview

The **Page Properties** modal can be accessed by clicking the <kbd>:la:pen-nib:</kbd> button in the right-most bar. It's available in both read and edit mode.

> [!IMPORTANT]
> Any changes made in the **Page Properties** modal are not applied until clicking the **Save Changes** button in the page header.

> [!TIP]
> You can quickly jump to specific sections of the **Page Properties** modal by clicking the related icon in the black bar on the left.

# Info

> [!TIP]
> Avoid putting sensitive information into the **title** and **short description** as they could be seen by users that have read access to other pages pointing to it, in which case that info might be shown.

## Title

The title of the page, shown in:
- Page Header
- File Manager
- Search Results
- Site Navigation
- Index Content Blocks listing the page

## Short Description

A subtitle for the page, shown in:
- Page Header
- Search Results
- Index Content Blocks listing the page

## Icon

An icon or image shown to the left of the page title. Click the <kbd>:la:icons:</kbd> button on the right to open the icon picker dialog.

## Color

An optional color to assign the page. When set, the page icon takes this color and a faint background gradient is applied to the page header. The color is also used in some content blocks like the [block-index](/guide/blocks/index) to apply a colored border to each card.

If not set, the page icon uses the site primary color.

## Alias

An optional alias to quickly access the page regardless of its current location. This is useful for sharing URLs or having a permanent reference link to a page.

The alias becomes accessible at `/a/` + the alias.

For example, by setting an alias of `KB1000` for a page at path `network/knowledge-base/dns-cache-expiration`, a user can now access it by going to `https://wiki.example.com/a/KB1000`. The page can be renamed or moved elsewhere later on and that link will still work.

# Lifecycle Rules

Lifecycle rules are used to perform certain actions automatically on some condition.

Click the **:la:plus: Add Rule** button to create a new rule.

Give it a name and choose a trigger:
- **Days since last content update**: Triggers after X days since the page body (not metadata) was last modified.
- **Every number of days**: Triggers every X days, regardless of whether the page was modified or not.
- **Days since last comment**: Triggers after X days since the last comment was posted to the page.

Then enable one or more actions:
- **Show banner**: Show a banner at the top of the article, with a custom text and icon. By default, the text warns the user that the information might be outdated and needs a review. The page owner and any user with write:pages permission can resolve it.
- **Notify page owner(s)**: Send a notification to the page owner *(see [Ownership](#ownership) below)* that the page needs review.
- **Move page to...**: Move the page to another location. The path can use variables **`{pagePathName}`** (only the last segment of the path, e.g. `foo-bar`) or **`{pagePath}`** (the full path to the page, e.g. `lorem/ipsum/foo-bar`).
- **Apply tags...**: Add one or more tags to the page. Tags are added to existing ones, not replaced.
- **Remove rule after...**: Remove this rule after X trigger(s). Note that you need to enable at least another action in addition to this one.

A common example is to ask a review from the page owner every 90 days to ensure the information is still up to date. In this case, you would select the "**Days since last content update**" trigger with `90` days, and enable the "**Show banner**" and **Notify page owner(s)** actions.

# Ownership

Set who owns the page:

- **Page Creator** *(default)*: the user who created the page.
- **User(s)**: One or more users.
- **Group(s)**: One or more groups.

> [!IMPORTANT]
> In order to use the **User(s)** and **Group(s)** options, you must have the `list:users` and `list:groups` permissions respectively.

# Publishing State

| State | Description |
| :-- | :-- |
| Draft | Visible to users with write access only. |
| Published | Visible to all users with read access. |
| Date Range | Select the start and end date for this page publication. The page will only be accessible to users with read access within the selected date range. |
{.table-leading-col}

# Relations

## Page Relations

Add links to other related pages in the footer.

## Set Locale Relations

Define the alternate versions of this page in other languages. When defined, switching locale will automatically redirect to the related page for that locale.

### Example

For example, if you already have the following 2 pages:
- In **English**, at path `books/popular`
- In **French**, at path `livres/populaires`

When editing the **French** page, from the **Page Properties** modal, click the <kbd>Set Locale Relations</kbd> button and select the `books/popular` for the **English** locale. Both pages are now part of the same set of pages across locales. You can link more locales as needed.

From the `livres/populaires` page in **French**, you can now change the locale to **English** from the locale picker menu (in the top-left corner of the page) to be automatically redirected to `books/popular` in **English**.

> [!NOTE]
> A page can only be part of a single set of pages. You cannot select a page to be the alternate version of multiple pages from the same locale.

## Show Links Tab

Whether to display the Links tab, which shows a list of pages linking to this page (aka backlinks).

## Link Glossary Terms

Whether to link glossary terms *(first occurence of each)* on the page. Only terms that have auto-linking enabled will be linked.

# Scripts

## Javascript - On Load

> [!NOTE]
> You must have `write:scripts` permission to use this feature.

Javascript code that will be executed upon loading the page.

## Javascript - On Unload

> [!NOTE]
> You must have `write:scripts` permission to use this feature.

Javascript code that will be executed when unloading the page.

## CSS Styles

> [!NOTE]
> You must have `write:styles` permission to use this feature.

CSS styles to add or override any CSS on the page.

# Sidebar

## Show Sidebar

Whether to show the page sidebar which usually displays the table of contents, tags, etc.

## Show Table of Contents

Whether to show the table of contents or not. 

## Min/Max Depth

The minimum and maximum header level to display in the table of contents. For example, if you start all your headers as H2 when writing, you should set the minimum to H2 and the maximum to H3.

## Show Tags

Whether to show the list of tags for this page.

## Show Last Edited by

Whether to show the author that made the last edit to this page.

# Social

## Allow Comments

Whether to show comments and allow readers to submit new comments *(if allowed by the reader's group permissions)*.

## Allow Contributions

Whether to allow readers to [suggest edits](/guide/suggest-edits) *(if allowed by an [approval](/admin/approvals) rule)*. 

## Allow Ratings

Whether to allow readers to rate the page. Disable to hide this feature from the page.

# Tags

Assign one or more tags to the page so that it can be found when searching by tag.

> [!TIP]
> Tags can also be edited directly from the page by clicking the **Edit** button while your cursor is over the **Tags** section in the page sidebar.

# Visibility

## Show in Site Navigation

Whether to show this page in the Browse menu. It will still appear in the [File Manager](/guide/file-manager) regardless of this setting.

## Include in Search Results

Whether to show this page in search results.

## Require Password

Whether to require a static password to view this page. The password you set is intended to be shared with other users via external processes, from other pages or via your own communication channels.

> [!IMPORTANT]
> - The page **MUST be published** and the user **MUST have read access** to this page.
> - The password can be seen by **anyone having write access** to this page.
> - Do **NOT** put highly sensitive info behind this password protection feature. It is **NOT** intended for storing secrets, but rather as a convenient way to share access on-demand as part of a company workflow / learning process.

---
title: Navigation
description: Manage the sidebar navigation
published: true
date: '2026-08-28T08:04:07.895Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-28T07:25:11.406Z'
---

# Overview

The site navigation sidebar is fully customizable and can be changed per path.

Additionally, the following buttons are present at the top:

- The **:la:globe: Locale** button to switch between locales *(shown if the [Show Locale Menu](/admin/locale#site-locale-settings) option is enabled)*.
- The **:la:sitemap: Browse** button to quickly navigate via the site hierarchy *(shown if the [Allow Browsing](/admin/general#features) option is enabled)*.

# Hierarchy / Visibility Modes

Click the <kbd>**:la:dharmachakra: Edit Nav**</kbd> button at the bottom of the site navigation sidebar to open the **Edit Navigation** menu.

> [!NOTE] Required Permission
> You must have the `manage:navigation` global permission to edit the navigation. This button will not be shown otherwise.

## Root

On the homepage, you can choose to either **Show** or **Hide** the site navigation:

![Edit Navigation - Root](/guide/images/navigation-ui-modes-root.png =320x){.shadow-md}

## Descendants

On all other pages, you have the following options:

![Edit Navigation - Descendants](/guide/images/navigation-ui-modes.png =480x){.shadow-md}

| Mode | Description |
| :-- | :-- |
| Inherit | Use the menu items and settings from the parent path. **Editing the menu items with this mode selected will edit the parent navigation as well.** |
| Override Current + Descendants | Use a different menu configuration on this page and all children from this path will inherit it as well. |
| Override Current Only | Use a different menu configuration on this page and **only this page**. All children down from this path will keep inheriting the configuration from this page's parent. |
| Hide Current + Descendants | Hide the site navigation sidebar on this page and all children from this path will inherit this mode as well. |
| Hide Current Only | Hide the site navigation sidebar on this page and **only this page**. All children down from this path will keep inheriting the configuration from this page's parent. |
{.table-leading-col}

# Edit Menu Items

Click the orange <kbd>**:mdi:playlist-edit: Edit Menu Items**</kbd> button to open the **Edit Menu Items** overlay.

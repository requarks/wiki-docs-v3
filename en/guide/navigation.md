---
title: Navigation
description: Manage the sidebar navigation
published: true
date: '2026-08-28T22:46:18.987Z'
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

![Edit Menu Items](/guide/images/navigation-ui-edit-overlay.png =820x){.shadow-md}

Click the green <kbd>**:la:plus-circle: Add**</kbd> button to add one of: header, link or separator.

- Click on a menu item to **edit** it.
- Menu items can be **re-ordered** by dragging the :mdi:drag-horizontal: handle.
- Right-click on a menu item to **duplicate**, **nest**/**unnest** or **delete** it.
- Click the <kbd>:la:ellipsis-v:</kbd> button to access the <kbd>**:la:trash-alt: Clear All Items**</kbd> option.

Any change is only persisted upon clicking the <kbd>**:la:check: Save**</kbd> button.

## Header

| Property | Description |
| :-- | :-- |
| Label | Text to display on the menu item. |
| Visibility | Whether to show the menu item to everyone or just selected groups. |
{.table-leading-col}

## Link

| Property | Description |
| :-- | :-- |
| Label | Text to display on the menu item. |
| Icon | Icon or image to display to the left of the menu item. Click the :la:icons: button to open the icon picker. |
| Expand by Default | Whether the submenu is already expanded when the page loads. *(only shown when menu items are nested under it)* |
| Target | The target path or external link to point to. Click the :la:folder-open: button to open the page picker. |
| Open in New Window | Whether to open the link in a new window or not. |
| Visibility | Whether to show the menu item to everyone or just selected groups. |
{.table-leading-col}

### Submenu

To create submenus, first create a normal link menu item to act as a the submenu trigger. Then create a second link menu item under it and click the <kbd>:mdi:format-indent-increase: Nest Item</kbd> to indent it. It is now nested under the first link and will only appear upon clicking the first link. You can nest any number of menu items.

A nested link without a normal link or another nested link above it will be shown in red as invalid.

## Separator

| Property | Description |
| :-- | :-- |
| Visibility | Whether to show the menu item to everyone or just selected groups. |
{.table-leading-col}



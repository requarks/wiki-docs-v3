---
title: Theme
description: Modify the look & feel of your wiki
published: true
date: '2026-10-30T04:40:35.308Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-14T07:57:57.518Z'
---

# Overview

The theme options changes the look and feel of your wiki site.

# Appearance

| Property | Description | Default Value |
| :-- | :-- | :-: |
| Dark Mode | Whether the site should be in dark mode by default. Not recommended for accessibility. Can always be turned off by the user. | :x: |
| Primary Color | The main color for primary action buttons and most form elements. | `#1976D2` |
| Secondary Color | The alternate color for secondary action buttons and for some other elements. | `#02C39A` |
| Accent Color | The accent color for elements that need to stand out or grab the user attention. | `#FF9800` |
| Header Color | The background color for the site top header. | `#000000` |
| Sidebar Color | The background color for the side navigation menu on content pages. | `#1976D2` |
{.table-leading-col}

> [!NOTE]
> These colors do not apply to the administration area, which always uses the default colors. Users who have enabled a color vision deficiency setting in their profile will also see different colors.

# Code Blocks

| Property | Description | Default Value |
| :-- | :-- | :-: |
| Code Blocks Appearance | The color theme used to display code blocks on pages. | **Github Dark** |
{.table-leading-col}

# Animations

| Property | Description | Default Value |
| :-- | :-- | :-: |
| Show Linear Page Load Progress Bar | Display a thin progress bar along the top edge of the screen while a page is loading. | :white_check_mark: |
| Use Fade Transitions Between Pages | Cross-fade from one page to the next instead of switching instantly. Only in browsers that support view transitions. | :white_check_mark: |
{.table-leading-col}

# Layout

| Property | Description | Default Value |
| :-- | :-- | :-: |
| Content Width | Should the content use all available viewport space or stay centered. | **Full Width** |
| Sidebar Position | On which side should the main site navigation sidebar be displayed. | **Left** |
| TOC Position | On which side should the Table of Contents sidebar be displayed for content pages. | **Right** |
| Show Print Button | Should the print button be displayed on all pages. Note that this doesn't prevent the user from printing the page using the system dialog. | :white_check_mark: |
{.table-leading-col}

# Code Injection

| Property | Description | Notes |
| :-- | :-- | :-- |
| CSS Override | DCSS code to inject after system default CSS. | :warning: Injecting too much CSS code can result in poor page load performance! |
| Head HTML Injection | HTML code to be injected just before the closing head tag. Usually for script tags. Applied the next time a page is loaded. | :warning: A user with `manage:theme` permission can inject malicious scripts using this field. Use caution when handing out this permission. |
| Body HTML Injection | HTML code to be injected just before the closing body tag. Applied the next time a page is loaded. | :warning: A user with `manage:theme` permission can inject malicious scripts using this field. Use caution when handing out this permission. |
{.table-leading-col}

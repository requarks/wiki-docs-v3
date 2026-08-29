---
title: Locale
description: Set localization options for your wiki
published: true
date: '2026-08-28T08:44:00.147Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-21T07:59:28.259Z'
---

# Overview

Wiki.js offers strong multi-language capabilities:

- The user interface can be changed to a different language.
- The ability to write content in multiple languages.
- [Link pages together](/guide/page-properties#set-locale-relations) as alternate languages of the same page.

> [!TIP]
> The term **language** refers to the written words / grammars, while the term **locale** refers to the cultural differences in formatting, presentation and conventions.
> For example, Portuguese (`pr`) is a **language** which has some differences depending on whether you're in **Portugal** (`pr-PT`) or **Brazil** (`pr-BR`), which are **locales**.
>
> By default, only the language code is used, unless a language has more than 2 locales, in which case the variant is appended to the language code.

# Site Locale Settings

From the **Administration Area**, click the **Locale** menu item from the sidebar.

| Parameter | Description |
| :-- | :-- |
| Primary Locale | The locale to use as default / fallback for this site. |
| Force Locale Prefix | Paths without a locale code will always be redirected to the primary locale. [More details](#force-locale-prefix). |
| Show Locale Menu | Display a locale selector in the sidebar, so visitors can switch to another active locale. |
{.table-leading-col}

> [!NOTE]
> The locale settings are per site. For example, one site could be strictly in English while another is available in 5 different languages.

## Force Locale Prefix

When this option is enabled, a user loading the homepage of a wiki site (e.g. `https://wiki.example.org/`) will automatically be redirected to `https://wiki.example.org/en/` if the primary locale is **English**. When off, the locale prefix is optional (both `/` and `/en/` will work without any redirects).

## Storage Considerations

When using multiple locales, extra care needs to be taken with your [storage targets](/admin/storage) configuration. Ensure to enable "**Add Locale Prefix**" option so that all content from different locales are stored in their distinct subdirectory. Otherwise only the primary locale will be stored and directly at the root.

# Install Locales

The **English** locale is included by default in Wiki.js.

You can fetch the latest list of locales by clicking the <kbd>Fetch Locales</kbd> button in the top-right corner of the page. This will download the list of available locales and updates for any installed locales.

To install a new locale, click the <kbd>:la:download: Install</kbd> button next to the desired locale to install it. It can then be activated in the **Active Locales** section.

## Custom Name / Short Code

In order to set a custom name and short code for a locale, click the <kbd>:la:pencil-alt:</kbd> button next to the desired locale.

This is useful in scenarios where you're using a single locale for a language with multiple variants. For example, you may want to only use **Portuguese Brazil** (`pr-BR`) and have it shown as just **Portuguese** (`pr`).

> [!IMPORTANT]
> Locales custom name and short codes are global to the wiki.

# Contribute translations

You can contribute new locales or improve existing ones. [Read more](/dev/translations) on how to contribute, no coding experience needed.

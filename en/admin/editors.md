---
title: Editors
description: Manage editors and their configuration
published: true
date: '2026-08-20T07:06:26.917Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-15T04:04:47.029Z'
---

> [!NOTE]
> This page is for administrators configuring the editors.
> For the guide on how to use them, refer to the [User Guide Editors](/guide/editors) page instead.

Wiki.js ships with multiple editors.

- Editors can be enabled or disabled by using the "**Active**" toggle on the right of the desired editor.
- Some editors have additional options you can configure by clicking the <kbd>:mdi:cog-outline: **Configuration**</kbd> button on the corresponding row. See the associated section below to learn about the various options.

# Markdown

The markdown editor is the fully-featured flagship editor for Wiki.js.

## Configuration

| Parameter | Description | Default Value | Notes |
| :-- | :-- | :-- | :-- |
| Allow HTML | Allow HTML tags in content. | :white_check_mark: |  |
| Auto-linking | Automatically convert URLs into clickable links. | :white_check_mark: |  |
| Auto Line Breaks | Automatically add linebreaks within paragraphs. | :white_check_mark: |  |
| Code Block Tab Width | Amount of spaces for each tab in code blocks. | `2` |  |
| MultiMarkdown Table | Enable support for MultiMarkdown Table features. | :white_check_mark: |  |
| Typographer | Enable some language-neutral replacement + quotes beautification. | :x: |  |
| Quotes Styles | When typographer is enabled. Double + single quotes replacement pairs. e.g. `«»„“` for Russian, `„“‚‘` for German, etc. | `English` | *Only available when **Typographer** is enabled.* |
| Underline Emphasis | Enable text underlining by using `_underline_` syntax. | :white_check_mark: |  |
{.table-leading-col}


# Redirect

The redirect editor allows users to create redirections to other pages or URLs.

## Configuration

*There's no configuration for this editor.*

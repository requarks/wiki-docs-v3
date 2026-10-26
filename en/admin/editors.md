---
title: Editors
description: Manage editors and their configuration
published: true
date: '2026-10-26T02:05:48.613Z'
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

# AsciiDoc Editor

The alternative plain-text editor using AsciiDoc syntax.

### Configuration

| Parameter | Description | Default Value | Notes |
| :-- | :-- | :-- | :-- |
| Math | Typeset LaTeX written with `latexmath:[…]` or `stem:[…]` within a line of text, and in `[latexmath]` or `[stem]` blocks, with the KaTeX or MathJax content block. stem always means LaTeX, and AsciiMath is shown as its source. When off, every formula is shown as its source. | `KaTeX` | That block ([KaTeX](/guide/blocks/katex) or [Mathjax](/guide/blocks/mathjax)) must also be enabled under Content Blocks. |
| Show minimap | Show a zoomed-out overview of the whole document along the right edge of the editor, for scrolling through long pages. | `false` |  |
{.table-leading-col}

# Blog

Create a blog inside your wiki.

### Configuration

*There's no configuration for this editor.*

# Feedback Board Editor

Collect ideas from your readers, let them vote, and tell them where each one stands.

### Configuration

| Parameter | Description | Default Value | Notes |
| :-- | :-- | :-- | :-- |
| Time Between Submissions | How long an account must wait after submitting an idea before it can submit another, on every board of this site. A duration such as 30s, 1m, 5m or 1h, or 0 for no limit. | `1m` | The rate limiter applies per user, not per IP. |
{.table-leading-col}

# Markdown Editor

The markdown editor is the fully-featured flagship editor for Wiki.js.

### Configuration

| Parameter | Description | Default Value | Notes |
| :-- | :-- | :-- | :-- |
| Allow HTML | Allow HTML tags in content. | :white_check_mark: |  |
| Auto-linking | Automatically convert URLs into clickable links. | :white_check_mark: |  |
| Auto Line Breaks | Automatically add linebreaks within paragraphs. | :white_check_mark: |  |
| Code Block Tab Width | Amount of spaces for each tab in code blocks. | `2` |  |
| Inline Math | Typeset TeX written as ``` $`E = mc^2`$ ``` within a line of text, with the KaTeX or MathJax content block. That block must also be enabled under Content Blocks. A dollar sign without the backticks is never treated as math. | `KaTeX` | That block ([KaTeX](/guide/blocks/katex) or [Mathjax](/guide/blocks/mathjax)) must also be enabled under Content Blocks. |
| MultiMarkdown Table | Enable support for MultiMarkdown Table features. | :white_check_mark: |  |
| Show minimap | Show a zoomed-out overview of the whole document along the right edge of the editor, for scrolling through long pages. | `false` |  |
| Typographer | Enable some language-neutral replacement + quotes beautification. | :x: |  |
| Quotes Styles | When typographer is enabled. Double + single quotes replacement pairs. e.g. `«»„“` for Russian, `„“‚‘` for German, etc. | `English` | *Only available when **Typographer** is enabled.* |
| Underline Emphasis | Enable text underlining by using `_underline_` syntax. | :white_check_mark: |  |
| Wikilinks | Link to pages by name with the `[[Page Name]]` and `[[Page Name|text]]` syntax. Spaces become dashes and letters are lowercased. | :white_check_mark: |  |
{.table-leading-col}


# Redirection

The redirect editor allows users to create redirections to other pages or URLs.

### Configuration

*There's no configuration for this editor.*

# Visual Editor

The editor for non-technical users.

### Configuration

*There's no configuration for this editor.*

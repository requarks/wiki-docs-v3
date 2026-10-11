---
title: Glossary
description: Define terms used across your wiki
published: true
date: '2026-10-11T06:29:02.976Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-10-09T03:57:46.946Z'
---

# Overview

A glossary is a collection of specialized terms. They are often technical words, abbreviations or codenames. The glossary lists those terms with a definition, reference links, aliases, related terms and more.

The glossary can be accessed via the :mdi:museum-outline: **Library** button in the header.

> [!NOTE]
> The glossary is **per locale** and **per site**.

# Adding Terms

To add a new term to the glossary, click the **:la:plus: New Term** button in the top-right corner.

Fill in the form to define the term:

| Field | Description |
| :-- | :-- |
| Term | The term to define (e.g. `REST`) |
| Expansion | The full form, if the term is an abbreviation. (e.g. `Representational State Transfer`) |
| Definition | The definition of the term. Basic markdown is supported. |
| Aliases | Alternate forms, spellings and inflections. Press <kbd>Enter</kbd> to add each one. |
| Related Terms | Related glossary terms. They are listed on both terms. The related term must already exist to select it. |
| Category | Groups terms together in the list. Press <kbd>Enter</kbd> to use a new one. |
| Documentation Page | The page on this wiki that documents the term, in the same locale. |
| :mdi:subdirectory-arrow-right: Link Label | Optional label for the documentation page link. Leave empty to use the default "Read more" label. |
| External References | Link(s) to external HTTP/S resources. Click the **Add Reference** button to add a new reference. |
| Case Sensitive | Only match text written with the exact same case, e.g. `REST` but not `rest`. Only used when auto-linking terms. |
| Auto-Link | Link the term where it appears in page text, the first time it is mentioned on each page. See [Auto-Linking Terms](#auto-linking-terms). |
{.table-leading-col}

# Viewing Terms

The list of glossary terms is displayed on the left. Click on a term to view its definition.

Terms are listed alphabetically by default. They can also be sorted by category by clicking the **Category** button at the top.

Use the search field at the top of the glossary overlay to find a specific term.

# Manage Terms

To edit or delete a glossary term, select it from the glossary list and click the :la:pen: **Edit** button or :la:trash: **Delete** button.

# Auto-Linking Terms

When a term has the "Auto-Link" property enabled, it will automatically be linked the first time it is mentioned on any page.

> [!NOTE]
> Auto-linking can be disabled per page via the **Link Glossary Terms** option in the [Page Properties](/guide/page-properties) dialog.

Terms can also be linked manually (refer to each [Editors](/guide/editors) guide for the usage / syntax). For example, in Markdown, terms can be linked manually using the `[[Glossary:TERM]]` syntax (where `TERM` is the glossary term).

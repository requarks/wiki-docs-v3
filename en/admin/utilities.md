---
title: Utilities
description: Maintenance and miscellaneous tools
published: true
date: '2026-11-20T08:24:09.220Z'
tags: []
editor: markdown
dateCreated: '2026-08-14T06:23:44.054Z'
---

# Overview

Utilities are miscellaneous maintenance tasks an administrator can run.

# Authentication Utilities

## Disconnect WebSocket Sessions

Force all active websocket connections to be closed, on every instance.

> [!CAUTION]
> This will disrupt live collaboration services and the admin terminal feature.

## Invalidate API Keys Certificates

Regenerate the passphrase and the keypair API keys are signed with. **Every key already issued stops working and must be reissued.**

> [!NOTE]
> User sessions are not affected.

## Invalidate User Sessions Secret

Rotate the secret used to sign session cookies and end every open session. **Everyone is logged out.**

> [!NOTE]
> API keys are not affected.

## Purge Revoked API Keys

Permanently delete the API keys that have been revoked. Invalidated keys are kept.

# Maintenance Utilities

## Delete Empty Folders

Delete every folder with no page or asset anywhere below it, on every site. A folder left holding only empty folders is deleted as well.

## Flush Cache

Files, icons and site settings are cached for better performance. Flushing forces everything to be fetched from the database again, on every instance.

## Purge History

Delete history *(content versioning)* older than the selected timeframe. **This applies to all sites.**

> [!CAUTION]
> - Pages keep the content they have now, but a discarded version cannot be brought back!
> - Any deleted page older than the selected timeframe cannot be recovered!

## Rebuild Page Links

Work out again what every page links to, from the content already stored, and mark the links that point to pages that do not exist. Runs in the background.

## Rebuild Page Ratings

Recalculate the rating totals shown on every page from the ratings actually recorded, in case they have fallen out of step.

## Rerender All Pages

Render every page on every site again from its source, in this browser. For pages that show a blank or out-of-date render, or after the markdown settings changed.

## Scan for Page Problems

Check every page on every site for empty or unreadable content, broken redirections, file tree entries out of step and more. Nothing is changed.

# Migration / Backup Utilities

## Import from Wiki.js 2.x

Migrate content from a Wiki.js 2.x backup. Refer to the [Upgrade from 2.x](/setup/upgrade#upgrade-from-2x) guide for instructions.

### Inputs

| Section | Parameter | Description |
| :-- | :-- | :-- |
| Destination | **Site to import into** | Everything in the archive is written to this site. |
| What to import || Assets, Pages, Comments, History, Groups, Users, Navigation and Settings |
| Options | **Overwrite on conflict** | What to do when the destination already has something at the same path, name or ID. *This is a destructive action. Existing content cannot be recovered!*{.text-negative} |
| ^^ | **Visual Editor Conversion** | 3.x uses markdown for the visual editor and requires a conversion from HTML to markdown to be editable. Should affected pages be converted to markdown to keep using the visual editor or stay as HTML but only editable as code? |
| Archive || Select the `.wkbackup` file to import. |
{.table-leading-col}

> [!TIP]
> The import is idempotent and can safely be performed multiple times. Existing items will be skipped unless the **Overwrite on conflict** option is checked.

## Import from Confluence

Migrate spaces, pages and comments from a Confluence backup (Cloud or Server / Data Center).

### Inputs

| Section | Parameter | Description |
| :-- | :-- | :-- |
| Source and Destination | **Site to import into** | Every space selected is written to this site. |
| ^^ | **Select backup...** | A .zip backup of a Confluence site, from Cloud (CSV) or Server / Data Center (XML). |
| Spaces || Each space selected is imported under its own path, with its home page at that path. Leave a path empty to import that space at the root of the site. |
| What to import || Pages, History, Comments and Attachments |
| Authors || Choose which account on this wiki becomes the author of each person's pages and comments. |
| Options | **Overwrite on conflict** | What to do when the destination already has something at the same path, name or ID. *This is a destructive action. Existing content cannot be recovered!*{.text-negative} |
| ^^ | **Page Format** | Confluence pages are HTML. Converted to markdown, they open in the visual editor; kept as HTML, they render the same but are only editable as code. |
{.table-leading-col}

> [!TIP]
> The import is idempotent and can safely be performed multiple times. Existing items will be skipped unless the **Overwrite on conflict** option is checked.

## Import from DokuWiki

Migrate pages, history and media from a DokuWiki data directory.

### Inputs

| Section | Parameter | Description |
| :-- | :-- | :-- |
| Source and Destination | **Site to import into** | Everything selected is written to this site. |
| ^^ | **Select zip / folder...** | The data directory of a DokuWiki install (or of the whole install), as a folder or a .zip of it. Include the conf folder to bring user names and email addresses along. |
| Namespaces | **Namespaces**| The namespaces selected are imported as folders, each with its start page at the folder's own path. DokuWiki's sample namespaces start unselected. |
| ^^ | **Import Under** | The path the wiki is imported under. Leave it empty to import at the root of the site, where the start page becomes the home page. |
| What to import || Pages, History, Media Files|
| Authors || Choose which account on this wiki becomes the author of each DokuWiki user's pages and files. Users with the same email address as an account are already matched. For anyone you leave as is, you will be the author. |
| Options | **Overwrite on conflict** | What to do when the destination already has something at the same path, name or ID. *This is a destructive action. Existing content cannot be recovered!*{.text-negative} |
| ^^ | **Page Format** | DokuWiki pages are converted from DokuWiki syntax. As markdown, they open in the visual editor; kept as HTML, they render the same but are only editable as code. |
{.table-leading-col}

> [!TIP]
> The import is idempotent and can safely be performed multiple times. Existing items will be skipped unless the **Overwrite on conflict** option is checked.

## Import from HedgeDoc

Bring the notes and accounts of a HedgeDoc instance in as live notes.

### Inputs

| Section | Parameter | Description |
| :-- | :-- | :-- |
| Source | **PostgreSQL Connection String** | The HedgeDoc database, as the wiki server reaches it. Only read from, and used for this import only: it is not stored anywhere. |
| ^^ | Upload URLs | Where HedgeDoc served uploaded images from, one per line, e.g. `https://notes.example.org/uploads/`. Images under these are copied into the notes that show them; any other image is left where it is. An upload server on a private address has to be allowed under **Security** :la:arrow-right: **Outbound Requests**. |
| Destination | **Site to import into** | Every note is imported as a live note of this site. Accounts are shared by every site. |
| Options | **Overwrite on conflict** | What to do when the site already has a live note under the same key. Off, the note is skipped. Existing accounts are never changed. *This is a destructive action. Existing notes cannot be recovered!*{.text-negative} |
{.table-leading-col}

## Import from XWiki

Migrate pages, history, attachments and comments from an XWiki XAR export.

### Inputs

| Section | Parameter | Description |
| :-- | :-- | :-- |
| Source and Destination | **Site to import into** | Everything selected is written to this site. |
| ^^ | **Select XAR...** | A XAR exported from XWiki. Export it with history to bring earlier versions along, and with the users' profile pages to bring their names and email addresses. |
| Spaces | **Spaces** | The spaces selected are imported as folders, each with its home page (WebHome) at the folder's own path. XWiki's own spaces start unselected. |
| ^^ | **Include hidden pages** | XWiki hides the pages that make up its own applications, skins and settings. Leave this off unless pages of your own content were hidden. |
| ^^ | **Import Under** | The path the wiki is imported under. Leave it empty to import at the root of the site, where XWiki's home page (Main.WebHome) becomes the home page. |
| What to import || Pages, History, Attachments and Comments |
| Authors || Choose which account on your wiki becomes the author of each XWiki user's pages, attachments and comments. |
| Options | **Overwrite on conflict** | What to do when the destination already has something at the same path, name or ID. *This is a destructive action. Existing content cannot be recovered!*{.text-negative} |
| ^^ | **Page Format** | XWiki pages are converted from XWiki syntax. As markdown, they open in the visual editor; kept as HTML, they render the same but are only editable as code. Pages written in markdown in XWiki are kept as they are. |
{.table-leading-col}

> [!TIP]
> The import is idempotent and can safely be performed multiple times. Existing items will be skipped unless the **Overwrite on conflict** option is checked.

# Testing Utilities

## Generate Sample Content

Fill this site with pages covering every kind of formatting and every block, in a folder tree several levels deep, a page with a busy discussion on it, plus a blog at /my-blog with 25 posts under it, and a home page linking to all of it if the site has none. Mostly for development / debugging purposes.

## Purge Sample Content

Delete every page on this site tagged "test", which is what Generate Sample Content tags the pages it writes.

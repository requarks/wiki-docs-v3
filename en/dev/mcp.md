---
title: MCP
description: Manage the Model Context Protocol server
published: true
date: '2026-10-21T06:20:04.798Z'
tags: []
editor: markdown
dateCreated: '2026-08-29T02:01:45.818Z'
---

# Overview

Wiki.js has an **optional** *(off by default)* built-in **Model Context Protocol (MCP) server**. With it, AI assistants such as Claude Code, Claude Desktop, VS Code, Cursor, and the claude.ai and ChatGPT connectors can **search and read** (and optionally **write and contribute to**) your wiki.

These assistants using the MCP endpoint always act **on behalf of a user** by using [Personal Access Tokens (PATs)](/guide/profile#personal-access-tokens). They can only perform actions the user is allowed to perform. The user can further limit access by selecting specific access scopes.

## Capabilities

### Answering from the wiki

The main use is letting an assistant answer questions from your documentation instead of from its own memory or from the web. For example:

- "What does our runbook say about rotating the database credentials?"
- "Which of our services still use the old auth library?"
- "Summarize the onboarding guide for a contractor."

To answer, an assistant can:

- **Search** with the wiki's own full-text search. It can filter by path, tags and locale, and each result comes with a snippet showing why it matched. If you don't name a locale, the search covers every locale of the site.
- **Browse the tree** to see what a section contains without reading every page in it.
- **Read a page** by its URL, by its path, or by its ID. A long page is read in parts: the outline first, then only the section that matters.
- **Follow links** in both directions: what a page links to and what links to it.
- **Read the history**: list a page's versions, read an old version, and compare two versions, including the reason given for each change.
- **Look up glossary terms**, where the wiki defines its own vocabulary.
- **Read comments** on a page *(built-in comments only)*.
- **List and view files and images**. An image comes back in a form the model can look at. This is optional and off by default.

Every answer can be cited. Each page in a result carries its URL, title, locale, last-updated date and version, so the assistant can link you to its source. Because the last updated date is always included, the assistant can tell you when the information it relies on is old.

### Contributing to the wiki

An assistant can write new / updated knowledge back:

- **Create a page** for something that isn't documented yet.
- **Update a page** that is wrong or out of date. Small, targeted edits are preferred over rewriting the whole page.
- **Suggest an edit** for the page's reviewers to approve, when the person doesn't have edit rights on that page.
- **Post a comment** to flag a problem. The comment can highlight the exact passages it refers to.
- **Define or update glossary terms** so they can be referred to in pages.
- **Upload an image or file**, such as a screenshot for a page *(optional, off by default)*.
- **Move or delete pages**. This is optional and off by default. A deleted page goes to the recycle bin.

An assistant's contribution is **an ordinary page edit**. It lives in the same tree, under the same page rules and in the same history as any other edit. It shows up in search and recent changes, it notifies the page's watchers, and it is mirrored to storage targets. Nothing an assistant writes is hidden, and anything it writes can be reviewed and reverted.

> [!NOTE]
> - **Every write needs a reason.** This applies even on sites where a reason for change is normally optional. The reason appears in the page history, and it becomes the commit message on a Git storage target.
> - **Every write is marked as made through MCP.** The version shows an **AI** badge next to the author's name in the page history, and on the page itself while the latest version is the assistant's version. The author is still the person who owns the token, because they are accountable for it. The badge tells readers which edits that person typed and which an assistant made for them. This badge can be hidden in the Administration Area.
> - **Writes are checked against the version the assistant read.** If someone saved the page in the meantime, the edit is refused and the assistant is shown the current version, so it never overwrites a change it didn't see.
> - **An edit is refused while someone has the page open in the editor** to prevent an assistant overwriting an active editing session. The assistant is told to suggest the edit or try again later.
> - **Broken links are reported.** After a write, the assistant is told about any links in the new content that don't lead to a page, so it can fix them in the same task.

### What it does not do

- **No administration.** There are no tools for users, groups, settings, storage or sites. A token can't reach the admin area, even if its owner is an administrator. This is by design and these actions are better served by the standard REST API.
- **No AI inside the wiki.** The wiki itself doesn't run a model, and it doesn't summarise, embed or rewrite anything. It simply doesn't make sense to add such features at the moment, which are better served by dedicated AI tools that can instead read and write to the wiki as needed.

# Getting Connected

## Requirements

- An administrator has enabled the necessary [prerequisites](#prerequisites) on your wiki.
- You belong in a group that holds the **`use:mcp`** permission. Otherwise, the **Connect an AI Assistant** tab under the **Profile** :la:arrow-right: **Personal Access Tokens** page will not be shown.

## Create a token

::block-steps
1. Go to the **Profile** :la:arrow-right: **Personal Access Tokens** page.
2. Open the **Connect an AI Assistant** tab.
3. Click the **Create a Token for an Assistant** button. This opens a dialog with read-only defaults preselected.
    > [!NOTE]
    > Any scope you select will be limited by the **AI Assistants (MCP)** scope. For example, to allow an assistant to write to pages, you must allow **Read & Write** on **BOTH** the **Pages** and **AI Assistants (MCP)** scopes.
4. Give it a name (e.g. "*Claude Code Read-Only*"), select an expiry and create the token.
5. Copy the token or use the provided commands/settings for your AI / IDE client.
    > [!IMPORTANT]
    > The token will **NOT** be shown again. Make sure to copy it before closing the dialog.
::

## Configure your client

The server URL is the wiki's own address followed by `/_mcp`, for example `https://wiki.example.com/_mcp`. **Each site answers on its own hostname** and an assistant connected to one site sees only that site.

**Claude Code**

```sh
claude mcp add --transport http wiki https://wiki.example.com/_mcp --header "Authorization: Bearer YOUR-TOKEN"
```

**VS Code**, in `.vscode/mcp.json`:

```json
{
  "servers": {
    "wiki": {
      "type": "http",
      "url": "https://wiki.example.com/_mcp",
      "headers": { "Authorization": "Bearer YOUR-TOKEN" }
    }
  }
}
```

**Cursor**, in `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "wiki": {
      "url": "https://wiki.example.com/_mcp",
      "headers": { "Authorization": "Bearer YOUR-TOKEN" }
    }
  }
}
```

Some remote connectors, such as **claude.ai** and **ChatGPT** can't be given a token. Add the server URL as a custom connector and sign in when the connector asks. See [Signing in with OAuth](#signing-in-with-oauth) below.

## Signing in with OAuth

The remote connectors in claude.ai and ChatGPT use OAuth 2.1 to sign in. There's nothing to set up on the wiki for this:

::block-steps
1. Add `https://wiki.example.com/_mcp` *(replacing `wiki.example.com` with your wiki's hostname)* as a custom connector in the client.
2. The client registers itself with the wiki and sends your browser to the wiki's **consent screen**. If you aren't signed in, you'll be prompted to sign in first.
3. The consent screen names the client, the address it will send you back to, and the account it will act as. It shows the scope grid, starting from what the client asked for, or from the read-only defaults if it asked for nothing. **You can change any row** before approving and you choose how long the grant lasts.
4. **Approve** and the connector is connected.
::

An OAuth grant behaves like a personal access token but with two differences: it works **only on the MCP server** and is refused on the REST API, and the tokens it issues last an hour and are refreshed automatically. Grants are listed under the **Profile** :la:arrow-right: **Personal Access Tokens** page with the client's name, marked *connected through OAuth*. Deleting one disconnects that client.

OAuth is available only while MCP, the API and Personal Access Tokens are all enabled.

## Disconnecting

Delete the token (or the OAuth connection) under the **Profile** :la:arrow-right: **Personal Access Tokens** page. It stops working immediately. An administrator can also delete a user's tokens from the user editor.

# Administration

MCP is configured under the **Administration Area** :la:arrow-right: **MCP** page.

> [!TIP]
> The sidebar light next to it shows whether the server is on. It turns amber when MCP is on but the API is off.

MCP is **one setting for the whole instance**. There is no per-site switch. Which sites and pages an assistant sees is decided by page rules, like everything else. The only per-site setting is the guidelines page.

Most settings on this screen need **`manage:system`**. The guidelines page needs **`manage:sites`**. Changes apply on the next call, on every instance, with no restart required.

## Enable / Disable

The button in the header turns the MCP server on or off for everybody. It is **off by default**. While it is off, `/_mcp` refuses every request and OAuth isn't offered.

## Prerequisites

The following prerequisites must be met before **MCP** can be enabled:

- **API** must be enabled. It can be enabled under the **Administration Area** :la:arrow-right: **API Access**. While the API is off, every token is refused and only anonymous access *(if enabled)* can work.
- **Personal Access Tokens** must be allowed. It is set under the **Administration Area** :la:arrow-right: **Authentication** :la:arrow-right: **Configuration**. While personal tokens are off, every token is refused *(existing tokens are kept and work again once the setting is back on)*, and only anonymous access *(if enabled)* can work.
- **Puppeteer** extension must be installed. It comes already installed in the container image; it can be installed via the **Administration Area** :la:arrow-right: **Extensions** if not. A page's HTML is normally produced by the editor's browser when it is saved. A page an assistant writes has no browser behind it, so it is rendered in the background by Puppeteer. A page that hasn't been rendered is blank to readers and invisible to search. Without the extension, `create_page` and `update_page` report that they are unavailable and point the assistant to `suggest_edit`. Comments, glossary terms, uploads and suggestions work without it.

## Tools

There is one switch per tool group, each labelled with the scopes its tools need. A group that is off is **offered to no one**, regardless of a token scopes.

- **The groups with write tools are on by default.** The scopes given to each token is what determine whether write is allowed. Turn **Create & Edit Pages** off if no assistant should edit pages directly on this wiki, regardless of what the tokens allow.
- **Assets** is off by default. Binary content is expensive in a model's context and an upload is the one write that isn't text a person can review in a diff.
- **Move & Delete Pages** is off by default, and turning it on shows a warning. Moves and deletions reorganize the wiki rather than add to it so enable with caution.

## Guidance

The **Guidelines Page** is a page on your wiki site, in its primary locale, whose text is given to every assistant that connects. Use it for the site's own conventions: where new pages go, how they are named, which sections are reference and which are history, and the house style. Example: `meta/assistant-guidelines`.

> [!TIP]
> - It is an ordinary page, so people and assistants can improve it like any other.
> - Up to 6,000 characters are included. An assistant receives the page only if its token's owner can read it.
> - Leave it empty for none. Assistants then get only the generic guidance.

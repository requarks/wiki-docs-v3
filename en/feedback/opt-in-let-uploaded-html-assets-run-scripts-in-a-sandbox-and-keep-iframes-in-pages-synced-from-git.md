---
title: >-
  Opt-in: let uploaded HTML assets run scripts in a sandbox, and keep iframes in
  pages synced from git
description: >-
  We use Wiki.js as the home for a team's design sketches and clickable
  prototypes. Each one is a single self-contained HTML file with its own CSS and
  JavaScript (tabs, filters, a prototype on made-up…
published: true
date: '2026-11-26T14:32:05.805Z'
tags: []
editor: markdown
dateCreated: '2026-11-26T14:32:05.805Z'
---

We use Wiki.js as the home for a team's design sketches and clickable prototypes. Each one is a single self-contained HTML file with its own CSS and JavaScript (tabs, filters, a prototype on made-up data). A wiki page per sketch describes it and embeds the file in an iframe. Content lives in git and syncs both ways, so developers can add sketches by pull request.

This works on 2.x. On 3.x (tested on 3.6.1) two things stop it, both on purpose as far as I can tell:

1. Every asset except a PDF is served with `Content-Security-Policy: default-src 'none'; img-src data:; style-src 'unsafe-inline'; sandbox` (`ASSET_CSP` in `backend/models/assets.ts`). So no script in an uploaded HTML file runs, whatever the security settings say. Turning off `forceAssetDownload` only removes the download.
2. A page imported from a storage target is rendered with no `write:scripts`, and only `write:scripts` keeps an `<iframe>` (`inheritedPermissions` in `backend/models/rendering.ts`). A page that comes in through git loses its embed, and nothing brings it back short of someone with `write:scripts` saving it in the editor.

I understand why both defaults are there: an uploaded file should not run in the wiki's origin, and a file in a repository is not vouched for by whoever ran the import.

**What would solve it without weakening the default:**

- A security setting, off by default, for which extensions (or folders) are served as *sandboxed interactive* content: the same `sandbox` directive plus `allow-scripts` (and perhaps `allow-popups`, `allow-forms`), with `default-src 'self' 'unsafe-inline' data: blob:`. Without `allow-same-origin` the file still runs in an opaque origin, so it cannot reach the wiki's cookies or API. That keeps the guarantee behind the current CSP ("runs nothing in the wiki's origin") while letting the file work.
- For storage imports: a per-target option such as "trust this target's content with `write:scripts` / `write:styles`", meant for a repository whose push access is already limited to people who hold those permissions in the wiki. Push access to the remote is effectively write access to the wiki already, so the option would only make the render match that.

For now we serve the sketches from a separate static server and link to them from the wiki pages, which works but loses the inline view. Happy to test a build or a branch.

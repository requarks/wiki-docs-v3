---
title: >-
  Git storage: sync only selected folders (path include/exclude) instead of the
  whole site
description: >-
  Hi Wiki.js team, and thanks for 3.0! We’ve upgraded from 2.x and are really
  enjoying the multi-site model, live collaboration and the new editors. There’s
  one thing we keep running into with the Git…
published: true
date: '2026-11-15T00:55:42.201Z'
tags:
  - storage
editor: markdown
dateCreated: '2026-11-14T18:37:44.556Z'
---

Hi Wiki.js team, and thanks for 3.0!

We’ve upgraded from 2.x and are really enjoying the multi-site model, live collaboration and the new editors. There’s one thing we keep running into with the Git storage target, and we couldn’t find it in the docs or on the feedback board, so here’s a request.

The need

We would like to sync a specific folder (a path prefix) of a site with a Git repository, rather than the whole site.

Typical cases:

A wiki has a section of technical or product documentation that should live in a Git repository (reviewed, versioned, reused by CI), while the rest of the wiki is internal and should not leave Wiki.js.
Several teams share a site, and each team wants its own folder mirrored to its own repository.
Some content is sensitive and must stay out of Git, while the folder next to it is perfectly fine to export.

What we found

As far as we can tell, the Git target is configured per site and exports every page of the site. The site-level storage settings control things like path layout, locale/site prefixes and the sync interval, but we didn’t see a way to restrict which paths are synced. The 2.x docs also state that the repository must be dedicated to Wiki.js and that a subfolder can’t be used. In the API, each site has one target per storage module, so we can’t declare several Git targets with different scopes either.

Current workarounds (and why they aren’t ideal)

Creating a dedicated site per synced section: it works, but it forces a hostname per section and splits content that belongs together.
Using a webhook plus a small custom service that filters by path and commits to the repository: it works for Wiki.js → Git, but it means maintaining our own code, and writing back requires a personal access token.

Suggested behaviour (just an idea, happy with any approach)

On a storage target, an optional list of included paths and an optional list of excluded paths (prefix match, maybe globs).
Optionally, a target subdirectory in the repository, so a folder can be mirrored under docs/ in a larger repo instead of requiring a dedicated repo.
Ideally, the ability to enable more than one Git target per site, each with its own repository and path scope.
The same filter would apply to import, so nothing outside the scope is created or overwritten when pulling from Git.

Why it matters

It would let teams keep sensitive pages in Wiki.js only, publish documentation to Git without exposing the rest, and avoid creating one site per repository.

Thanks for considering it, and for all the work on Wiki.js!

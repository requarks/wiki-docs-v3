---
title: 'Discussion: optional per-site storage and file-count quotas'
description: >-
  Hi Wiki.js team, I’m Ludovic, and I manage a self-hosted Wiki.js installation
  with multiple sites. I’d like to discuss optional per-site quotas to prevent
  one site from consuming a disproportionate s…
published: true
date: '2026-11-17T21:09:22.892Z'
tags:
  - storage
editor: markdown
dateCreated: '2026-11-16T21:44:09.157Z'
---

Hi Wiki.js team,

I’m Ludovic, and I manage a self-hosted Wiki.js installation with multiple sites.

I’d like to discuss optional per-site quotas to prevent one site from consuming a disproportionate share of storage. Each site would have two independent limits:

- Maximum storage in decimal GB.
- Maximum number of retained files or content objects.

We have developed a prototype for our installation, with an administration interface showing usage, limits and a breakdown by content category. Limits can remain unlimited, and lowering a limit never automatically deletes existing content.

Our implementation currently counts retained content, including attachments, page sources, rendered pages, history, previews and storage copies. Each retained copy counts separately; links do not create additional copies.

Before proposing code, I’d appreciate your feedback on whether this feature fits Wiki.js and what accounting scope you would prefer. Would you favour quotas limited to uploaded files, or a broader retained-content budget?

An implementation is already available, including tests and documentation. I’m sharing it as a prototype for discussion, before opening a pull request.

The prototype has automated tests covering PostgreSQL transactions and concurrency, plus real local disk, S3-compatible, SFTP and Git storage scenarios. Some provider-specific behaviour still requires further validation.

I understand this is a substantial change. I’m happy to discuss a narrower scope and a manageable contribution structure rather than submit a large unsolicited pull request.

Thank you for your time and for maintaining Wiki.js.

Ludovic

---
title: Utilities
description: Maintenance and miscellaneous tools
published: true
date: '2026-08-14T06:31:13.562Z'
tags: []
editor: markdown
dateCreated: '2026-08-14T06:23:44.054Z'
---

# Overview

Utilities are miscellaneous maintenance tasks an administrator can run.

# Available Utilities

## Disconnect WebSocket Sessions

Force all active websocket connections to be closed, on every instance.

> [!CAUTION]
> This will disrupt live collaboration services and the admin terminal feature.

## Flush Cache

Files, icons and site settings are cached for better performance. Flushing forces everything to be fetched from the database again, on every instance.

## Invalidate API Keys Certificates

Regenerate the passphrase and the keypair API keys are signed with. **Every key already issued stops working and must be reissued.**

> [!NOTE]
> User sessions are not affected.

## Invalidate User Sessions Secret

Rotate the secret used to sign session cookies and end every open session. **Everyone is logged out.**

> [!NOTE]
> API keys are not affected.

## Purge History

Delete history *(content versioning)* older than the selected timeframe. **This applies to all sites.**

> [!CAUTION]
> - Pages keep the content they have now, but a discarded version cannot be brought back!
> - Any deleted page older than the selected timeframe cannot be recovered!

## Purge Revoked API Keys

Permanently delete the API keys that have been revoked. Invalidated keys are kept.

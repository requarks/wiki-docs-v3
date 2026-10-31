---
title: Configurable WebAuthn RP ID for multisite passkeys
description: >-
  I’d like to see an option to configure the WebAuthn Relying Party ID (RP ID),
  allowing a single passkey to work across multiple Wiki.js sites hosted on
  subdomains of the same parent domain. Currently…
published: true
date: '2026-10-31T19:32:05.495Z'
tags: []
editor: markdown
dateCreated: '2026-10-31T19:32:05.495Z'
---

I’d like to see an option to configure the WebAuthn Relying Party ID (RP ID), allowing a single passkey to work across multiple Wiki.js sites hosted on subdomains of the same parent domain.

Currently, Wiki.js 3 uses the site’s hostname as the RP ID when registering and authenticating passkeys. Although passkeys are associated with the shared user account and appear in the user’s profile across all sites, they can only be used to authenticate on the hostname where they were registered.

For example, with the following sites:

* wiki.example.com
* manuals.wiki.example.com
* ideas.wiki.example.com
* tasks.wiki.example.com

A passkey registered on manuals.wiki.example.com cannot be used on the other sites.

WebAuthn supports using a common parent domain (wiki.example.com) as the RP ID, allowing the same passkey to authenticate across all these subdomains.

Proposed solution

Allow the RP ID to be configured, either through an environment variable (e.g. WEBAUTHN_RP_ID) or through the Wiki.js configuration.

When no RP ID is configured, Wiki.js should continue using the current hostname, preserving existing behaviour.

Working proof of concept

I’ve successfully implemented and tested this on my Wiki.js 3 beta multisite installation.

The change required replacing the four occurrences of rpID: hostname / rpId: hostname in backend/models/passkeys.ts with:

rpID: process.env.WEBAUTHN_RP_ID || hostname

(and the equivalent rpId assignments).

With WEBAUTHN_RP_ID set to the shared parent domain, I registered a new passkey on one site and successfully authenticated on another site where I had never previously logged in.

The existing per-site origin verification remains unchanged.

This would make passkeys considerably more convenient for multisite installations without changing the default behaviour for existing users.

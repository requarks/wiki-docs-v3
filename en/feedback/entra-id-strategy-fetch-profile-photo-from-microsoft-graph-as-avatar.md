---
title: 'Entra ID strategy: fetch profile photo from Microsoft Graph as avatar'
description: >-
  Summary The Entra ID strategy has a Picture Claim setting, but Entra ID
  doesn't provide the Microsoft 365 profile photo as an image URL in the token.
  The photo is only available through Microsoft Gra…
published: true
date: '2026-11-19T12:24:26.592Z'
tags: []
editor: markdown
dateCreated: '2026-11-19T12:24:26.592Z'
---

**Summary**
 The Entra ID strategy has a Picture Claim setting, but Entra ID doesn't provide the Microsoft 365 profile photo as an image URL in the token. The photo is only available through Microsoft Graph.

As a result, Entra ID users get the initials avatar in Wiki.js even when they have a profile photo in Microsoft 365.

**Proposal**
 Add an option to the Entra ID strategy: "Fetch profile photo from Microsoft Graph".

When enabled:

Fetch the user's photo after sign-in using GET https://graph.microsoft.com/v1.0/me/photo/$value.
Store it as the user's Wiki.js avatar.
Keep the existing avatar/initials when no photo exists.
Refresh the photo periodically or when it has changed.
Don't overwrite a manually uploaded avatar when the user opts out of synchronization.

This would allow Wiki.js avatars to stay consistent with Teams, Outlook and other Microsoft 365 services.


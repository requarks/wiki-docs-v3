---
title: Discord
description: Authentication strategy
published: true
date: '2026-09-08T22:36:55.067Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:36:55.067Z'
---

# Overview

Sign in with a Discord account, optionally only from the members of one Discord server.

# Guide

*Coming soon*

# Configuration

> [!TIP]
> To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Client ID | From the OAuth2 page of the application registered in the Discord Developer Portal. |  |
| Client Secret | From the same OAuth2 page. Discord shows it once, so reset it there if it was not noted. |  |
| Restrict to Server | (optional) The ID of a Discord server — turn on Developer Mode in Discord, then right-click the server and Copy Server ID. Only its members may sign in. Required to map groups, since a role belongs to a server. |  |
| Map Groups | Put the user in the wiki groups their roles on that server name, on every login. Only groups that already exist here are matched — nothing is created. Needs a Server ID. | :x: |
| :mdi:subdirectory-arrow-right: Bot Token | (optional) A bot token for an application that is a member of the server, from the Bot page of the Developer Portal. With one, roles are matched by NAME. Without one, Discord only tells this wiki a role's numeric ID and a group here has to be named as that ID to match. |  |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer held on the server | Off adds what the roles name and takes nothing away, so a membership granted here survives. On makes the Discord server the authority instead, and a role taken away there is taken away here — bar the groups this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}


---
title: Discord
description: Authentication strategy
published: true
date: '2026-09-09T09:33:04.974Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:36:55.067Z'
---

# Overview

Sign in with a Discord account, optionally only from the members of one Discord server.

# Guide

1. In your wiki installation, go to **Administration** :la:arrow-right: **Authentication**.
    1. Add a new **Discord** strategy.
    1. Click **Apply** in order to generate the *Authorization Callback URL*.
    1. Copy the the **Authorization Callback URL** shown at the bottom (under the **Configuration Reference** section).
    1. Leave this page opened.
1. In a new tab, sign in to Discord and go to [**Discord Developer Portal :la:arrow-right: Applications**](https://discord.com/developers/applications).
    1. Click **New Application**
    1. Give it a **name** (e.g. `My Wiki`), accept the terms and click **Create**.
    1. Go to the **OAuth2** tab.
    1. Under the **Redirects** section, click **Add redirect** and paste the **Authorization Callback URL** you copied in step 1.
    1. Click outside the field and click **Save changes** at the bottom.
    1. Copy the **Client ID** and click the **Reset secret** button to generate a new **Client Secret**. Copy it as it won't be shown again.
1. Go back to the Wiki.js page from step 1.
    1. Paste the **Client ID** and **Client Secret** you copied in step 2.
    1. Set **Enabled** to on at the top.
    1. Click **Apply**.
1. For the desired wiki site, go to **Login**.
    1. Enable the **Discord** strategy you just created.
    2. Click **Apply**.

> [!IMPORTANT]
> If you want any Discord account to be able to login, you need to enable **Registration** option on the GitHub strategy you created. Otherwise, only existing accounts with an email address that match the Discord account will be allowed to login.

## Restricting to a server

Filling in the **Restrict to Server** field lets only members of that Discord server in. To find the ID:

1. In the Discord client, open **User Settings** :la:arrow-right: **Advanced** and turn on **Developer Mode**.
1. Right-click the server in the sidebar and choose **Copy Server ID**.

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


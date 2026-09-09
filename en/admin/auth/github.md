---
title: GitHub
description: Authentication strategy
published: true
date: '2026-09-09T09:08:29.198Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T11:09:03.826Z'
---

# Overview

Sign in with a GitHub account, on github.com or a GitHub Enterprise Server.

# Guide

1. In your wiki installation, go to **Administration** :la:arrow-right: **Authentication**.
    1. Add a new **GitHub** strategy.
    1. Click **Apply** in order to generate the *Authorization Callback URL*.
    1. Copy the the **Authorization Callback URL** shown at the bottom (under the **Configuration Reference** section).
    1. Leave this page opened.
1. In a new tab, sign in to GitHub and go to [**Settings :la:arrow-right: Developer settings :la:arrow-right: OAuth Apps**](https://github.com/settings/developers) for personal accounts or **Organization Settings :la:arrow-right: Developer settings :la:arrow-right: OAuth Apps** for organizations.
    1. Click **New OAuth App**
    1. Fill in the **Application name** (e.g. `My Wiki`) and the **Homepage URL** (e.g. `https://wiki.example.org`) fields.
    1. Enter the URL you copied in step 1 in the **Redirect URI** field.
    1. Click **Register application** and copy the **Client ID**.
    1. Click **Generate a new client secret** and copy the generated **Client Secret**.
1. Go back to the Wiki.js page from step 1.
    1. Paste the **Client ID** and **Client Secret** you copied in step 2.
    1. Set **Enabled** to on at the top.
    1. Click **Apply**.
1. For the desired wiki site, go to **Login**.
    1. Enable the **GitHub** strategy you just created.
    2. Click **Apply**.

> [!IMPORTANT]
> If you want any GitHub account to be able to login, you need to enable **Registration** option on the GitHub strategy you created. Otherwise, only existing accounts with an email address that match the GitHub account will be allowed to login.

## Restricting to an organization

Fill in the **Restrict to Organization** field to restrict login only to members of the organization.

> [!IMPORTANT]
> GitHub only reveals a private membership to an app the organization has approved. Therefore you need to either approve the app under **Organization Settings** :la:arrow-right: **OAuth app policy** or have each member set their membership to public.
>
> Failing to do so will result in authentication failure.

# Configuration

> [!TIP]
> To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Client ID | From the OAuth app registered under Developer settings. |  |
| Client Secret | From the same OAuth app. |  |
| GitHub Enterprise Host | *(optional)* Hostname of a GitHub Enterprise Server, e.g. github.example.com. Leave empty for github.com. |  |
| Restrict to Organization | *(optional)* Login name of a GitHub organization. Only its members may sign in — which needs the account to be a public member, or the OAuth app to be approved by the organization. Required to map groups, since a team belongs to an organization. |  |
| Map Groups | Put the user in the wiki groups their teams in that organization name, on every login. Matched on the team's name as GitHub shows it, not its URL slug — only groups that already exist here are matched, and nothing is created. Needs Restrict to Organization. | :x: |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in claim | Off adds what the teams name and takes nothing away, so a membership granted here survives. On makes the organization the authority instead, and a team somebody is removed from there is taken away here — bar the groups this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}


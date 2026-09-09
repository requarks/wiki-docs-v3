---
title: Google
description: Authentication strategy
published: true
date: '2026-09-09T21:20:59.636Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:22:52.363Z'
---

# Overview

Sign in with a Google account or a Google Workspace domain.

# Guide

1. In your wiki installation, go to **Administration** :la:arrow-right: **Authentication**.
    1. Add a new **Google** strategy.
    1. Click **Apply** in order to generate the *Authorization Callback URL*.
    1. Copy the the **Authorization Callback URL** shown at the bottom (under the **Configuration Reference** section).
    1. Leave this page opened.
1. In a new tab, sign in to the [Google Cloud console](https://console.cloud.google.com/).
    1. In the project picker at the top, click **New Project**. If your organization uses Google Workspace, make sure to create the project **inside your organization** rather than under your personal account.
    1. Give it a name (e.g. `My Wiki`) and click **Create**.
    1. Ensure the newly created project is selected before continuing.
    1. Go to **API & Services** :la:arrow-right: **OAuth consent screen**.
    1. Click the **Get started** button.
    1. Enter a **App name** (e.g. `My Wiki`) and a **User support email**. Click **Next**.
    1. Choose the audience and click **Next**:
        1. **Internal**: Only accounts in your Google Workspace organization can login.
        1. **External**: Any Google account can login. Note that you'll need to publish the app to allow any account to login. While in testing mode, only the list of users you specify can login.
    1. Fill in the contact information and click **Next**.
    1. Accept the terms and click **Continue**. Then click **Create**.
    1. Go to the **Clients** page and click **Create client**.
    1. Select **Web Application** as the application type, and give it a name (e.g. `My Wiki`).
    1. Under the **Authorized redirect URIs** section, click **Add URI** and paste the **Authorization Callback URL** you copied in step 1.
    1. Click **Create**.
    1. Copy the **Client ID** and the **Client Secret**.
1. Go back to the Wiki.js page from step 1.
    1. Paste the **Client ID** and **Client Secret** you copied in step 2.
    1. Set **Enabled** to on at the top.
    1. Click **Apply**.
1. For the desired wiki site, go to **Login**.
    1. Enable the **Google** strategy you just created.
    2. Click **Apply**.

> [!IMPORTANT]
> If you want any Google account authorized by the configuration above to be able to login, you need to enable **Registration** option on the Google strategy you created. Otherwise, only existing accounts with an email address that match the Google account will be allowed to login.

# Configuration

> [!TIP]
> To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Client ID | From the OAuth 2.0 Client ID created in the Google Cloud console. |  |
| Client Secret | From the same OAuth 2.0 Client ID. |  |
| Restrict to Workspace Domain | A Workspace domain, e.g. example.com. Only accounts on it may sign in — checked here as well as asked for, since the parameter alone is a hint to Google rather than a guarantee. |  |
| Accept Unverified Addresses | Off by default. A Google account whose address is unverified proves nothing about the mailbox, and an account here is matched on the address. | :x: |
| Map Groups | Put the user in the wiki groups their Google Workspace groups name, on every login. Only groups that already exist here are matched — nothing is created. Workspace only, and it needs the Cloud Identity API enabled on the Google Cloud project this OAuth client belongs to. | :x: |
| :mdi:subdirectory-arrow-right: Match Groups By | Which of the two things a Workspace group has is matched against the names of the groups here — the address, engineering@example.com, or the display name, Engineering. The address is unique and survives a rename; the display name reads better, but two groups may share one and then both match. | `Group address` |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in Workspace | Off adds what Workspace names and takes nothing away, so a membership granted here survives. On makes Workspace the authority instead, and a group somebody is removed from there is taken away here — bar the groups this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}


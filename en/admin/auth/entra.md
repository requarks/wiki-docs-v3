---
title: Microsoft Entra ID
description: Authentication strategy
published: true
date: '2026-09-09T10:09:10.043Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:28:46.438Z'
---

# Overview

Microsoft Entra ID (formerly Azure Active Directory) is Microsoft's cloud-based identity and access management service.

# Guide

1. In your wiki installation, go to **Administration** :la:arrow-right: **Authentication**.
    1. Add a new **Microsoft Entra ID** strategy.
    1. Click **Apply** in order to generate the *Authorization Callback URL*.
    1. Copy the the **Authorization Callback URL** shown at the bottom (under the **Configuration Reference** section).
    1. Leave this page opened.
1. In a new tab, sign in to the [**Microsoft Entra admin center**](https://entra.microsoft.com) and go to **App registrations** in the sidebar.
    1. Click **New registration**
    1. Give it a **Name** (e.g. `My Wiki`)
    1. Select **Single tenant** for the **Supported account types**.
    1. Under **Redirect URI**, select **Web** for the type and paste the **Authorization Callback URL** you copied in step 1.
    1. Click **Register** at the bottom.
    1. On the app's **Overview** page, copy the **Application (client) ID** and the **Directory (tenant) ID** values.
    1. On the app's **Certificates & Secrets** page, under the **Client secrets** tab, click **New client secret** and give it a description and expiry *(24 months is the maximum)*, and click **Add**.
    1. Copy the **Value** column (and **NOT** the Secret ID).
1. Go back to the Wiki.js page from step 1.
    1. Paste the **Directory (tenant) ID**, **Application (client) ID** and **Client Secret** values you copied in step 2.
    1. Set both **Enabled** and **Registration** to on at the top. Registration **MUST** be enabled in order to automatically create accounts that are authorized from Entra ID. Otherwise, only existing accounts in Wiki.js will be able to login.
    1. Click **Apply**.
1. For the desired wiki site, go to **Login**.
    1. Enable the **Microsoft Entra ID** strategy you just created.
    2. Click **Apply**.

> [!IMPORTANT]
> Entry only fills the `email` claim when the account has a **Mail** attribute. If this isn't the case, set the **Email Claim** to `preferred_username` *(or add an optional `email` claim in Entra for the token)*.

## Mapping groups

**Map Groups** puts each user in the wiki groups the token's groups claim names on every login. Only groups that already exist in Wiki.js are matched.

Entra doesn't include that info by default. It needs to be added in the token configuration:

1. Open the app's **Token configuration** page and click **Add groups claim**.
2. Choose which groups to emit: **Security groups** or **Groups assigned to the application** if the directory is large.
3. Expand **ID** and pick what the claim carries:
   - **Group ID** *(default)*: Object GUIDs. A wiki group then has to be named as the GUID to match.
   - **sAMAccountName** or **NetBIOS Domain + sAMAccountName**: Group names and much easier to work with, but only available for groups synced from on-premises Active Directory.

Leave the strategy's **Groups Claim** as `groups` unless you emit it under another name.

# Configuration

> [!TIP]
> To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Directory (tenant) ID | The tenant this wiki signs people in from — its GUID, or one of its verified domains. From the app registration's Overview page. |  |
| Application (client) ID | The app registration's own GUID, from the same Overview page. |  |
| Client Secret | A secret value from the app registration's Certificates & secrets page. Note the value, not the secret ID — Entra shows it once. |  |
| Email Claim | Which claim carries the email address. Entra fills `email` from the account's Mail attribute, or from the optional claim of that name; a tenant that populates neither has the address in `preferred_username` instead. | `email` |
| Display Name Claim | Which claim carries the name to show. Falls back to the email address when the claim is absent. | `name` |
| Picture Claim | Which claim carries the URL of the account's picture, fetched on login and stored as the avatar. Empty by default because Entra sends no such claim unless the app registration is set up to map one. |  |
| Map Groups | Put the user in the wiki groups the groups claim names, on every login. Only groups that already exist here are matched — nothing is created. | :x: |
| :mdi:subdirectory-arrow-right: Groups Claim | Which claim carries the groups. Configure the app registration's token to emit it — note that Entra sends group object IDs unless the tenant is synced from Active Directory and set to emit sAMAccountName, so a wiki group has to be named to match whatever arrives. | `groups` |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in claim | Off adds what the claim names and takes nothing away, so a membership granted here survives. On makes Entra the authority instead, and a group it stops naming is taken back — bar the ones this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}


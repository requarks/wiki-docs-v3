---
title: Microsoft Entra ID
description: Authentication strategy
published: true
date: '2026-09-08T22:28:46.438Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:28:46.438Z'
---

# Overview

Microsoft Entra ID (formerly Azure Active Directory) is Microsoft's cloud-based identity and access management service.

# Guide

*Coming soon*

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


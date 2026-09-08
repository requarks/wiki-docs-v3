---
title: Google
description: Authentication strategy
published: true
date: '2026-09-08T22:22:52.363Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:22:52.363Z'
---

# Overview

Sign in with a Google account or a Google Workspace domain.

# Guide

*Coming soon*

# Configuration

> [!TIP]
> To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Client ID | From the OAuth 2.0 Client ID created in the Google Cloud console. |  |
| Client Secret | From the same OAuth 2.0 Client ID. |  |
| Restrict to Workspace Domain | *(optional)* Login name of a GitHub organization. Only its members may sign in — which needs the account to be a public member, or the OAuth app to be approved by the organization. Required to map groups, since a team belongs to an organization. |  |
| Accept Unverified Addresses | Off by default. A Google account whose address is unverified proves nothing about the mailbox, and an account here is matched on the address. | :x: |
| Map Groups | Put the user in the wiki groups their Google Workspace groups name, on every login. Only groups that already exist here are matched — nothing is created. Workspace only, and it needs the Cloud Identity API enabled on the Google Cloud project this OAuth client belongs to. | :x: |
| :mdi:subdirectory-arrow-right: Match Groups By | Which of the two things a Workspace group has is matched against the names of the groups here — the address, engineering@example.com, or the display name, Engineering. The address is unique and survives a rename; the display name reads better, but two groups may share one and then both match. | `Group address` |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in Workspace | Off adds what Workspace names and takes nothing away, so a membership granted here survives. On makes Workspace the authority instead, and a group somebody is removed from there is taken away here — bar the groups this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}


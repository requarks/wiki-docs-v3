---
title: GitHub
description: Authentication strategy
published: true
date: '2026-09-08T11:09:03.826Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T11:09:03.826Z'
---

# Overview

Sign in with a GitHub account, on github.com or a GitHub Enterprise Server.

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


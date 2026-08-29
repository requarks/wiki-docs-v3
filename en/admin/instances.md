---
title: Instances
description: View a list of active instances
published: true
date: '2026-08-20T07:07:14.412Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-16T22:57:22.553Z'
---

# Overview

The **Instances** page lists all Wiki.js instances currently connected to the same database.

In order to provide high-availability for you wiki, you may want to run multiple replicas of Wiki.js. This is useful for serving wikis with very large amount of traffic. All replicas are automatically kept in sync.

# Reported Info

| Property | Description |
| :-- | :-- |
| ID | The unique identifier, IP and database user of the instance. |
| Active Connections | The number of active connections this instance has to the database. |
| Active Listeners | The number of event listeners to the database. |
| First Seen | The datetime the instance first connected to the database. |
| Last Seen | The datetime the instance last queried the database. |
{.table-leading-col}


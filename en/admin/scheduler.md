---
title: Scheduler
description: View scheduled and completed jobs
published: true
date: '2026-10-29T01:54:27.782Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-08-20T07:03:34.424Z'
---

# Overview

The scheduler manages all scheduled tasks, one-off jobs and background workers.

You're not expected to perform any action in this view and is mostly provided for observability.

> [!NOTE]
> For high-availability installations, the scheduler will automatically select a random available node to run jobs.

## Views

| View | Description |
| :-- | :-- |
| Schedule | List of scheduled jobs that run on a regular basis. A job run can be triggered manually via the <kbd>:la:play:</kbd> button. |
| Upcoming | List of upcoming job runs that are about to run in the next hours / minutes. A job run can be cancelled via the <kbd>:la:window-close:</kbd> button. |
| Active | List of job runs currently running. Unless a job run is taking a long time to run, this view will likely be empty. |
| Completed | List of recently completed job runs. A job run can be triggered again using the <kbd>:la:undo-alt:</kbd> button. |
| Failed | List of recently failed job runs. A job run can be triggered again using the <kbd>:la:undo-alt:</kbd> button. |
{.table-leading-col}

## Execution Mode

Jobs can either run **In-Process** or in a **Worker**. Lightweight jobs will run in the same process as the main thread while heavier tasks will use a separate worker to run, to avoid overloading the main process.

---
title: Webhooks
description: Manage webhooks to external services
published: true
date: '2026-08-17T07:16:25.873Z'
tags: []
editor: markdown
dateCreated: '2026-08-17T07:16:25.873Z'
---

# Overview

Webhooks are endpoints to be called upon specific events. This is useful for automation with external services.

For example, you may want an API to be notified when a new page is created or updated.

# New Webhook

To create a new webhook, click the **New Webhook** button in the top-right corner of the page.

::block-gallery{thumbnailSize="640" fit="contain" unlockAspectRatio="true"}
![admin-webhook-new.png](/admin/images/admin-webhook-new.png)
::

| Property | Description |
| :-- | :-- |
| Name | Name of the webhook |
| Events | Select one or more events that should trigger this webhook. Refer to the [Events](#events) sections below for details. |
| URL | The remote endpoint URL to call when this webhook is triggered |
| Include Metadata | Should the payload include metadata such as title, description, author, etc. |
| Include Content | Should the payload include content (e.g. the full page body). Make sure that your remote endpoint can accept large payloads! |
| Accept untrusted SSL certificates | It is recommended that you leave this off for proper security. |
| Authentication Header | *(optional)* The value of the `Authorization` header to send along the request. |
{.table-leading-col}

# Manage Webhooks

A webhook will stay in **Pending** state until an event triggers it for the first time.

- Click the **Edit** button next to the desired webhook to edit its configuration.
- Click the **Delete** button next to the desired webhook to permanently delete it. You'll be prompted to confirm before deletion.

# Events

*todo*

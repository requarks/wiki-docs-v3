---
title: Suggest Edits
description: >-
  Allow read-only users to submit edits to existing pages and review them before
  publishing
published: true
date: '2026-08-24T00:07:05.576Z'
tags:
  - user-guide
  - editing
editor: markdown
dateCreated: '2026-08-17T20:35:50.510Z'
---

# Overview

The [Approvals](/admin/approvals) feature lets administrator define rules about which set of pages can accept edit submissions from read-only users.

Reviewers are then able to [review the submissions](#review-submissions) and publish the changes.

# Workflow

## Approval Rules

An administrator must first create one or more approval rules in the [Administration Area :mdi:arrow-right: Approvals](/admin/approvals).

## Suggest Edits

When a page matches an [approval rule](/admin/approvals) and a user is an allowed group, the **Suggest Edits** button appears in the top-right corner of the page:

![approvals-suggest-edits-btn.png](/guide/images/approvals-suggest-edits-btn.png =160x)

Upon clicking it, the page switches to editor mode.

> [!NOTE] Assets Access / Upload
> A user can only view and upload assets to folders allowed by the user group permissions. Guests cannot upload assets regardless of permissions.

When ready, click the **Submit Edits** button in the top-right corner to send the submission for review. If you're not logged in (and the Guests group is allowed to submit edits), you'll be prompted to provide a name and email address for attribution.

Users marked as reviewers for this page will be notified and will be able to [review the submission](#review-submissions).

As long as a submission is not approved or rejected, you can click the **Suggest Edits** button to keep editing your submission with further changes.

## Review Submissions

Reviewers can view active submissions in their **Inbox** page (click the <kbd>:mdi:inbox-full:</kbd> button in the top-right corner), under the **Pending Review** tab.

Select a submission to view the proposed changes. You have the option to either **Approve** or **Reject** a submission. Upon approval, the page is updated with the proposed changes and they become part of the page history timeline.

---
title: Local Authentication
description: Authentication strategy
published: true
date: '2026-09-08T23:12:31.600Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T23:12:31.600Z'
---

# Overview

Built-in authentication for Wiki.js

> [!NOTE]
> This strategy cannot be disabled. You can however hide it from each site's Login page authentication methods

# Configuration

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Enforce Two-Factor Authentication | Users will be required to set up 2FA the first time they login, and cannot turn it off afterwards. | :x: |
| Email Validation | Send a verification email with a validation link when somebody registers, and refuse them a login until they follow it. Requires a configured mail server — registration is refused outright without one. | :white_check_mark: |
| Allow Forgot Password | Users who have forgotten their password can request a reset link by email from the login screen. Turn this off where passwords are handed out rather than chosen. | :white_check_mark: |
{.table-leading-col}


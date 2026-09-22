---
title: SCIM Provisioning
description: Let an identity provider create and deactivate accounts
published: true
date: '2026-09-22T17:44:57.284Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-09-20T06:36:16.971Z'
---

# Overview

**System for Cross-domain Identity Management** (SCIM) provides a common interface for an identity provider to create and deactivate accounts. This reduces the complexity of user management by keeping the state of users in sync with the identity provider.

Wiki.js is compliant with the [SCIM 2.0 specification](https://scim.cloud/).

## SCIM Provisioners

Some popular providers that can act as a SCIM provisioner:
| Identity Provider | Notes |
| :-- | :-- |
| Authentik | Using the built-in SCIM provider |
| JumpCloud | Using **Identity Management** on a custom SCIM app |
| Keycloak | Using the `scim-for-keycloak` extension |
| Microsoft Entra ID | Under **Enterprise application** :la:arrow-right: **Provisioning** |
| Okta | Using the **SCIM 2.0** app integration |
| OneLogin | Using the **SCIM Provisioner** with SAML |
| Ping Identity | Using **PingOne** / **PingFederate** |
{.table-leading-col}

# Configuration

> [!IMPORTANT]
> Both the **SCIM Provisioning** and the **REST API** must be enabled for the endpoint to work. The **REST API** can be enabled under the **Administration Area** :la:arrow-right: **API Access**.

*docs coming soon*

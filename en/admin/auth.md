---
title: Authentication
description: Configure the authentication settings of your wiki
published: true
date: '2026-09-08T23:16:09.834Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T10:32:04.629Z'
---

# Overview

Wiki.js comes with local authentication by default. This is the standard email & password combination found on most websites.

However, it's possible add 3rd-party authentication providers in order to login using your pre-existing identity solution. You can add any number of strategies and select the ones that should be available for each site.

> [!IMPORTANT]
> Once an authentication strategy is enabled, it becomes available to be associated to any site.
> You **MUST** therefore first activate it under each site's **Administration** :la:arrow-right: **Login** page. Only then will it be displayed on the login screen.

# Strategies

::block-index{path="admin/auth" showIcons="true"}
::

> [!TIP]
> If you're looking for strategies previously found in Wiki.js 2.x, such as **Dropbox**, **Facebook**, **GitLab**, **Keycloak**, **Okta**, **Rocket.chat**, **Slack** or **Twitch**, use the [OpenID Connect / OAuth2](/admin/auth/oidc) strategy instead.

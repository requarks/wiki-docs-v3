---
title: Authentication
description: Configure the authentication settings of your wiki
published: true
date: '2026-09-30T20:33:33.777Z'
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
> Once an authentication strategy is enabled, it becomes ready to be associated to any site.
> You **MUST** therefore first activate it under each site's **Administration** :la:arrow-right: **Login** page. Only then will it be displayed on the login screen.

# Strategies

::block-index{path="admin/auth" showIcons="true"}
::

> [!TIP]
> If you're looking for strategies previously found in Wiki.js 2.x, such as **Dropbox**, **Facebook**, **GitLab**, **Keycloak**, **Okta**, **Rocket.chat**, **Slack** or **Twitch**, use the [OpenID Connect / OAuth2](/admin/auth/oidc) strategy instead.

# Reverse Proxies

If you're using a reverse proxy (like nginx, Cloudflare Tunnels, etc.), you need to perform this extra configuration so that the callback URL is using the correct values.

- Ensure **Trust X-Forwarded-\* Proxy Headers** is enabled under **Administration Area** :la:arrow-right: **Security**. Failure to do so will result in the redirect URL being incorrectly set to the "http" protocol and potentially an internal hostname.
- If you have multiple sites, you need to allow the hostnames for all your sites in the authentication provider.
- In your reverse proxy configuration, ensure the hostname and protocol X-Fowarded-* headers are properly set.

Refer to the requirements [Reverse Proxy](/setup/requirements#reverse-proxy) section for more details and examples.

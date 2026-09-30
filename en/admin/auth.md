---
title: Authentication
description: Configure the authentication settings of your wiki
published: true
date: '2026-09-30T19:40:12.467Z'
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
- In your reverse proxy configuration, ensure the hostname and protocol X-Fowarded-* headers are properly set.

### NGINX Example

```nginx linesHighlight="22-25"
server {
  listen 80;
  server_name wiki.example.com;
  return 301 https://$host$request_uri;
}

server {
  listen 443 ssl;
  http2 on;
  server_name wiki.example.com;

  ssl_certificate     /etc/ssl/wiki.example.com/fullchain.pem;
  ssl_certificate_key /etc/ssl/wiki.example.com/privkey.pem;

  # At least the wiki's uploadMaxFileSize (10 MB by default); nginx's own default is 1 MB
  client_max_body_size 10m;

  location / {
    proxy_pass http://127.0.0.1:3000;
    proxy_http_version 1.1;

    # Auth callback URL is built from these
    proxy_set_header Host              $host;
    proxy_set_header X-Forwarded-Host  $host;
    proxy_set_header X-Forwarded-Proto $scheme;

    # Client address, for rate limiting, the audit log and metrics access
    proxy_set_header X-Real-IP         $remote_addr;
    proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;

    # Websockets: real-time collaboration (/_collab)
    proxy_set_header Upgrade    $http_upgrade;
    proxy_set_header Connection $connection_upgrade;
    proxy_read_timeout 3600s;
  }
}
```


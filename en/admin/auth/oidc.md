---
title: OpenID Connect / OAuth2
description: Authentication strategy
published: true
date: '2026-09-10T05:00:17.669Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T10:34:04.850Z'
---

# Overview

OpenID Connect 1.0 (OIDC) is a simple identity layer on top of the OAuth 2.0 protocol.

Unless there's a dedicated strategy for your authentication provider already (e.g. [Discord](/admin/auth/discord), [Google](/admin/auth/google), [GitHub](/admin/auth/github)), this is most likely the strategy you're looking for.

[View guides for common providers :la:chevron-right:](#providers-docs)

# Configuration

> [!TIP]
> To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Client ID | Application Client ID, as the provider issued it. |  |
| Client Secret | Application Client Secret, as the provider issued it. |  |
| Issuer | The provider's issuer URL, e.g. `https://id.example.com`. Everything else is discovered from it. |  |
| Use Discovery | Read the endpoints and signing keys from the issuer's `/.well-known/openid-configuration`. Turn off only for a provider that does not publish one, and fill in the endpoints below. | :white_check_mark: |
| :mdi:subdirectory-arrow-right: Authorization Endpoint URL | Where the browser is sent to log in. |  |
| :mdi:subdirectory-arrow-right: Token Endpoint URL | Where the authorization code is exchanged for tokens. |  |
| :mdi:subdirectory-arrow-right: User Info Endpoint URL | Optional - the ID token alone can carry everything needed. |  |
| :mdi:subdirectory-arrow-right: Pass access token via GET query string to User Info Endpoint | Pass the access token in an `access_token` parameter attached to the GET query string of the User Info Endpoint URL. Otherwise the access token will be passed in the Authorization header. | :x: |
| :mdi:subdirectory-arrow-right: JSON Web Key Set URL | Where the keys that signed the ID token are published. Without it the ID token cannot be verified and logins are refused. |  |
| :mdi:subdirectory-arrow-right: Logout URL | Optional - Where the browser is sent once the wiki has logged somebody out, so that the provider's own session ends too — its `end_session_endpoint`. Discovery finds this on its own, which is why it is only asked for here. Without it, signing out leaves the provider still signed in and the next login goes through without a password being asked for. |  |
| Scopes | Space-separated. `openid` is required; `email` is what an account is matched on here. | `openid profile email` |
| Use ACR Values | Optional - Ask the provider for a particular kind of sign-in — two-factor, a smart card, a specific policy — by naming the authentication context this wiki wants. |  |
| :mdi:subdirectory-arrow-right: ACR Values | Space-separated Authentication Context Class References, most preferred first, as the provider documents them. e.g. `urn:mace:incommon:iap:silver`, or a policy name the provider defines. |  |
| :mdi:subdirectory-arrow-right: Require the authentication context | Refuse a login whose `acr` claim is not one of the values above. Off, they are only a request — OpenID Connect lets a provider ignore them and still answer with a valid token, so without this the setting expresses a preference rather than a requirement. Turn it on once the provider is known to return the claim, since one that returns none refuses everybody. | :x: |
| ID Claim | Which claim carries the provider's own identifier for the account. Usually sub or id, which never changes. | `sub` |
| Email Claim | Which claim carries the email address. | `email` |
| Display Name Claim | Which claim carries the name to show. Falls back to the email address when the claim is absent. | `name` |
| Picture Claim | Which claim carries the URL of the account's picture, fetched on login and stored as the avatar. Leave empty to let people keep whatever avatar they set here. | `picture` |
| Map Groups | Put the user in the wiki groups a claim names, on every login. Only groups that already exist here are matched, by name and ignoring case — nothing is created. | :x: |
| :mdi:subdirectory-arrow-right: Groups Claim | Which claim carries the group names. Either one name or a list of them. | `groups` |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in claim | Off adds what the claim names and takes nothing away, so a membership granted here survives. On makes the provider the authority instead, and a group it stops naming is taken back — bar the ones this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}

## Group Mapping

When **Map Groups** is enabled, groups listed in the `groups` claim *(or the one defined via the **Groups Claim** property)* are used for comparison against the Wiki.js groups. If there's a match, the user is automatically assigned to that group.

The groups claim can be either a single string or an array of strings.

> [!IMPORTANT]
> If the `groups` claim requires a special scope, make sure to add it to the **Scopes** field.

By enabling the **Unassign from groups no longer present in claim** as well, the identity provider becomes the sole source of truth for group assignment. On login, the user will be unassigned from any Wiki.js group that isn't listed in the `groups` claim.

# Providers Docs

Below are some of the most popular OIDC / OAuth2 providers compatible with this strategy; with links to their documentation:

- [Authentik](https://integrations.goauthentik.io/documentation/wiki-js/){target=_blank}
- [Dropbox](https://developers.dropbox.com/oauth-guide){rel="nofollow" target=_blank}
- [Facebook](https://developers.facebook.com/documentation/facebook-login){rel="nofollow" target=_blank}
- [GitLab](https://docs.gitlab.com/integration/openid_connect_provider/){rel="nofollow" target=_blank}
- [Keycloak](https://www.keycloak.org/securing-apps/oidc-layers){rel="nofollow" target=_blank}
- [Okta](https://developer.okta.com/docs/api/openapi/okta-oauth/guides/overview){rel="nofollow" target=_blank}
- [Rocket.chat](https://docs.rocket.chat/docs/third-party-login){rel="nofollow" target=_blank}
- [Slack](https://docs.slack.dev/authentication/sign-in-with-slack/){rel="nofollow" target=_blank}
- [Twitch](https://dev.twitch.tv/docs/authentication/){rel="nofollow" target=_blank}

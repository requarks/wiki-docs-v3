---
title: OAuth2
description: Authentication strategy
published: true
date: '2026-11-16T08:28:52.291Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-11-16T08:23:26.917Z'
---

# Overview

Sign in through any OAuth 2.0 provider that answers who the user is from a user info endpoint, without an ID token (e.g Mattermost and Rocket.Chat).

> [!IMPORTANT]
> In most cases, you should instead use the [OIDC / OpenID Connect](/admin/auth/oidc) strategy. Only use the OAuth2 strategy for providers that don't support the ID token

[View guides for common providers :la:chevron-right:](#providers-docs)

# Configuration

> [!TIP]
> - To obtain the **Authorization Callback URL**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.
> - **If you're using a reverse proxy**, make sure you followed the [Reverse Proxy](/setup/requirements#reverse-proxy) setup section first. Otherwise the callback URL may be incorrect and result in authentication failures.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Client ID | Application Client ID, as the provider issued it. |  |
| Client Secret | Application Client Secret, as the provider issued it. |  |
| Authorization Endpoint URL | Where the browser is sent to log in. |  |
| Token Endpoint URL | Where the authorization code is exchanged for an access token. |  |
| User Info Endpoint URL | Where the access token is spent to learn who signed in. It must answer with a JSON object about the account the token belongs to — every claim below is read from it. |  |
| Logout URL | Optional - Where the browser is sent once the wiki has logged somebody out, so that the provider's own session ends too. Sent as it is — OAuth2 has no standard way of asking the provider to send the browser back afterwards. Without it, signing out leaves the provider still signed in and the next login goes through without a password being asked for. |  |
| Allow Insecure HTTP | Allow the endpoints above to be plain `http://` URLs. Off, they must be `https://`. They carry the authorization code, the client secret and the access token, and over plain HTTP anything between the wiki, the browser and the provider can read them. Turn on only for a provider on a network you trust, such as a test server. | :x: |
| Client Authentication | How the Client ID and Secret are presented to the token endpoint. In the request body is what most providers that are not OpenID Connect expect; the Authorization header is the one RFC 6749 says every provider must accept. Only one is sent — a provider may refuse a request carrying both. Either `In the request body (client_secret_post)` or `In an Authorization header (client_secret_basic)`. | `In the request body (client_secret_post)` |
| Use PKCE | Bind the authorization code to this login with a PKCE challenge, so that a code intercepted on its way back is useless to anybody else. Providers that do not support it generally ignore it; turn it off only for one that refuses the login because of it. | :white_check_mark: |
| Scopes | Optional - Space-separated, as the provider documents them. Left empty, no scope is asked for and the provider grants its default. | |
| Pass access token via GET query string to User Info Endpoint | Pass the access token in an `access_token` parameter attached to the GET query string of the User Info Endpoint URL. Otherwise the access token will be passed in the Authorization header, which is the one to use — the query string puts a live credential in every access log between here and the provider. | :x: |
| ID Claim | Which field of the user info answer carries the provider's own identifier for the account — one that never changes, not a username that can be renamed. Usually `id` *(Mattermost)* or `sub` *(Rocket.Chat's /oauth/userinfo)*. A number is accepted too. A dotted path reaches into a nested object, e.g. `data.id`, and a number in it indexes a list. | `id` |
| Email Claim | Which field carries the email address, e.g. `email`, or `emails.0.address` for a list of them. | `email` |
| Require Verified Email | Refuse a login or registration unless the provider says it has verified the email address. An account here is matched by address, so an unverified one says nothing about who holds the mailbox — on a provider that lets people type in any address they like, it is a way into somebody else's account. | :x: |
| :mdi:subdirectory-arrow-right: Verified Email Claim | Which field says the email address was verified, e.g. `email_verified`, or `emails.0.verified`. Only `true` (also as the string "true", in any casing) or `1` counts; anything else, the field missing included, refuses the login. | `email_verified` |
| Display Name Claim | Which field carries the name to show, e.g. `name`, or `username` for a provider with no full name in one field. Falls back to the email address when the field is absent. | `name` |
| Picture Claim | Optional - Which field carries the absolute URL of the account's picture, fetched on login and stored as the avatar. It is fetched without the access token, so a picture the provider only serves to a signed-in client cannot be used. Leave empty to let people keep whatever avatar they set here. | `picture` |
| Handle Claim | Optional - Which field carries the person's mention handle, e.g. `username` or `preferred_username`. Copied to their profile on every login, replacing what was set here. A value that is not 3 to 32 letters, digits, hyphens and underscores, or that another account already holds, is skipped and the handle left as it was. Leave empty to let people pick their own. | |
| Location Claim | Optional - Which field carries where the person is. Copied to their profile on every login, replacing what was set here. Leave empty to let people set their own. | |
| Job Title Claim | Optional - Which field carries the person's job title, e.g. `position`. Copied to their profile on every login, replacing what was set here. Leave empty to let people set their own. | |
| Pronouns Claim | Optional - Which field carries the person's pronouns. Copied to their profile on every login, replacing what was set here. Leave empty to let people set their own. | |
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

Below are some of the most popular OAuth2 providers compatible with this strategy; with links to their documentation:

- [Mattermost](https://docs.mattermost.com/developers/integrate/apps/authentication/oauth2){rel="nofollow" target=_blank}
- [Rocket.chat](https://docs.rocket.chat/docs/third-party-login){rel="nofollow" target=_blank}

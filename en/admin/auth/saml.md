---
title: SAML 2.0
description: Authentication strategy
published: true
date: '2026-09-08T23:06:11.832Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T23:06:11.832Z'
---

# Overview

Security Assertion Markup Language 2.0, the standard for exchanging authentication and authorization data between security domains.

# Configuration

> [!TIP]
> To obtain the **Assertion Consumer Service URL** and **Service Provider Metadata**, you must first click **Apply** on the newly added strategy *(It won't be active until you check the **Enabled** checkbox)*. The endpoint URL will then be displayed at the bottom of the page under the **Configuration Reference** section.

| Property | Description | Default Value |
| :-- | :-- | :-- |
| Entry Point | The identity provider's single sign-on URL, where the browser is sent to log in. |  |
| Issuer | The entity ID this wiki identifies itself to the provider as. Any stable string the provider is told to expect — a URL naming this wiki is the convention. |  |
| Audience | (optional) The audience an assertion must be restricted to for this wiki to accept it. Defaults to the Issuer above, which is what a provider configured against this wiki will send. |  |
| Certificate | The provider's public PEM-encoded X.509 signing certificate, which is what every assertion is checked against. Join several with the \| pipe symbol where the provider is rotating keys. |  |
| Private Key | (optional) PEM-formatted key this wiki signs its authentication requests with. Only needed by a provider that requires signed requests. |  |
| Signing Certificate | The public PEM-encoded X.509 certificate matching the private key above. Required alongside it, because it is what the metadata document publishes for the provider to verify this wiki's requests with. |  |
| Decryption Private Key | (optional) PEM-formatted key used to decrypt encrypted assertions. Only needed by a provider that encrypts them. |  |
| Decryption Certificate | The public PEM-encoded X.509 certificate matching the decryption key above. Required alongside it, because it is what the metadata document publishes for the provider to encrypt assertions to. |  |
| Signature Algorithm | Which algorithm this wiki signs its requests with. SHA-1 is broken and is here only for a provider that accepts nothing else. One of SHA-256, SHA-512 or SHA-1 (insecure). | SHA-256 |
| Digest Algorithm | Which algorithm digests the data being signed. Match it to the signature algorithm unless the provider asks otherwise. One of SHA-256, SHA-512 or SHA-1 (insecure). | SHA-256 |
| Name Identifier Format | What kind of name the request asks the provider to identify people by. Leave empty to ask for no particular format, which is what a provider that objects to being asked wants. | `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress` |
| Require Signed Assertions | Refuse a response whose assertion is not signed in its own right. Worth leaving on — a signature over the response alone leaves the assertion inside it unprotected. | :white_check_mark: |
| Accepted Clock Skew (ms) | How far this server's clock may differ from the provider's before an assertion is judged not yet valid or expired. Set to -1 to stop checking those timestamps entirely, which throws away the assertion's own expiry. | 0 |
| Disable Requested Auth Context | Ask for no particular authentication method, rather than the one below. Known to be what AD FS wants. | :x: |
| :mdi:subdirectory-arrow-right: Auth Context | Which authentication method the request asks for. Join several with the \| pipe symbol. | `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` |
| :mdi:subdirectory-arrow-right: RAC Comparison Type | How the provider is to compare what it actually did against the context asked for. One of exact, minimum, maximum or better. | exact |
| Force Initial Re-authentication | Ask the provider to authenticate the person again even if they already have a session there. | :x: |
| Passive | Ask the provider not to interact with the person at all — so an existing session signs them in and no session sends them straight back. | :x: |
| Provider Name | (optional) A human-readable name for this wiki, which a provider may show to the person being asked to log in. | Wiki.js |
| Request Binding | How the authentication request reaches the provider. Redirect sends the browser straight there; POST answers with a page holding a form that submits itself, which under a content security policy forbidding inline scripts becomes a button the person has to press. | Redirect |
| Skip Request Compression | Send the authentication request uncompressed. The Redirect binding requires it to be deflated, so this is for a provider that wants otherwise. | :x: |
| Unique ID Field Mapping | The attribute holding the provider's own identifier for the account. Falls back to the assertion's NameID, which is what most providers identify people by. | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier` |
| Email Field Mapping | The attribute holding the email address. An account here is matched on it, so an assertion without one cannot sign anybody in. | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |
| Display Name Field Mapping | The attribute holding the name to show. Falls back to the email address when the assertion has neither. | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` |
| Avatar Picture Field Mapping | The attribute holding the URL of the account's picture, fetched on login and stored as the avatar. Leave empty to let people keep whatever avatar they set here. | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/picture` |
| Map Groups | Put the user in the wiki groups the attribute below names, on every login. Only groups that already exist here are matched, by name and ignoring case — nothing is created. | :x: |
| :mdi:subdirectory-arrow-right: User Groups Field Mapping | The attribute holding the groups. Either one name or a list of them. | `memberOf` |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in assertion | Off adds what the assertion names and takes nothing away, so a membership granted here survives. On makes the provider the authority instead, and a group it stops naming is taken back — bar the ones this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |

{.table-leading-col}


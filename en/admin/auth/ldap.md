---
title: LDAP / Active Directory
description: Authentication strategy
published: true
date: '2026-09-09T09:09:32.515Z'
tags:
  - admin
  - auth
editor: markdown
dateCreated: '2026-09-08T22:48:42.051Z'
---

# Overview

Lightweight Directory Access Protocol, as spoken by Active Directory, OpenLDAP, FreeIPA and everything else that holds a directory of people.

# Configuration

| Property | Description | Default Value |
| :-- | :-- | :-- |
| LDAP URL | e.g. `ldap://directory.example.com:389`, or `ldaps://directory.example.com:636` for a connection that is encrypted from the start. | `ldap://localhost:389` |
| Admin Bind DN | The distinguished name of the account this wiki searches the directory as. It needs to read the user entries and nothing more. | `cn=readonly,dc=example,dc=com` |
| Admin Bind Credentials | The password of the account above. |  |
| Search Base | The base DN under which to look for the person signing in. | `ou=people,dc=example,dc=com` |
| Search Filter | How a username is turned into one entry. `{{username}}` must appear and is substituted with what was typed, escaped. e.g. `(uid={{username}})` or `(sAMAccountName={{username}})`. | `(uid={{username}})` |
| Use StartTLS | Upgrade a plain `ldap://` connection to TLS before anything is sent over it. Leave off for an `ldaps://` URL, which is encrypted already. | :x: |
| Verify TLS Certificate | Check the directory's certificate against the trusted authorities. Turning this off means the connection is encrypted but the server is not identified, which is no protection at all against something sitting in the middle of it. | :white_check_mark: |
| TLS Certificate Path | (optional) Absolute path, on the server, to the PEM certificate authority to trust in addition to the system's own. For a directory using an internal CA. |  |
| Unique ID Field Mapping | The attribute holding the directory's own identifier for the entry. Usually `uid` or `sAMAccountName`. It has to be one that is never reassigned. | `uid` |
| Email Field Mapping | The attribute holding the email address, usually `mail`. An account here is matched on it, so an entry without one cannot sign in. | `mail` |
| Display Name Field Mapping | The attribute holding the name to show. Usually `displayName` or `cn`. Falls back to the email address when the entry has neither. | `displayName` |
| Avatar Picture Field Mapping | The attribute holding the account's photo, usually `jpegPhoto` or `thumbnailPhoto` — the image itself, not a link to one. Leave empty to let people keep whatever avatar they set here. | `jpegPhoto` |
| Map Groups | Put the user in the wiki groups their directory groups are named after, on every login. Only groups that already exist here are matched, by name and ignoring case — nothing is created. | :x: |
| :mdi:subdirectory-arrow-right: Group Search Base | The base DN under which to look for the groups an entry belongs to. | `ou=groups,dc=example,dc=com` |
| :mdi:subdirectory-arrow-right: Group Search Filter | Which groups count as the user's. `{{dn}}` is substituted with the value of the property below, escaped. `(member={{dn}})` is right for most directories. | `(member={{dn}})` |
| :mdi:subdirectory-arrow-right: Group Search Scope | How far below the Group Search Base to look. `sub` searches the whole subtree, `one` its immediate children, `base` only the entry itself. | `sub` |
| :mdi:subdirectory-arrow-right: Group DN Property | Which property of the user's entry `{{dn}}` stands for in the filter above. Usually `dn`. | `dn` |
| :mdi:subdirectory-arrow-right: Group Name Field | The attribute on a group entry holding the name to match a wiki group against. Usually `name` or `cn`. | `name` |
| :mdi:subdirectory-arrow-right: Unassign from groups no longer present in directory | Off adds what the directory says and takes nothing away, so a membership granted here survives. On makes the directory the authority instead, and a group it stops naming is taken back — bar the ones this strategy auto-enrolls into, which are granted here to everyone it lets in. | :x: |
{.table-leading-col}


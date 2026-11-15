---
title: >-
  Delegated group management: let a group manage the members of specific other
  groups
description: >-
  Hi Wiki.js team, and congratulations on the 3.0 release! We migrated from 2.x
  a few days ago and we’re really enjoying it, especially multi-site and live
  collaboration. While setting up our instance,…
published: true
date: '2026-11-15T00:54:31.031Z'
tags:
  - auth
editor: markdown
dateCreated: '2026-11-14T18:42:29.497Z'
---

Hi Wiki.js team, and congratulations on the 3.0 release!

We migrated from 2.x a few days ago and we’re really enjoying it, especially multi-site and live collaboration. While setting up our instance, we hit one small thing that we think would make life easier for a lot of teams, so we wanted to share it.

What we’d love to do

Let the members of one group manage who is in some other groups, without handing them the keys to every group on the instance.

A real example from our setup: teachers should be able to add and remove students from the “students” group of their own site, but they should never be able to touch the administrators group or the groups of other sites.

What we ran into

From the API documentation, assigning or removing a user from a group (and updating a group) requires write:groups, manage:groups or manage:system. These permissions apply to the whole instance, so giving them to a teacher means giving them access to every group. We couldn’t find a way to limit them to a few groups, and we weren’t comfortable granting something that might let someone assign themselves to a more privileged group. (We may well be missing an option, and if there is one we’d be glad to hear about it!)

What we tried instead

Managing membership in our identity provider: it works, but it means giving non-technical users access to the provider’s admin console, which is a heavier setup than we’d like.
Doing it ourselves as administrators: fine for a handful of people, but it doesn’t scale, and users only exist in Wiki.js after their first login, so we can’t prepare things ahead of time.

An idea, in case it’s useful

A group-level setting like “can manage the members of these groups”, where you pick the target groups.
Managers could add and remove members of those groups only. They wouldn’t be able to edit the groups’ rules or permissions, or assign anything that gives more access than they already have.
Elevated groups, like administrators, would be left out by default.
Every change made this way would show up in the audit log.

Why we think it would help

On an instance shared by several teams or sites, it would let the people closest to the work take care of their own groups safely, and save instance administrators from handling every membership change.

Thank you for reading, and for building such a great tool!

---
title: Timestamp
description: A date and time in a line of text, shown in the reader's own timezone.
published: true
date: '2026-10-31T07:32:25.708Z'
tags:
  - blocks
editor: markdown
dateCreated: '2026-10-31T07:32:25.708Z'
---

# Description

A date and time in a line of text, shown in the reader's own timezone.

# Demo

The next meeting is on :block-timestamp[2030-04-01T12:00:00Z]{length="full"}.

The last event was :block-timestamp[2026-11-01T12:00:00Z]{format="relative"}.

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `format` | `datetime` | `datetime`, `date`, `time` or `relative` |
| `length` | `medium` | `short`, `medium`, `long` or `full` |
| `precision` | `minute` | `minute` or `second` |
| `timezone` | `UTC` | Any valid IANA name, e.g. `Europe/Paris`, that a value with no offset of its own is read in. The reader always sees their own timezone. |
{.table-leading-col .table-code-nohighlight}

:block-timestamp[2026-01-01T12:00:00Z]{timezone=""}

# Default Code

````md
:block-timestamp[2026-01-01T12:00:00Z]
````


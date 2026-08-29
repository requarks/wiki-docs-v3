---
title: Countdown
description: Counts down to a date and time.
published: true
date: '2026-08-16T23:59:41.328Z'
tags: []
editor: markdown
dateCreated: '2026-08-12T08:36:42.693Z'
---

# Description

Counts down to a date and time.

# Demo

::block-countdown{date="2040-01-01" label="Countdown to 2040-01-01"}
::

# Parameters

| Parameter | Default Value | Possible Values |
| :-- | :-- | :-- |
| `date` | `<required>` | ISO timestamp, e.g. `2026-01-01` or `2026-01-01T12:00:00` |
| `timezone` | `UTC` | *see dropdown list* |
| `label` | `<none>` | `-` |
| `expiredMsg` | `The countdown has ended.` | `-` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-countdown{date="2026-12-25T09:00"}
::
````



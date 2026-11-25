---
title: >-
  Credit approved suggestion authors on the page: "last edited by" and,
  optionally, per-line attribution
description: >-
  Summary When a reviewer approves an edit suggestion, the page records only the
  reviewer as its author. The person who actually wrote the change disappears
  from the page entirely: no mention in the si…
published: true
date: '2026-11-25T11:32:12.188Z'
tags: []
editor: markdown
dateCreated: '2026-11-25T11:32:12.188Z'
---

## Summary

When a reviewer approves an edit suggestion, the page records only the reviewer as its author. The person who actually wrote the change disappears from the page entirely: no mention in the sidebar, no author in the version history, nothing in the source view. For a wiki whose whole point is collaborative writing, a contributor whose improvement is accepted never sees that their work landed.

I would like the page to credit them. Minimally, the sidebar's "Last edited by" block should be able to include the suggestion's author. Ideally, a reader should be able to tell which lines came from a suggestion, and from whom.

## Current behaviour

An approved suggestion is applied as an ordinary page edit, attributed to the reviewer who approved it.
The suggestion itself is then discarded, so the submitter's name is no longer associated with the change.
The sidebar shows a single author — the reviewer — with no indication that the change originated as a suggestion.
Nothing in the version history, the source view or anywhere on the page names the submitter.
The only surviving trace is outside the page (an administrative audit entry, a webhook event). Neither is visible to a reader, and the audit trail expires on schedule.
Proposed behaviour
Two tiers, so the first can ship without committing to the second.

### Tier 1 — credit the submitter alongside the edit

Keep the suggestion author's identity attached to the version that the approval produced, instead of discarding it.
Show it wherever the page already attributes an edit:
the sidebar's "Last edited by" block: e.g. Jane Doe, from a suggestion by Bob Smith;
the version history: the same annotation on that version;
the source view and any public page data, so themes and custom layouts can use it.
Distinguish "accepted as written" from "accepted after the reviewer rewrote it". Crediting someone for a suggestion the reviewer substantially changed is misleading, so the page should say which it is.
Anonymous suggestions: credit the name the submitter typed, if any; otherwise say the suggestion was anonymous. Do not invent a profile link.

### Tier 2 — per-line attribution (a further goal, lower priority)

When a suggestion is approved, remember which lines it introduced, so they can be marked on the page.
Surface the mark on hover or in a gutter: the submitter's avatar and name, and a way to see the original suggestion.
Treat it as best-effort. A later edit touching those lines invalidates the attribution, and lines the reviewer rewrote belong to the reviewer. This is line-level authorship, and it carries the same caveats.

## Why it matters

Suggestion-based contribution is the entry point for exactly the people a wiki most wants to keep: readers who know the subject but have no edit rights. Today their improvement becomes invisible to them the moment it is accepted, and the page credits someone else for their work. Giving the name back is a small change that turns approval into visible recognition, and makes the loop feel like contributing rather than submitting into a void.

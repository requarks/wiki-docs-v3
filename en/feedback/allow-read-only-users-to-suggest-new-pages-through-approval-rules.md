---
title: Allow read-only users to suggest new pages through approval rules
description: >-
  Summary Approval rules let read-only users submit edit suggestions for
  existing pages, which a reviewer group can accept or reject. This works well
  for changes, but there is no equivalent for new pag…
published: true
date: '2026-11-16T13:30:16.273Z'
tags: []
editor: markdown
dateCreated: '2026-11-16T13:30:16.273Z'
---


**Summary**
Approval rules let read-only users submit edit suggestions for existing pages, which a reviewer group can accept or reject. This works well for changes, but there is no equivalent for *new* pages: a suggestion is always tied to an existing page id, so a contributor without `write:pages` cannot propose a page that does not exist yet.

**Use case**
A section of the wiki has a group of contributors who are read-only there, and an editor group that reviews their submissions before they go live. For changes to existing pages the approval flow covers this. For new pages, the only options today are:
- an editor creates an empty placeholder page so the contributor can suggest content into it, or
- granting the contributors `write:pages` on a separate "drafts" path and having editors move pages afterwards.

Both work around the approval flow instead of using it, and the second one gives contributors direct publish rights on part of the tree.

**Proposal**
- Add a "Can suggest new pages" option to approval rules, scoped by the rule's path match (e.g. path starts with `/section-a`).
- A contributor covered by such a rule can open the editor at a new path within that scope and submit it as a *page suggestion* instead of publishing.
- The suggestion appears in the reviewers' inbox like an edit suggestion, showing the proposed path, title, tags and content.
- On accept, the page is created at the proposed path (or a path the reviewer adjusts), with the contributor recorded as author and the reviewer as approver in the history.
- On reject, nothing is created; the contributor gets the reviewer's note.

**Nice to have**
- Let the reviewer change the target path/folder before accepting.
- Expose it as webhook events, same as edit suggestions (`page.suggestion.*`).
- Optionally require new-page suggestions to start from a page template.

---
title: Basics
description: Learn the basics of Wiki.js
published: true
date: '2026-08-27T00:09:09.308Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-13T22:40:50.191Z'
---

*This wiki is incomplete and actively being populated.*

# User Interface

## Header

![Header](/guide/images/basics-ui-header.png)

The site header is present on all pages.

- The left section contains the site logo and title. You can always **return to the homepage** by clicking the logo.
- The middle section is the [search](/guide/search) bar. Enter a term and press <kbd>Enter</kbd> to [search](/guide/search) for that term across the wiki. You can also press <kbd>Ctrl/Cmd</kbd> + <kbd>K</kbd> to quickly focus the search bar and start typing.
- The right section contains links to features of the wiki:
  - Click *:la:plus-circle:*{.text-blue} to create a new page. You'll be prompted to select the [editor](/guide/editors) to use.
  - Click *:la:folder-open:*{.text-positive} to open the [File Manager](/guide/file-manager), which is where you can manage pages and assets.
  - Click *:mdi:inbox-full:*{.text-amber} to go to the [Inbox & Notifications](/guide/inbox) area.
  - Click *:la:tools:*{.text-pink} to access the [Administration Area](/admin/dashboard). This button is only visible if you have access to the admin dashboard.
  - Click :la:user-circle: or round avatar picture to access your [profile](/guide/profile) page or to logout.

> [!NOTE]
> If you're not authenticated, you'll instead see a <kbd>:la:sign-in-alt: Login</kbd> button in the right section.

## Sidebar Navigation

## Page Actions Bar

## Page Header

![Page Header](/guide/images/basics-ui-page-header.png)

The page header is composed of 4 components:

### Breadcrumb Bar

The left section of the top bar shows the hierarchy of the page from the root. You can click on any segment to go up to that parent.

### Last Modified

The right section of the top bar shows the last modification timestamp of the page.

### Title Bar

The left section contains the page title, description and icon.
All these elements become editable when in edit mode.

### Actions

The right section contains actions you can perform on this page, depending on the mode you're in:

#### In View Mode

- Click :la:bell: to watch the page. You'll be notified when it gets updated.
- Click :la:print: to print the page. This button might not be visible if the administrator disabled it. You can always trigger a print from your browser menu or using <kbd>Ctrl/Cmd</kbd> + <kbd>P</kbd> on most systems.
- Click :la:inbox: to view edit suggestions pending review. This button is only visible if [Approvals](/admin/approvals) are enabled and you're a reviewer for the page.
- If you have write permissions to this page, click the orange <kbd>:la:edit: Edit</kbd> button to enter the Edit mode.
- If you only have a read access but an [Approvals](/admin/approvals) rule cover this page, click the orange <kbd>:la:edit: Suggest Edits</kbd> button to enter a basic Edit mode to propose changes to the page. If you already submitted an edit proposal but it hasn't been reviewed yet, click the <kbd>:la:edit: Continue Suggestion</kbd> button to keep editing your suggestion.

#### In Edit Mode

- Click :la:question-circle: to read the documentation for the current editor.
- Click the red <kbd>:la:times: Discard/Close</kbd> button to cancel editing and return to the view mode.
- If in "Suggest Edits" mode, click the green <kbd>:la:paper-plane: Submit Edits</kbd> to submit your edits for review.
- If you're creating a new page, click the green <kbd>:la:check: Create Page</kbd> to save the page.
- If you're editing an existing page, click the green <kbd>:la:check: Save Changes</kbd> to save the page. A second <kbd>:la:check-double:</kbd> button is also available next to it as a shortcut to save and close (return to the view mode).

## Page Sidebar

## Page Contents

# Writing a Page

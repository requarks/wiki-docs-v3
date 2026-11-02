---
title: Basics
description: Learn the basics of Wiki.js
published: true
date: '2026-11-02T02:30:30.545Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-13T22:40:50.191Z'
---

*This wiki is incomplete and actively being populated.*

# User Interface

## Header

![Header](/guide/images/basics-ui-header.png){.decor-shadow .decor-rounded}

The site header is present on all pages.

- The left section contains the site logo and title. You can always **return to the homepage** by clicking the logo.
- The middle section is the [search](/guide/search) bar. Enter a term and press <kbd>Enter</kbd> to [search](/guide/search) for that term across the wiki. You can also press <kbd>Ctrl/Cmd</kbd> + <kbd>K</kbd> to quickly focus the search bar and start typing.
- The right section contains links to features of the wiki:
  - Click *:la:plus-circle:*{.text-blue} to create a new page. You'll be prompted to select the [editor](/guide/editors) to use.
  - Click *:mdi:museum-outline:*{.text-positive} to access the [File Manager](/guide/file-manager) *(to manage pages and assets)*, the [Glossary](/guide/glossary) and [Tags](/guide/tags) view.
  - Click *:mdi:inbox-full:*{.text-amber} to go to the [Inbox & Notifications](/guide/inbox) area.
  - Click *:la:tools:*{.text-pink} to access the [Administration Area](/admin/dashboard). This button is only visible if you have access to the admin dashboard.
  - Click :la:user-circle: or round avatar picture to access your [profile](/guide/profile) page or to logout.

> [!NOTE]
> If you're not authenticated, you'll instead see a <kbd>:la:sign-in-alt: Login</kbd> button in the right section.

## Sidebar Navigation



## Page Header

![Page Header](/guide/images/basics-ui-page-header.png){.decor-shadow .decor-rounded .decor-border}

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

## Page Rail

The rail is an action side bar displayed on the right side of the screen. It's grey in view mode and becomes orange in edit mode.

It contains actions for the current page:

| Button | Action | Description |
| :-: | :-- | :-- |
| :la:pen-nib: | Open [Page Properties](/guide/page-properties) | Open the page properties dialog to modify page metadata. |
| :mdi:image-sync-outline: | Show Pending Uploads | **Only shown in edit mode.** Images that have been pasted or dropped into the editor that are awaiting upload. They get uploaded upon saving the page.
| :la:history: | Show [Page History](/guide/history) | Show the page revisions overlay to browse and view previous versions of the page. |
| :la:code: | Show [Page Source](/guide/source) | Show the page source overlay to see the original code of the page before render. |
| :la:atom: | Convert Page | **Shown under the extra Page Actions menu (:la:ellipsis-h:).** Change the editor of the page (e.g. Visual editor to Markdown editor). Not available for all pages. |
| :la:magic: | Rerender Page | **Shown under the extra Page Actions menu (:la:ellipsis-h:).** Trigger a re-render of the page on the server. This is only needed when the current render failed or is outdated. |
| :la:copy: | [Duplicate Page](/guide/pages#duplicate) | Create a copy of the page and start editing it. |
| :la:share: | [Rename / Move Page](/guide/pages#rename-move) | Rename the page or move it to a different location. |
| :la:trash: | [Delete Page](/guide/pages#delete) | Delete the page and send it to the recycle bin. |

> [!NOTE]
> Some actions may not be available depending on your group permissions.

## Page Sidebar

## Page Contents

![Content Tabs](/guide/images/basics-ui-content-tabs.webp){.decor-shadow .decor-rounded .decor-border}

In the top-right corner of the page contents, there are 3 tabs:

- **Article**: The page contents
- **Talk**: Discussions (comments and annotations)
- **Links**: List of pages that link to this one.

> [!NOTE]
> Some tabs may not be displayed if comments and backlinks are disabled.

# Writing a Page

To write a new page, click the *:la:plus-circle:*{.text-blue} button in the top-right section of the site. You'll be prompted to select the editor to use. Most users will choose either the [Markdown editor](/guide/editors/markdown) *(best for technical documentation)* or the [Visual editor](/guide/editors/visual) *(best for non-technical users)*.

Once you land into the editor, enter a **page title** and **description** at the top. You can optionally select a different **page icon** as well by clicking on it and searching for keywords.

When you're ready to save the page, click the **Create Page** button in the top-right corner of the page. You'll be prompted where to save the page. This works exactly like a file system on your desktop, with files and folders. Create a folder to organize your pages or save it at the root of the site.

> [!TIP]
> You can right-click a folder in the left sidebar and select **New Folder** to create a folder under it.

Click the **Save** button to publish the page. To go back to editing the page, simply click the **Edit** button in the top-right corner.

## Page Metadata

Metadata and settings of a page can be changed via the [Page Properties](/guide/page-properties) dialog. Click the :la:pen-nib: button on the right side of the page (page rail) to access it. It's present in both view and edit mode.

# Comment on a Page

On any page with comments enabled, click on the **Talk** tab to switch to the discussion view.

You can either create a new comment by clicking the **New Comment** button on the right sidebar, or click the **Reply** button under an existing comment.

The text area will be focused for you to write a comment. Click **Post Comment** when you're done to submit the comment.



---
title: Audit Log
description: A log of all events by users across the wiki for auditing purposes
published: true
date: '2026-09-06T07:27:25.933Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-09-06T06:54:57.404Z'
---

# Overview

The audit log records all events initiated by a user.

Click the <kbd>:la:search-plus: Details</kbd> button next to the desired row to view the context metadata *(e.g. which setting was changed, asset filename and path, etc.)*.

> [!NOTE]
> The goal of the audit log is not to store the exact state but to keep a log of which actions a user has taken.
> The following are **NOT** stored in the logs:
> - Page contents, as this is already stored by the page versioning. The page version ID is instead stored in the audit log, which can be referenced.
> - Admin settings values *(e.g. auth and storage configs)*
> - User authentication values *(e.g. passwords, keys, etc.)*

## Filters

Logs can be filtered by:
- Users
- Area
- Action
- Date Range

## Export

Logs can be exported to NDJSON format *(Newline delimited JSON)* by clicking the **Export** button in the top-right corner of the Audit Log page. The currently active filters are respected.

## Retention

By default, all events up to **90 days** are kept. A scheduled job runs once a day to purge older entries.

The retention period can be changed by clicking the **Retention** button in the top-right corner of the Audit Log page. Select a range between **30 days** and **forever**.

> [!IMPORTANT]
> - For security reasons, it's **NOT** possible to set a value lower than **30 days**.
> - Note that keeping logs forever or years can cause the database size to balloon dramatically over time on an active wiki. Be mindful of the logs volume and consider exporting logs for offline safe-keeping instead.

## Action Reference

| Action | Area | Description |
| :-- | :-- | :-- |
| `addIconSet` | `admin` | Added an icon set |
| `approvePageEdit` | `page` | Approved an edit suggestion |
| `assignUserToGroup` | `admin` | Added a user to a group |
| `cancelJob` | `admin` | Cancelled a pending job |
| `changePassword` | `profile` | Changed their own password |
| `checkForUpdate` | `admin` | Checked for an update |
| `createApiKey` | `admin` | Created an API key |
| `createApprovalRule` | `admin` | Created an approval rule |
| `createAuthStrategy` | `admin` | Added an authentication strategy |
| `createFolder` | `page` | Created a folder |
| `createGroup` | `admin` | Created a group |
| `createHook` | `admin` | Created a webhook |
| `createPage` | `page` | Created a page |
| `createSite` | `admin` | Created a site |
| `createUser` | `admin` | Created a user |
| `deleteApprovalRule` | `admin` | Deleted an approval rule |
| `deleteAsset` | `asset` | Deleted a file |
| `deleteAuthStrategy` | `admin` | Deleted an authentication strategy |
| `deleteAvatar` | `profile` | Removed their avatar |
| `deleteBlock` | `admin` | Deleted a custom block |
| `deleteFolder` | `page` | Deleted a folder |
| `deleteGroup` | `admin` | Deleted a group |
| `deleteHook` | `admin` | Deleted a webhook |
| `deleteIconSet` | `admin` | Deleted an icon set |
| `deletePage` | `page` | Deleted a page |
| `deletePasskey` | `profile` | Removed a passkey |
| `deleteSite` | `admin` | Deleted a site |
| `deleteSiteImage` | `admin` | Removed a site image |
| `deleteUser` | `admin` | Deleted a user |
| `disableTfa` | `profile` | Turned 2FA off |
| `disconnectWebsockets` | `admin` | Closed the websocket connections |
| `duplicateFolder` | `page` | Duplicated a folder |
| `enableTfa` | `profile` | Turned 2FA on |
| `exportAuditLog` | `admin` | Exported the audit log |
| `fetchLocales` | `admin` | Fetched the locale list |
| `flushCache` | `admin` | Flushed the caches |
| `flushIconCache` | `admin` | Purged the icon cache |
| `forcedPasswordChange` | `auth` | Changed a password when required to at sign-in |
| `installExtension` | `admin` | Installed an extension |
| `installLocale` | `admin` | Installed a locale |
| `invalidateSessions` | `admin` | Ended every session |
| `login` | `auth` | Signed in |
| `logout` | `auth` | Signed out |
| `materializeIcons` | `admin` | Stored icons for offline use |
| `moveFolder` | `page` | Moved a folder |
| `movePage` | `page` | Moved or renamed a page |
| `purgeApiKeys` | `admin` | Purged the revoked API keys |
| `purgePageHistory` | `admin` | Purged page history |
| `purgeSampleContent` | `admin` | Purged the sample content |
| `rebuildSearchIndex` | `admin` | Rebuilt the search index |
| `refreshIconSets` | `admin` | Refreshed the icon sets |
| `regenerateCertificates` | `admin` | Regenerated the API key certificates |
| `register` | `auth` | Registered an account |
| `registerPasskey` | `profile` | Registered a passkey |
| `rejectPageEdit` | `page` | Declined an edit suggestion |
| `renderPage` | `page` | Queued a page for rendering |
| `requestPasswordReset` | `auth` | Requested a password reset |
| `resetPassword` | `auth` | Reset a password from an emailed link |
| `resetUserPassword` | `admin` | Set a user's password |
| `retryJob` | `admin` | Retried a job |
| `revokeApiKey` | `admin` | Revoked an API key |
| `runScheduledTask` | `admin` | Ran a scheduled task |
| `runStorageAction` | `admin` | Ran a storage action |
| `sendTestEmail` | `admin` | Sent a test email |
| `sendWelcomeEmail` | `admin` | Sent a welcome email |
| `setFolderColor` | `page` | Changed a folder colour |
| `submitPageEdit` | `page` | Suggested an edit |
| `togglePasswordLogin` | `profile` | Turned password sign-in on or off |
| `unassignUserFromGroup` | `admin` | Removed a user from a group |
| `unlockPage` | `page` | Unlocked a password-protected page |
| `unwatchPage` | `page` | Stopped watching a page |
| `updateApiState` | `admin` | Turned the API on or off |
| `updateApprovalRule` | `admin` | Updated an approval rule |
| `updateAsset` | `asset` | Renamed or moved a file |
| `updateAuditConfig` | `admin` | Changed the audit log retention |
| `updateAuthStrategy` | `admin` | Updated an authentication strategy |
| `updateAvatar` | `profile` | Changed their avatar |
| `updateBlock` | `admin` | Changed the blocks of a site |
| `updateEditorSettings` | `profile` | Changed their editor settings |
| `updateFlags` | `admin` | Changed the system flags |
| `updateFolder` | `page` | Renamed a folder |
| `updateGroup` | `admin` | Updated a group |
| `updateHook` | `admin` | Updated a webhook |
| `updateIconSet` | `admin` | Enabled or disabled an icon set |
| `updateLocale` | `admin` | Changed a locale alias |
| `updateMailConfig` | `admin` | Updated the mail configuration |
| `updateMetricsState` | `admin` | Turned the metrics endpoint on or off |
| `updatePage` | `page` | Edited a page |
| `updatePageNavigation` | `admin` | Changed the navigation of a page |
| `updateProfile` | `profile` | Updated their profile |
| `updateSearchConfig` | `admin` | Changed the search configuration |
| `updateSecurity` | `admin` | Changed the security configuration |
| `updateSite` | `admin` | Updated a site |
| `updateSiteImage` | `admin` | Uploaded a site image |
| `updateStorage` | `admin` | Updated the storage configuration |
| `updateUser` | `admin` | Updated a user |
| `updateUserDefaults` | `admin` | Changed the user defaults |
| `uploadAsset` | `asset` | Uploaded a file |
| `verifyEmail` | `auth` | Confirmed an email address |
| `watchPage` | `page` | Started watching a page |
{.table-leading-col}

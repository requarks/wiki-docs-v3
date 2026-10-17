---
title: Profile
description: Manage your user info and settings
published: true
date: '2026-10-17T03:29:28.237Z'
tags:
  - user-guide
editor: markdown
dateCreated: '2026-08-14T07:19:08.906Z'
---

# Profile

## My Info

> [!NOTE]
> Some fields may not be editable depending on the configuration set by your wiki administrator.

| Field | Description | Notes |
| :-- | :-- | :-- |
| Display Name | Your full name; shown when authoring content *(e.g. pages, comments, etc.)*. |  |
| Email Address | The email address used for login. | Read-only. *Cannot be edited.* |
| Handle | The unique @name people mention you by in comments. 3 to 32 letters, digits, hyphens or underscores. Leave it empty to not be mentionable. |  |
| Location | Your city and country; shown on your profile page. |  |
| Job Title | Your position in your organization; shown on your profile page. |  |
| Pronouns | Let people know which pronouns should they use when referring to you. |  |
{.table-leading-col}

## Preferences

| Field | Description | Options / Default |
| :-- | :-- | :-- |
| Timezone | Set your timezone to display local time correctly. | *The default value is set by your administrator.* |
| Date Format | Set your preferred format to display dates. | *The default value is set by your administrator.* |
| Time Format | Set your preferred format to display time. | *The default value is set by your administrator.* |
| Site Appearance | Use the light or dark theme. | **Site Default** *(default)*, Light or Dark |
{.table-leading-col}

## Accessibility

| Field | Description | Options / Default |
| :-- | :-- | :-- |
| Color Vision Deficiency | Alter the color scheme of certain UI elements to account for certain color vision dificiencies. | **None** *(default)*, Protanopia, Deuteranopia or Tritanopia |
| Reduce Motion | Turn off most animations and smooth scrolling. Always on if your operating system asks for reduced motion. | **Follow System** *(default)* or On |
| Underline Links | Always underline links in page content, so they can be told apart without relying on color. | **Off** *(default)* or On |
| Content Text Size | Enlarge the text of page content. The rest of the interface keeps its size. | **Default** *(default)*, Large or Larger |
{.table-leading-col}

# Avatar

Change your profile picture by uploading a JPG, PNG or WebP file, ideally in a square ratio. The image will be cropped to fit a square ratio.

# Authentication

## Local Authentication

Click the <kbd>:la:cog:</kbd> button to access the following options:

- **Change Password**: Change your current password to a new one.
- **Set 2FA**: Add a Two-Factor Authentication (2FA) step to protect your account. You need a mobile authenticator app or a password manager that supports TOTP codes.
- **Turn Off Password Login**: Disable the password-based authentication to instead use other more secure methods. This requires at least one other authentication method or a passkey to be created first.

## Passkeys

Passkeys are a replacement for passwords for a faster, easier and more secure login. It relies on your device existing biometrics *(phone, computer, security key)* to validate your identity.
*This option may not be available if disabled by your wiki administrator.*

> [!TIP]
> Passkeys are the most secure authentication method and can be used as an alternative to other methods.

# Groups

See the groups you are assigned to. Note that only an administrator can change your group assigment(s).

# Notifications

Select which notifications to receive and whether to receive them via in-app and/or email.

# Personal Access Tokens

Personal access tokens (PAT) let scripts, automations and other integrations to act on your behalf. A token can only do what you can do, and only in the areas you grant it. Treat it like a password.

Click the **New Token** button in the top-right to create a token. Enter a name, an expiration and select the scopes to grant.

> [!WARNING]
> Make sure to save the token in a safe place. It will not be shown again!

To revoke a token, click the <kbd>:la:trash-alt:</kbd> button.

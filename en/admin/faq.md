---
title: Troubleshooting / FAQs
description: Solutions to common issues / Frequently Asked Questions
published: true
date: '2026-08-24T08:54:33.179Z'
tags: []
editor: markdown
dateCreated: '2026-08-19T03:23:08.396Z'
---

# General

## Cannot upload files larger than X

**Cause:** You are most likely using a reverse proxy such as nginx or apache.
**Resolution:** Increase your reverse proxy configuration for file uploads.

## Why are sub-folder installations not supported?

**tl;dr:** Because it's not worth the significant downsides.

**Long answer:** It introduces many problems:

- **Path parsing:** Assuming an installation at `/wiki`. If a user enters a link to `/foobar`, does it mean `/foobar` or `/wiki/foobar`? When creating a page, do you enter the subfolder in the path or not? What if the user does? Should it strips the subfolder? What if the user does want to put the page in a folder wiki under `/wiki`? When adding an image to a page, should it rewrite the path with the prefix? Having assets in a subfolder at the root is a very common case. One user would expect one behavior while another would expect the opposite. This becomes extremely confusing for both the developer and the end users.

- **Export/import:** When exporting the page to a Git repository, should all the links be rewritten without the prefix? How about importing? Should it assume all links need to be prefixed? What if I want to link to another folder at the domain root?

- **Security**: There's no isolation between the wiki and other services/apps running on the same host. Any script on the host can open pages in iframes and execute arbitrary code with the user session. Cookies can be read by any app on the domain.

- **Service workers**: Any app on the same domain using service workers is now intercepting requests/responses meant for Wiki.js. In addition to the lack of security, you're also now dealing with potential stale assets because the service worker is in control of everything on the domain.

- **Storage collision:** By hosting multiple sites on the same hostname, you're sharing the cookies and localStorage for that domain. If another site decides to change / delete the cookie used by Wiki.js, you'll run into issues. The cookie header is also limited in length (4096 characters) and can also lead to issues if too many apps set cookies (especially with JWT).

- **Passkeys/WebAuthn:** Passkeys are registered on the domain, not per path. The same is true for password autofill in most cases.

- **Sitemap/Robots/Favicons:** These special files can only live at the root, which means these features would be completely broken and non-functional.

- **Support:** This is by far the biggest pain point. v1 had support for subfolder installations. The vast majority of support tickets were about reverse-proxy not setup correctly. Good docs alone cannot prevent this as there a million different reverse-proxy solutions and you'd be surprised how many users can't be bothered with reading docs in the first place. This puts a massive strain on developer support.

For these reasons, there's no plan to support subfolder installations for the foreseeable future.
Use a subdomain. If you absolutely can't, then sorry, use something else.

# Authentication

## Reset admin password manually

The only way to change a password, without access to the administration web UI, is via the database. Use a tool like [pgAdmin](https://www.pgadmin.org/) if you're not comfortable with shell commands.

> [!WARNING]
> **It's NOT possible to read the current password value.** Passwords are stored using a one-way bcrypt hashing process, which is not reversible. You can only overwrite it with a new value.

The code below replaces the config for the **Local Authentication** strategy *(which has a static ID of `5a528c4c-0a82-4ad2-96a5-2b23811e6588`)* for the `admin@example.com` user *(replace with your email address in the code below)*.

The new config sets a new temporary password of `recovery123` and enables the "Must Change Password" flag to force a new password on the next login.

> [!TIP]
> You can also generate a different password hash using a [bcrypt hash generator](https://bcrypt-generator.com/) set to `12` rounds and set the `mustChangePwd` flag to `false`. However, it's recommended to use the predefined hash below instead to avoid logging your actual password hash into the shell history.

### SQL Query

Using [pgAdmin](https://www.pgadmin.org/) or **psql**, execute the following query against your wiki database:

```sql
UPDATE wiki.users
SET auth = jsonb_set(
  auth,
  '{5a528c4c-0a82-4ad2-96a5-2b23811e6588}',
  '{
    "password": "$2a$12$VzIQGsgG4wjUNSNBPRwif.bDsMwsyy1R3Sox9yfVL1V3fYTya3sMq",
    "tfaSecret": "",
    "tfaIsActive": false,
    "tfaRequired": false,
    "mustChangePwd": true,
    "restrictLogin": false
  }'::jsonb,
  true
)
WHERE email = 'admin@example.com';
```

### Using docker

Assuming your database container is named `db` with a `wiki` user and database name:

```sh
docker exec -i db psql -U wiki -d wiki <<'EOF'
UPDATE wiki.users
SET auth = jsonb_set(
  auth,
  '{5a528c4c-0a82-4ad2-96a5-2b23811e6588}',
  '{
    "password": "$2a$12$VzIQGsgG4wjUNSNBPRwif.bDsMwsyy1R3Sox9yfVL1V3fYTya3sMq",
    "tfaSecret": "",
    "tfaIsActive": false,
    "tfaRequired": false,
    "mustChangePwd": true,
    "restrictLogin": false
  }'::jsonb,
  true
)
WHERE email = 'admin@example.com';
EOF
```

# Development

## Are devcontainers required for development?

No but it's highly recommended as it includes all the necessary dependencies. Many IDEs now support devcontainers so you're no longer limited to VS Code.

## Was AI used to generate code during development?

Yes. Claude by Anthropic was used as a coding assistant. However, it was always used in a very directed manner for specific features. Every button, form element, API endpoint, DB schema fields, UX behavior, etc. is intentional and reasoned.

Nothing was "vibe-coded" or done using AI agents left on their own with instructions to follow a plan. This is a recipe for disaster and a great way to end up with insecure, buggy and unmaintainable software.

All documentation is written by a human.

## Are Pull Requests with AI generated code accepted?

Yes **BUT** a human must have reviewed the entirety of the proposed code and is fully responsible for it.

- AI brings a significant additional load to project maintainers as each PR must be reviewed by human before merging. The effort needed to create a PR versus the effort needed to review it becomes completely out of balance and isn't sustainable. If you can't be bothered to review your PR and be able to explain it in details, then it's not worth for the maintainers to review it and waste time on it.
- Because any feature development is now within reach of all users, it's trivial for anyone to submit a niche feature that isn't useful for most users. It's then up to the maintainers to keep this feature up to date and working. Just because your PR is fully working and well constructed, doesn't automatically make it sensible to be included in the project.
- PRs that are clearly submitted via automated AI bots / agents will be rejected. Simply adding a "Signed-off by: XYZ" at the end and calling it a day doesn't make it right. Take the time to review the code + write the PR description and the project maintainers will take the time to review it.

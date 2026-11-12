---
title: CLI
description: Command-line maintenance and recovery tool
published: true
date: '2026-11-12T10:48:49.199Z'
tags:
  - admin
editor: markdown
dateCreated: '2026-11-12T09:16:55.566Z'
---

> [!IMPORTANT]
> Coming soon in 3.4.0

# Overview

Wiki.js ships with a command-line tool for maintenance and recovery. This is useful if you get locked out of the administration web UI *(lost admin password, incorrectly changed site hostname, etc.)*.

The tool works directly against the wiki's database. It reads the configuration exactly as the server does, so wherever the server runs, the tool can run beside it with no extra setup.

> [!WARNING]
> **Anyone who can run this tool can take over any account on the wiki.**
> Read [Security considerations](#security-considerations) before you give someone access to the server.

# Running the CLI

The CLI is the file `backend/cli.ts` in the Wiki.js installation directory. Run it with a command name and that command's options:

```sh
backend/cli.ts <command> [options]
```

When run with no command, or with `--help`, it lists every available command. Run `<command> --help` to see that command's options.

## With Docker

Run it inside the running Wiki.js container:

```sh
docker exec -it wiki backend/cli.ts reset-password
```

Replace `wiki` with your container's name. The `-it` flags give the CLI a terminal to ask you questions on. Without them, pass every value as an option (see [Using it from scripts](#using-it-from-scripts)).

## With Kubernetes (Helm chart)

Run it inside one of the wiki pods:

```sh
kubectl exec -it deployment/wiki -- backend/cli.ts reset-password
```

With several replicas, it does not matter which pod you pick: they share one database, and the CLI tells all of them about any change they need to know about.

> [!NOTE]
> Run the CLI interactively rather than as a Kubernetes Job. The `reset-password` command prints the new password, and a Job's output is kept in the pod logs.

## Manually on Host

From the Wiki.js installation directory:

```sh
backend/cli.ts reset-password
```

That form works on Linux and macOS. On Windows, or if your system's `env` does not support `-S`, call Node.js directly:

```sh
node --no-experimental-webstorage backend/cli.ts reset-password
```

> [!IMPORTANT]
> - Run it as the **same OS user that runs Wiki.js**, so that it can read the same configuration file.
> - **The CLI must be the same version as the server it is used with.** The tool never upgrades the database itself; only the server does that, when it starts. If the database has been upgraded by a newer version, or not yet upgraded to this one, the tool refuses to run and says which.

# Commands

| Command | What it does |
| --- | --- |
| [`reset-password`](#reset-password) | Give an account a new random password, removing 2FA and passkeys |
| [`set-hostname`](#set-hostname) | Change the hostname a site answers to |
| [`list-admins`](#list-admins) | List the accounts that are administrators |
| [`grant-admin`](#grant-admin) | Make an account an administrator |
| [`enable-user`](#enable-user) | Re-enable a disabled account and turn its password sign-in back on |
| [`reset-security`](#reset-security) | Turn off the Content Security Policy and reset CORS |
| [`flush-caches`](#flush-caches) | Tell every running instance to drop its caches |
| [`info`](#info) | Show versions, database, instances, sites and scheduler health |

Every command that changes something shows what it is about to do, and asks before doing it.

## `reset-password`

Gives an account a new, randomly generated password *(will be displayed on screen once)*, and ensures that account is able to login. Use it when an administrator has lost their password or their two-factor device.

```sh
backend/cli.ts reset-password --email admin@example.com
```

| Option | Description |
| --- | --- |
| `-e`, `--email <address>` | Email address of the account. If you leave it out, the tool lists the administrators and asks. |
| `--keep-tokens` | Keep the account's personal access tokens instead of asking whether to revoke them. |

What it does to the account:

- **Replaces the password** with a random one, which must be changed at the next sign-in. This also works for an account that has only ever signed in through an external provider: it gets a password for the first time.
- **Turns password sign-in back on**, if it had been turned off for the account.
- **Turns off two-factor authentication.** If the account's group, or the wiki's authentication settings, require two-factor authentication, the user is asked to set it up again when they sign
  in.
- **Removes every passkey** registered to the account.
- **Signs the account out** everywhere.
- **Revokes its personal access tokens**, if enabled. The tool asks, and the default is yes. Any script or integration using one of them will need a new token.
- **Emails the account holder** to say the password was reset, if mail is configured. This can't be turned off; see [Security considerations](#security-considerations).

The tool warns you before turning off two-factor authentication or removing passkeys. It also warns if the account is disabled, since a new password won't let anyone in until the account is enabled again (see [`enable-user`](#enable-user)).

The new password is shown once, at the end:

```plaintext title="Example Output"
✔ Password reset for admin@example.com. Every session it held has been ended.
✔ Two-factor authentication turned off.
✔ 2 passkey(s) removed.
✔ 1 personal access token(s) revoked.
✔ Emailed admin@example.com to say the password was reset.

  New password:   jBWHX-wqhwY-Ktmyi-gmVuB

  Shown once and stored nowhere else. It must be changed at the next sign-in.
```

The dashes are part of the password. It leaves out characters that are easy to confuse (`0` and `O`, `1`, `l` and `I`), so it can be read off a screen and typed in by hand.

The tool never takes a password as an option, so a password never ends up in your shell history.

## `set-hostname`

Changes the hostname a site is served on. Use it when a site has moved to a new domain, or when it was set to a hostname nobody can reach.

```sh
backend/cli.ts set-hostname
backend/cli.ts set-hostname --site wiki.old-domain.org --hostname wiki.example.org
```

| Option | Description |
| --- | --- |
| `-s`, `--site <id|hostname>` | The site to change, by its ID or its current hostname. If you leave it out, the tool lists the sites and asks. |
| `-n`, `--hostname <hostname>` | The new hostname. If you leave it out, the tool asks. |

The hostname is either:

- a bare hostname such as `wiki.example.org`, with letters, digits, dots and hyphens only (no `https://`, port or path), or
- `*`, so the site answers every hostname that no other site claims.

> [!NOTE]
> Two sites can't share a hostname, and only one site can be `*`.

Running instances use the new hostname straight away, with no restart.

Before you confirm, the tool warns you about what the change can break:

- **Passkeys** are tied to the hostname they were registered on, unless a shared passkey domain is
  set under **Admin :la:arrow-right: Authentication**. Passkeys registered on the old hostname stop working on the new one.
  Their owners can still sign in with their password and register a new passkey.
- **Sign-in providers** (OIDC, SAML, OAuth) that send users back to the wiki need the new hostname
  added to their allowed callback URLs, at the provider.
- **Links in emails** keep pointing at the old address if the base URL under **Admin :la:arrow-right: Mail**
  still names it.

## `list-admins`

Lists every account that holds the `manage:system` permission.

```sh
backend/cli.ts list-admins
```

```plaintext title="Example Output"
Administrators (manage:system)
  Email              Name           Status  Last login            Groups
  admin@example.com  Administrator  active  2026-11-09 08:55 UTC  Administrators
```

The status shows whether each account is active, disabled, or not yet verified. If the list is empty, nobody can administer the wiki: use [`grant-admin`](#grant-admin) to fix that.

This command takes no options of its own and changes nothing.

## `grant-admin`

Makes an account an administrator by adding it to a group that holds `manage:system`. Use it when no working administrator account is left (e.g. the last one was removed from its group, deleted, or only ever signed in through a provider that is now unavailable).

```sh
backend/cli.ts grant-admin --email jane@example.com
```

| Option | Description |
| --- | --- |
| `-e`, `--email <address>` | Email address of the account. If you leave it out, the tool asks. |
| `-g`, `--group <id|name>` | The group to add it to, when more than one group holds `manage:system`. If you leave it out, the tool lists them and asks. |

- If the account is already an administrator, the tool says so and changes nothing.
- If exactly one group holds `manage:system`, the account is added to it.
- **If no group holds `manage:system` any more**, the tool offers to create one. The new group is called **Administrators**. If a group with that name already exists (but without the   permission), the new one is called **Administrators (recovered)** instead, and the existing group is left alone.

The account is signed out everywhere, and holds its new permissions from its next sign-in. If the account is disabled, the tool reminds you to run [`enable-user`](#enable-user) as well.

## `enable-user`

Makes a disabled account usable again.

```sh
backend/cli.ts enable-user --email jane@example.com
```

| Option | Description |
| --- | --- |
| `-e`, `--email <address>` | Email address of the account. If you leave it out, the tool asks. |

It does whichever of these the account needs:

- enables the account,
- marks its email address as verified,
- turns password sign-in back on, if it had been turned off for the account.

It doesn't change the password. If the account has no password, or nobody knows it, follow up with [`reset-password`](#reset-password). If the account needs none of these, the tool says so and changes nothing.

## `reset-security`

Turns off the Content Security Policy (CSP) and sets cross-origin resource sharing (CORS) back to its default. Use it when a CSP set under **Admin :la:arrow-right: Security** is stopping the wiki's interface from loading, so it can't be undone from the admin area.

```sh
backend/cli.ts reset-security
```

This command takes no options of its own.

- **CSP enforcement is turned off.** The directives you wrote are kept, so you can correct them and turn enforcement back on from the admin area.
- **CORS is set back to its default** (off).
- **HSTS is left alone.** Browsers that have seen an HSTS header remember it for its full duration, regardless of what the server sends afterwards, so turning it off would not help.

> [!IMPORTANT]
> **Restart every Wiki.js instance afterwards.** The server reads these settings when it starts, so the change takes effect only after a restart.

If neither setting needs resetting, the tool says so and changes nothing.

## `flush-caches`

Tells every running Wiki.js instance to drop its caches and reload them from the database. This is the same as **Administration Area :la:arrow-right: Utilities :la:arrow-right: Flush Cache**, for when the admin area can't be reached.

```sh
backend/cli.ts flush-caches
```

This command takes no options of its own. If no instance is connected to the database, the tool says so and does nothing.

## `info`

Shows an overview of the installation. It changes nothing, so it is safe to run at any time, and it is the first thing to include when asking for help.

```sh
backend/cli.ts info
```

```plaintext title="Example Output"
Installation
  Wiki.js            3.0.0
  Node.js            v26.10.0
  Config file        /wiki/config.yml
  Database           wiki on db:5432 (schema wiki)
  PostgreSQL         18.4.0
  Migrations         38 applied, up to date (20261109094533_group-rule-paths)

Running instances
  Instance    Address     Connected since
  54eea4c2c9  172.19.0.3  2026-11-12 08:01 UTC

Sites
  Hostname  Title         Status   ID
  *         Default Site  enabled  0bf40e0b-fd54-4999-b8c0-7979287d26ab

Accounts
  Accounts           9 (9 active)
  Administrators     1 (1 active) — see list-admins
  Mail               configured

Scheduler
  Scheduled checks   running
  Active jobs        0
  Queued jobs        60
  Failed (24h)       0
```

| Section | What it tells you |
| :-- | :-- |
| Installation | The versions in use, which configuration file was read, which database the tool connected to, and whether that database's version matches the tool's. |
| Running instances | Every Wiki.js server currently connected to the same database. |
| Sites | Every site, its hostname and whether it is enabled. |
| Accounts | How many accounts and administrators there are, and whether mail is configured. |
| Scheduler | Whether background jobs are being scheduled, and how many are running, waiting or recently failed. |
{.table-leading-col}

> [!NOTE]
> Unlike every other command, `info` still runs when the database is a different version from the CLI. In that case it shows the installation section, with the version problem under **Migrations**, and stops there.

# Common options

Every command accepts these:

| Option | Description |
| --- | --- |
| `-y`, `--yes` | Confirm without asking, and take the default answer to every question. |
| `-v`, `--verbose` | Also show the server's own log lines while the command runs. Useful when something goes wrong. |
| `-h`, `--help` | Show help for the tool, or for one command. |

# Using it from scripts

Every command can run without a terminal, for automation or a `docker exec` without `-it`:

- Pass every value the command would otherwise ask for as an option, such as `--email` or `--hostname`. If one is missing, the command stops and names the option to add.
- Pass `--yes` to confirm. Without it, a command that changes something stops before changing anything.
- With `--yes`, every question that has a default takes it. For example, `reset-password` revokes personal access tokens unless you also pass `--keep-tokens`.

```sh title="Example Command"
docker exec wiki backend/cli.ts set-hostname --site '*' --hostname wiki.example.org --yes
```

## Exit codes

| Code | Meaning |
| --- | --- |
| `0` | Success, including "nothing needed changing" and help you asked for with `--help`. |
| `1` | The command failed or was cancelled; nothing after the point of failure was changed. |
| `2` | The command was used incorrectly: an unknown command or option, a missing value with no terminal to ask for it, `--yes` missing with no terminal, or no command at all. |

# Audit Log

Every change the tool makes is recorded in the audit log (**Admin :la:arrow-right: Audit Log**), like a change made in the admin area. Because nobody is signed in on a command line, the entry names the operating-system user and the machine the tool ran on, such as `Command line (node@wiki-7c9f5d-x2k4p)`, and is marked as coming from the command line.

`info`, `list-admins` and the help screens change nothing and record nothing.

# Security considerations

**The tool gives full control of the wiki to anyone who can run it.** It deliberately skips the wiki's permission checks, which is how it can recover a wiki where nobody holds administrator rights any more. It doesn't add any new way in, though. To run it, you already need access to the server or container and its configuration file, and that file holds the database password. With that, anyone could change the database directly. In other words:

- **Protect shell access to the server or container** as you would protect the database credentials. That access is what controls who can use the tool.
- **The tool can only be run from a shell.** Nothing in the wiki's web interface or API can start it.

Some of its behaviour is there to limit the damage if the wrong person does get that access:

- **`reset-password` always emails the account holder** when mail is configured. You can't turn this off: it is how the owner of an account learns about a reset they didn't ask for. Configuring mail is worth doing for this reason alone.
- **Every change is in the audit log**, with the user and machine it came from.
- **A reset password must be changed at the next sign-in**, so a password seen by whoever ran the tool doesn't stay valid.
- **Passwords are never passed as options**, so they never end up in shell history or in the process list.

The new password does appear in your terminal. Clear your scrollback once you've passed it on, and don't run `reset-password` anywhere its output is saved, such as a CI job or a Kubernetes Job. Once the password is changed during the next login, the displayed password is no longer valid regardless.

# Troubleshooting

**"There is no Wiki.js installation in schema … : start Wiki.js once to create it."**
The tool connected to a database that Wiki.js has never been started against. Check the database line in the message: the tool may be reading the wrong configuration file. Set `CONFIG_FILE` if yours isn't `config.yml`.

**"The database is N migration(s) behind this copy of Wiki.js."**
You've upgraded Wiki.js, but the upgraded server hasn't started yet. Start it once (it upgrades the database as it starts), then run the tool again.

**"The database has N migration(s) this copy of Wiki.js does not know about."**
The database belongs to a newer version of Wiki.js than this copy of the tool. Run the tool that came with the version the server is running.

**"Missing --email, and there is no terminal to ask for it on."**
The tool has no terminal to ask you on, usually because `docker exec` or `kubectl exec` was run without `-it`. Add the flags, or pass the value as the option named in the message.

**"Nothing was changed: pass --yes to confirm without a terminal."**
Same cause: add `-it` to run it interactively, or pass `--yes`.

**"Could not email … "**
The reset went through, but the notice to the account holder couldn't be sent. The message gives the mail server's reason. Check the settings under **Administration Area :la:arrow-right: Mail**.

**A change didn't reach the running wiki.**
Run `info` and look at **Running instances**. If your server isn't listed, the tool and the server are using different databases: compare the **Database** line with the server's configuration. Remember that `reset-security` only takes effect after a restart.

**For anything else**, run the command again with `--verbose` to see the server's own log lines, and include the output of `info` when asking for help.


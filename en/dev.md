---
title: Dev - Getting Started
description: Guide to setup a development environment for Wiki.js
published: true
date: '2026-08-30T04:57:21.100Z'
tags:
  - dev
editor: markdown
dateCreated: '2026-08-30T04:54:23.401Z'
---

# Overview

It's very easy to run a development instance of Wiki.js with all the necessary dependencies and tools included.

# Requirements

:::block-tabs
::block-tab{label="Linux" header="2"}
- An IDE that supports [Dev Containers](https://containers.dev/), for example:
  - [Visual Studio Code](https://code.visualstudio.com/) *(recommended)*
    - You must also install the **Dev Containers** extension.
  - [IntelliJ WebStorm](https://www.jetbrains.com/webstorm/)
  - [Zed](https://zed.dev/)
- [Docker Engine with Docker Compose](https://docs.docker.com/engine/install/)

> [!NOTE]
> Avoid Docker Desktop on Linux as it's known to cause issues. Install the Docker Engine directly instead.
::

::block-tab{label="macOS" header="2"}
- An IDE that supports [Dev Containers](https://containers.dev/), for example:
  - [Visual Studio Code](https://code.visualstudio.com/) *(recommended)*
    - You must also install the **Dev Containers** extension.
  - [IntelliJ WebStorm](https://www.jetbrains.com/webstorm/)
  - [Zed](https://zed.dev/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
::

::block-tab{label="Windows" header="2"}
- An IDE that supports [Dev Containers](https://containers.dev/), for example:
  - [Visual Studio Code](https://code.visualstudio.com/) *(recommended)*
    - You must also install the **Dev Containers** and **WSL** extensions.
  - [IntelliJ WebStorm](https://www.jetbrains.com/webstorm/)
  - [Zed](https://zed.dev/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [WSL 2](https://learn.microsoft.com/en-us/windows/wsl/install) + [WSL Integration](https://docs.docker.com/desktop/wsl/) enabled in Docker Desktop
::
:::

# Basic Usage

> [!WARNING]
> All instructions below are written with **Visual Studio Code** in mind. The steps will defer for other editors.

1. Clone the project on your local machine.
1. Open the project in Visual Studio Code.
1. Reopen the project in container (from the popup in the lower-right corner of the screen when opening the project, or via the Command Palette (<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> *or* <kbd>F1</kbd>) afterwards).
1. Once in container mode, make a copy of `config.sample.yml` and rename it to `config.yml`. There's no need to edit the file, the default values are ok.
1. Two terminals should automatically launch in the lower part of the screen. If this isn't the case, from the Command Palette, run the task "Create terminals":
    1. Launch the Command Palette (<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> *or* <kbd>F1</kbd>)
    1. Type `Run Task` and press <kbd>Enter</kbd>
    1. Select the task "Create terminals" and press Enter
1. In the right-side terminal (Frontend), run the command:
    ```sh
    npm run build
    ```
1. In the left-side terminal (Backend), run the command:
    ```sh
    npm run start
    ```
1. Open your browser to `http://localhost:3000`
1. Login using the default administrator user:
    - Email: `admin@example.com`
    - Password: `12345678`

## Populate Sample Content

A tool to quickly generate sample content is available in the **Administration Area** > **Utilities** page.

- Click <kbd>Proceed</kbd> next to the **Generate Sample Content** action.
- To delete all sample content, click <kbd>Proceed</kbd> next to the **Purge Sample Content** action instead.

# Backend Development

> [!TIP]
> If you're still running the `npm run start` command, stop it first.

From the left-side terminal (Backend), run the command:

```sh
npm run dev
```

This will launch the server in dev mode and automatically restart upon modification of any server files.

Only precompiled client assets are served in this mode. See the sections below on how to modify the frontend and run in SPA (Single Page Application) mode.

# Frontend Development

> [!IMPORTANT]
> Make sure you are running `npm run dev` in the left-side terminal (Backend) first! Requests still need to be forwarded to the server, even in SPA mode!

If you wish to modify any frontend content (under `/frontend`), you need to start the Vite Dev Server in the right-side terminal (Frontend):

```sh
npm run dev
```

You can then access the site at `http://localhost:3001`. Notice the port being `3001` rather than `3000`. The app runs in a SPA (single-page application) mode and automatically hot-reload any modified component. Any requests made to the `/_api` endpoint are automatically forwarded to the server running on port `3000`, which is why both must be running at the same time.

Any change you make to the frontend will not be reflected on port `3000` until you run the command `npm run build` in the right-side terminal.

# Included Tools

## pgAdmin

A web version of pgAdmin (a PostgreSQL administration tool) is available at `http://localhost:8000`. Use the login `dev@js.wiki` / `123123` to login.

Add a new server with the following settings:

- Hostname: `db`
- Port: `5432`
- Username: `postgres`
- Password: `postgres`
- Database: `postgres`

## Mailpit

An instance of mailpit (an email testing tool) is available at `http://localhost:8025`.

In your Wiki.js dev instance, on the **Administration Area** > **Mail** page, enter the following settings to point to it:

- Host: `localhost`
- Port: `1025`
- TLS: `off`
- Username: `<none>`
- Password: `<none>`


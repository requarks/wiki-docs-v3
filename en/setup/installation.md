---
title: Installation
description: How to install Wiki.js
published: true
date: '2026-08-27T06:08:15.486Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-08-10T07:53:50.826Z'
---

> [!IMPORTANT]
> Before going any further, make sure you meet all the [requirements](/setup/requirements).

- [Install using Containers](#install-using-containers) *(Docker/Kubernetes)*{.text-sm} - **recommended**
- [Install on Host](#install-on-host) *(Linux/macOS/Windows)*{.text-sm}
- [Install using Cloud Images](#install-using-cloud-images) *(DigitalOcean)*{.text-sm}

# Install using Containers

:::block-tabs
::block-tab{label="Docker" header="2"}

### Tags

Images are tagged to **major**, **major.minor** and **major.minor.patch** versions.
It's recommended to use the **major** version, unless you have a specific requirement to pin your deployment to specific version.

> [!WARNING]
> Note that Wiki.js 3.x is in alpha and images are currently tagged as `3.0.0-alpha`. The tags below won't work until the beta phase has started.

```sh
# -----------------------------
# ALPHA VERSION
# -----------------------------
ghcr.io/requarks/wiki:3.0.0-alpha

# -----------------------------
# NOT YET WORKING (read above)
# -----------------------------
#ghcr.io/requarks/wiki:3

# or using a specific version:
#ghcr.io/requarks/wiki:3.0
#ghcr.io/requarks/wiki:3.0.1
```

> [!CAUTION]
> **DO NOT** use the `latest` tag as it may break your installation when a new major version with breaking changes is released!

All images are built for these architectures:
- **linux/amd64** *(Intel / AMD CPUs)*
- **linux/arm64** *(Apple silicon, Gravitron, Raspberry Pi, etc.)*

### Environment Variables

✅ = Required, ✴️ = Recommended

| Env | Description | Required | Default Value |
| :-- | :-- | :-: | :-- |
| `ADMIN_EMAIL` | Email address to use to create the root administrator account.<br>*Has no effect if the root administrator account is already created.* | ✴️ | `admin@example.com ` |
| `ADMIN_PASS` | Initial password to use to create the root administrator account.<br>*Has no effect if the root administrator account is already created.* | ✴️ | `12345678` |
| `CONFIG_FILE` | Path to the config file |  | `./config.yml` |
| `DATABASE_URL` | Database Connection String *(overrides all `DB_` prefixed env vars if set)* |  |  |
| `DB_HOST` | Database Hostname / IP Address | ✅ |  |
| `DB_NAME` | Database Name | ✅ |  |
| `DB_USER` | Database Username | ✅ |  |
| `DB_PASS` | Database Password | ✅ |  |
| `DB_PASS_FILE` | Path to the mapped file containing the database password. *(overrides `DB_PASS` if set)* |  |  |
| `DB_PORT` | Database Port |  | `5432` |
| `DB_SCHEMA` | Database Schema |  | `wiki` |
| `DB_SSL` | Whether to use SSL to connect to the database.<br>Accepted values: `0, 1, true, false` |  | `false` |
| `DB_SSL_CA` | Database CA certificate content, as a single line string *(without spaces or new lines)*, without the prefix and suffix lines. |  |  |
| `LOG_FORMAT` | Logging format<br>Accepted values: `default, json` |  | `default` |
| `LOG_LEVEL` | Severity level for logging<br>Accepted values: `debug, info, warn, error` | | `info` |
| `PORT` | HTTP Port to listen on | | `3000` |

### Example

Assuming you have a PostgreSQL container named `db` on the same network *(replace the values with your own!)*:

```sh
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "ADMIN_EMAIL=user@example.com" -e "ADMIN_PASS=SuperSecret123" -e "DB_HOST=db" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:3.0.0-alpha
```

Once the container is started, browse to `http://YOUR-IP-ADDRESS:8080` and login using the admin email and password you provided in the command above.

### Docker Compose

Here's a full example of a Docker Compose file for Wiki.js listening on port 80: *(replace the values of `ADMIN_EMAIL` and `ADMIN_PASS` with your own)*:

```yaml title="compose.yaml" linesHighlight="18,19"
services:

  db:
    image: postgres:18
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql

  wiki:
    image: ghcr.io/requarks/wiki:3.0.0-alpha
    depends_on:
      - db
    environment:
      ADMIN_EMAIL: user@example.com
      ADMIN_PASS: SuperSecret123
      DB_HOST: db
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"

volumes:
  db-data:
```

`DB_HOST` should match the service name *(in this case, `db`)*. If container_name is specified for the service, its value should be used instead.

See the [reference above](#environment-variables) for all available environment variables.

Once both containers are started, browse to `http://YOUR-IP-ADDRESS` and login using the admin email and password you provided above.

### User Mode

By default, the Wiki.js docker image runs as the user `wiki`. Some deployments require the container to run as root. Simply add the `-u root` parameter when creating the container to do so.

This is however **NOT** a secure way to run containers. **Make sure you understand the security implications before doing so.**
::

::block-tab{label="Kubernetes" header="2"}
*Coming soon | Not available during beta phase*
::

::block-tab{label="Guided Ubuntu Install" header="2"}
This guide provides an easy, no docker knowledge required, step-by-step instructions to install Wiki.js on a fresh Ubuntu server using containers.

#### Requirements

- Ubuntu 26.04 or 24.04
- Local Terminal or Remote SSH Access

#### Install dependencies

1. Update the machine
    ```sh
    sudo apt -qqy update
    sudo apt -qqy upgrade
    ```
2. Install Docker
    ```sh
    # Add Docker's official GPG key:
    sudo apt install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add the repository to Apt sources:
    sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
    Types: deb
    URIs: https://download.docker.com/linux/ubuntu
    Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
    Components: stable
    Architectures: $(dpkg --print-architecture)
    Signed-By: /etc/apt/keyrings/docker.asc
    EOF

    sudo apt update
    sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```
3. Setup firewall
    ```sh
    sudo ufw allow ssh
    sudo ufw allow http
    sudo ufw allow https

    sudo ufw --force enable
    ```

#### Setup containers
1. Create a new folder in the location of your choice (e.g. `~/wiki`, replace in the commands below if different).
2. Generate a random DB secret:
    ```sh
    cd ~/wiki
    openssl rand -base64 32 > .db-secret
    ```
3. Create a new file named `compose.yaml` *(under the same folder)* with the following contents:
    > [!IMPORTANT]
    > Replace `user@example.com` and `SuperSecret123` in the code below with your email address and a temporary password that you'll change on first login.
    ```yaml title="compose.yaml" linesHighlight="18,19"
    services:
      db:
        image: postgres:18
        environment:
          POSTGRES_DB: wiki
          POSTGRES_USER: wiki
          POSTGRES_PASSWORD_FILE: /etc/wiki/.db-secret
        restart: unless-stopped
        volumes:
          - db-data:/var/lib/postgresql
          - ./.db-secret:/etc/wiki/.db-secret:ro

      wiki:
        image: ghcr.io/requarks/wiki:3.0.0-alpha
        depends_on:
          - db
        environment:
          ADMIN_EMAIL: user@example.com
          ADMIN_PASS: SuperSecret123
          DB_HOST: db
          DB_NAME: wiki
          DB_USER: wiki
          DB_PASS_FILE: /etc/wiki/.db-secret
        restart: unless-stopped
        volumes:
          - ./.db-secret:/etc/wiki/.db-secret:ro
        ports:
          - "80:3000"

    volumes:
      db-data:
    ```
4. Start the containers
    ```sh
    sudo docker compose up -d
    ```
#### Access your wiki
On your browser, navigate to your server IP / domain name (e.g. `http://your-server-ip/`).

> [!NOTE]
> It can take a few minutes for the containers to download and initialize. Wait a few minutes and try again if the site doesn't load.

#### (Optional) Add HTTPS Support

By default, your wiki is accessible over unencrypted HTTP. This section adds automatic HTTPS using [Caddy](https://caddyserver.com/), a web server that obtains and renews free SSL certificates from Let's Encrypt for you.

> [!IMPORTANT]
> You need a **domain name** (e.g. `wiki.example.com`) with a DNS **A record** pointing to your server's public IP address.

1. Verify that your domain resolves to your server. From your local machine, run:
    ```sh
    ping wiki.example.com
    ```
    The IP shown must match your server's public IP. If it doesn't, wait a few minutes for DNS changes to propagate and try again. The ping doesn't need to succeed (it might not) but it should show the correct IP.

2. Create a new file named `Caddyfile` *(under the same folder as `compose.yaml`)* with the following contents:
    > [!IMPORTANT]
    > Replace `wiki.example.com` with your domain name and `user@example.com` with your email address. Let's Encrypt uses this address to notify you of any certificate issues.
    > Do **NOT** modify anything on the `reverse_proxy` line *(line 6)*.
    ```nginx title="Caddyfile"
    {
        email user@example.com
    }

    wiki.example.com {
        reverse_proxy wiki:3000
    }
    ```

3. Edit your `compose.yaml` file to match the following:
    > [!WARNING]
    > Note that the `ports` section was **removed** from the `wiki` service. Caddy now handles all incoming traffic, so the wiki container must no longer claim port 80 for itself.
    ```yaml title="compose.yaml" linesHighlight="18,19,27-39,43,44"
    services:
      db:
        image: postgres:18
        environment:
          POSTGRES_DB: wiki
          POSTGRES_USER: wiki
          POSTGRES_PASSWORD_FILE: /etc/wiki/.db-secret
        restart: unless-stopped
        volumes:
          - db-data:/var/lib/postgresql
          - ./.db-secret:/etc/wiki/.db-secret:ro

      wiki:
        image: ghcr.io/requarks/wiki:3.0.0-alpha
        depends_on:
          - db
        environment:
          ADMIN_EMAIL: user@example.com
          ADMIN_PASS: SuperSecret123
          DB_HOST: db
          DB_NAME: wiki
          DB_USER: wiki
          DB_PASS_FILE: /etc/wiki/.db-secret
        restart: unless-stopped
        volumes:
          - ./.db-secret:/etc/wiki/.db-secret:ro

      caddy:
        image: caddy:2
        depends_on:
          - wiki
        restart: unless-stopped
        ports:
          - "80:80"
          - "443:443"
        volumes:
          - ./Caddyfile:/etc/caddy/Caddyfile:ro
          - caddy-data:/data
          - caddy-config:/config

    volumes:
      db-data:
      caddy-data:
      caddy-config:
    ```

4. Apply the changes:
    ```sh
    cd ~/wiki
    sudo docker compose up -d
    ```

Your wiki is now available at `https://wiki.example.com/`. Visitors using `http://` are redirected to `https://` automatically.

> [!TIP]
> Certificates renew automatically in the background, roughly a month before they expire. There is nothing to schedule or maintain.

##### Troubleshooting

If the site doesn't load over HTTPS, check what Caddy is doing:
```sh
sudo docker compose logs caddy
```

Common causes:
- **DNS isn't pointing at your server yet.** Re-run the `ping` check from step 1.
- **Port 80 is unreachable from the internet.** Let's Encrypt must reach your server on port 80 to validate the domain. Confirm your firewall allows it (`sudo ufw status`) and that your hosting provider isn't blocking it.
- **Too many failed attempts.** Let's Encrypt applies rate limits per domain. If you hit one, wait an hour before retrying.
::
:::

# Install on Host

:::block-tabs
::block-tab{label="Linux" header="2"}

> [!TIP]
> It's **highly recommended** to use containers, even if you're not familiar with Docker. See the [Guided Ubuntu Install](#guided-ubuntu-install) section for an easy, no docker knowledge required, guide to install Wiki.js on a Ubuntu machine.

*Coming soon | Not available during beta phase*
::

::block-tab{label="macOS" header="2"}
*Coming soon | Not available during beta phase*
::

::block-tab{label="Windows" header="2"}
*Coming soon | Not available during beta phase*
::
:::

# Install using Cloud Images

:::block-tabs
::block-tab{label="DigitalOcean" header="2"}
*Coming soon | Not available during beta phase*
::
:::

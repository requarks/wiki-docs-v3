---
title: Installation
description: How to install Wiki.js
published: true
date: '2026-10-04T22:42:57.852Z'
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
::block-tab{label="Docker" header="2" icon="mdi:docker"}

### Tags

Images are tagged to **major**, **major.minor** and **major.minor.patch** versions.
It's recommended to use the **major** version, unless you have a specific requirement to pin your deployment to specific version.

> [!WARNING]
> Note that Wiki.js 3.x is in beta and images are currently tagged as `3.0.0-beta`. The non-beta tags below won't work until the beta phase has ended.

```sh
# -----------------------------
# BETA VERSION
# -----------------------------
ghcr.io/requarks/wiki:3.0.0-beta

# or using a specific version:
ghcr.io/requarks/wiki:3.0.0-beta.617

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
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "ADMIN_EMAIL=user@example.com" -e "ADMIN_PASS=SuperSecret123" -e "DB_HOST=db" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:3.0.0-beta
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
    image: ghcr.io/requarks/wiki:3.0.0-beta
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

::block-tab{label="Kubernetes" header="2" icon="mdi:kubernetes"}

Deploys Wiki.js 3.x, with a bundled PostgreSQL 18 or an existing PostgreSQL 16+ server.

### Quickstart

The chart is published as an OCI artifact, so no `helm repo add` is needed:

> [!WARNING]
> As this chart is still in beta, you **MUST** pass either the `--devel` flag or specify the version manually using the `--version 3.0.0-beta.<build>` flag.

```sh
# Deploy Chart
helm install wiki oci://ghcr.io/requarks/charts/wiki --devel

# Monitor Deployment
kubectl rollout status deployment/wiki
```

Unless `admin.email` and `admin.password` are set, the first login is `admin@example.com` / `12345678`, and it has to be changed.

### Values

Customize your deployment using a `values.yaml` file.

> [!NOTE] Reference
> Refer to the [values.yaml](https://github.com/requarks/wiki/blob/scarlett/dev/chart/values.yaml) file for all supported values and the chart [README](https://github.com/requarks/wiki/tree/scarlett/dev/chart#readme) for documentation.

You can then deploy the chart by referencing your values.yaml file:
```sh
helm install wiki oci://ghcr.io/requarks/charts/wiki --devel -f values.yaml
```

### Database

By default, the chart includes a PostgreSQL database as a single StatefulSet replica for convenience. For serious deployments, you should instead deploy your own PostgreSQL cluster using an operator like [CloudNativePG](https://cloudnative-pg.io/).

#### Using a Connection String

Passed to the wiki as `DATABASE_URL`, so an operator's generated Secret can be used as it is. For CloudNativePG:

```yaml
postgresql:
  enabled: false
externalDatabase:
  connectionString:
    existingSecret: mycluster-app # created by CloudNativePG for the cluster's app database
    existingSecretKey: uri
```

#### Using Individual Parameters

Connection parameters can also be passed individually, e.g.:

```yaml
postgresql:
  enabled: false
externalDatabase:
  parameters:
    host: pg.databases.svc
    database: wiki
    user: wiki
    existingSecret: wiki-db # key: password
  ssl:
    enabled: true
    existingSecret: pg-ca # key: ca.crt, and optionally tls.crt / tls.key
```

### Gateway / Ingress

The chart supports both the [Gateway API](https://kubernetes.io/docs/concepts/services-networking/gateway/) (via `httpRoute.enabled`) and [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) (via `ingress.enabled`).

In both cases, turn on **Administration Area :la:arrow-right: Security :la:arrow-right: Trust Proxy**, so the wiki records the visitor's address rather than the proxy's.

> [!NOTE] Reference
> Refer to the [values.yaml](https://github.com/requarks/wiki/blob/scarlett/dev/chart/values.yaml) file for all supported values and the chart [README](https://github.com/requarks/wiki/tree/scarlett/dev/chart#readme) for documentation.

### Replicas

The number of replicas (via `replicaCount`) can be raised freely. Replicas coordinate through the database, collaborative editing included, so no sticky sessions are needed. Replicas don't need to be able to talk to each other, however, they **MUST** both connect to the same database / cluster.
::

::block-tab{label="Guided Ubuntu Install" header="2" icon="mdi:ubuntu"}
This guide provides an easy, no docker knowledge required, step-by-step instructions to install Wiki.js on a fresh Ubuntu server using containers.

#### Requirements

- Ubuntu 26.04 or 24.04
- Local Terminal or Remote SSH Access

#### Install dependencies

::block-steps
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
::

#### Setup containers

::block-steps
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
        image: ghcr.io/requarks/wiki:3.0.0-beta
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
::

#### Access your wiki
On your browser, navigate to your server IP / domain name (e.g. `http://your-server-ip/`).

> [!NOTE]
> It can take a few minutes for the containers to download and initialize. Wait a few minutes and try again if the site doesn't load.

#### (Optional) Add HTTPS Support

By default, your wiki is accessible over unencrypted HTTP. This section adds automatic HTTPS using [Caddy](https://caddyserver.com/), a web server that obtains and renews free SSL certificates from Let's Encrypt for you.

> [!IMPORTANT]
> You need a **domain name** (e.g. `wiki.example.com`) with a DNS **A record** pointing to your server's public IP address.

::block-steps
1. Verify that your domain resolves to your server. From your local machine, run:
    ```sh
    ping wiki.example.com
    ```
    The IP shown must match your server's public IP. If it doesn't, wait a few minutes for DNS changes to propagate and try again. The ping doesn't need to succeed (it might not) but it should show the correct IP.

2. Create a new file named `Caddyfile` *(under the same folder as `compose.yaml`)* with the following contents:
    > [!IMPORTANT]
    > Replace `wiki.example.com` with your domain name and `user@example.com` with your email address. Let's Encrypt uses this address to notify you of any certificate issues.
    > Do **NOT** modify anything on the `reverse_proxy` line *(line 6)*.
    ```nginx title="Caddyfile" linesHighlight="2,5"
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
        image: ghcr.io/requarks/wiki:3.0.0-beta
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
::

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
::block-tab{label="Linux" header="2" icon="mdi:linux"}

> [!TIP]
> It's **highly recommended** to use containers, even if you're not familiar with Docker. See the [Guided Ubuntu Install](#guided-ubuntu-install) section for an easy, no docker knowledge required, guide to install Wiki.js on a Ubuntu machine.

Before going any further, make sure your system meets all the [requirements](/setup/requirements). The following instructions assume Node.js and PostgreSQL are already installed.

#### Setup

::block-steps
1. Download the latest version of Wiki.js:
    ```sh
    wget https://github.com/requarks/wiki/releases/latest/download/wiki-js.tar.gz
    ```

2. Extract the package to the final destination of your choice:
    ```sh
    mkdir wiki
    tar xzf wiki-js.tar.gz -C ./wiki
    cd ./wiki
    ```

3. Rename the sample config file to `config.yml`:
    ```sh
    mv config.sample.yml config.yml
    ```

4. Edit the config file and fill in your database and port settings (refer to the [configuration reference](/setup/config)):
    ```sh
    nano config.yml
    ```

4. Run Wiki.js
    ```sh
    node --no-experimental-webstorage backend
    ```
::

#### Run as service

There are several solutions to run Wiki.js as a background service. We'll focus on **systemd** in this guide as it's available in nearly all linux distributions.

::block-steps
1. Create a new file named `wiki.service` inside directory `/etc/systemd/system`.
    ```sh
    nano /etc/systemd/system/wiki.service
    ```
2. Paste the following contents (assuming your wiki is installed at `/var/wiki`):
    ```ini
    [Unit]
    Description=Wiki.js
    After=network.target

    [Service]
    Type=simple
    ExecStart=/usr/bin/node --no-experimental-webstorage backend
    Restart=always
    # Consider creating a dedicated user for Wiki.js here instead of using nobody:
    User=nobody
    Environment=NODE_ENV=production
    WorkingDirectory=/var/wiki

    [Install]
    WantedBy=multi-user.target
    ```
3. Save the service file ( <kbd>CTRL</kbd>+<kbd>X</kbd>, followed by <kbd>Y</kbd> ).
4. Reload systemd:
    ```sh
    systemctl daemon-reload
    ```
5. Run the service:
    ```sh
    systemctl start wiki
    ```
6. Enable the service on system boot.
    ```sh
    systemctl enable wiki
    ```
::

> [!TIP]
> You can see the logs of the service using `journalctl -u wiki`

::

::block-tab{label="macOS" header="2" icon="mdi:apple"}

Before going any further, make sure your system meets all the [requirements](/setup/requirements). The following instructions assume Node.js and PostgreSQL are already installed.

::block-steps
1. Open **Terminal**.
2. Download the latest version of Wiki.js:
    ```sh
    wget https://github.com/requarks/wiki/releases/latest/download/wiki-js.tar.gz
    ```

3. Extract the package to the final destination of your choice:
    ```sh
    mkdir wiki
    tar xzf wiki-js.tar.gz -C ./wiki
    cd ./wiki
    ```

4. Rename the sample config file to `config.yml`:
    ```sh
    mv config.sample.yml config.yml
    ```

5. Edit the config file and fill in your database and port settings (refer to the [configuration reference](/setup/config)):
    ```sh
    nano config.yml
    ```

6. Run Wiki.js
    ```sh
    node --no-experimental-webstorage backend
    ```
::

::

::block-tab{label="Windows" header="2" icon="mdi:microsoft-windows"}

Before going any further, make sure your system meets all the [requirements](/setup/requirements). The following instructions assume Node.js and PostgreSQL are already installed.

::block-steps
1. Open a **Powershell** prompt in administrator mode.
2. Download the latest version of Wiki.js:
    ```powershell
    Invoke-WebRequest -Uri "https://github.com/requarks/wiki/releases/latest/download/wiki-js-windows.tar.gz" -OutFile "wiki-js.tar.gz"
    ```

3. Extract the package to the final destination of your choice:
    ```powershell
    New-Item -Path "C:\" -Name "wiki" -ItemType "directory"
    tar xzf wiki-js.tar.gz -C "C:\wiki"
    cd C:\wiki
    ```

4. Rename the sample config file to `config.yml`:
    ```powershell
    Rename-Item -Path config.sample.yml -NewName config.yml
    ```

5. Edit the config file and fill in your database and port settings (refer to the [configuration reference](/setup/config)):
    ```powershell
    notepad .\config.yml
    ```

6. Run Wiki.js
    ```powershell
    node --no-experimental-webstorage backend
    ```
::

::
:::

# Install using Cloud Images

:::block-tabs
::block-tab{label="DigitalOcean" header="2" icon="mdi:digital-ocean"}
*Coming soon | Not available during beta phase*

> [!TIP] Status
> This image is officially maintained by the Wiki.js team.
::
::block-tab{label="PikaPods" header="2"}
See the [Wiki.js page on PikaPods](https://www.pikapods.com/pods?run=wiki-js)

> [!WARNING] Status
> - Only the 2.x image available at the moment.
> - This image is maintained by PikaPods.
::
:::

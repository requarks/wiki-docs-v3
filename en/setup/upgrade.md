---
title: Upgrade
description: How to upgrade to the latest version
published: true
date: '2026-10-06T23:37:28.720Z'
tags:
  - setup
editor: markdown
dateCreated: '2026-08-11T05:04:17.122Z'
---

> [!IMPORTANT]
> While upgrades are generally safe and it's very unlikely that it would result in data loss, **it's your responsibility to have a proper backup of your database before performing an upgrade**. Note that it's not possible to go back to a previous version of Wiki.js once the database schema has been upgraded.

> [!NOTE] Upgrade from Wiki.js 2.x
> To upgrade from 2.x, refer to the [Upgrade from 2.x](#upgrade-from-2x) section below.

# In-place upgrade

:::block-tabs
::block-tab{label="Docker" header="2" icon="mdi:docker"}
#### Standalone Container

Upgrading is simply a matter of recreating the container with the latest image version:

```bash
# Stop and remove container named "wiki"
docker stop wiki
docker rm wiki

# Pull latest image of Wiki.js
docker pull ghcr.io/requarks/wiki:3.0.0-beta

# Create new container of Wiki.js based on latest image
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_HOST=db" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:3.0.0-beta
```

Check out the [Docker installation guide](/setup/installation#environment-variables) for all the possible options when creating a Wiki.js container.

#### Docker Compose

The following commands will pull the latest image and recreate the containers defined in the [docker-compose](/setup/installation#docker-compose) file:

```bash
docker compose pull wiki
docker compose up --force-recreate -d
```
::

::block-tab{label="Kubernetes" header="2" icon="mdi:kubernetes"}
Use the `helm upgrade` command to upgrade to the latest version:

> [!WARNING]
> As this chart is still in beta, you **MUST** pass either the `--devel` flag or specify the version manually using the `--version 3.0.0-beta.<build>` flag.

```sh
# Without a values.yaml file:
helm upgrade wiki oci://ghcr.io/requarks/charts/wiki --devel --reset-then-reuse-values

# With a values.yaml file:
helm upgrade wiki oci://ghcr.io/requarks/charts/wiki --devel -f values.yaml
```

> [!NOTE] Reference
> Refer to the [values.yaml](https://github.com/requarks/wiki/blob/scarlett/dev/chart/values.yaml) file for all supported values and the chart [README](https://github.com/requarks/wiki/tree/scarlett/dev/chart#readme) for documentation.
::

::block-tab{label="Linux" header="2" icon="mdi:linux"}

> [!NOTE]
> The steps below assume an installation in a subdirectory named `wiki`.

::block-steps
1. Stop the running Wiki.js instance.
2. Make a backup of your config.yml file:
    ```sh
    cp wiki/config.yml ~/config.yml.bak
    ```

3. Delete the application folder:
    > [!WARNING]
    > If you're storing assets on disk in a subdirectory of the installation (using the [Local File System](/admin/storage/disk) storage option), make sure to either **create a backup** of it first, or **exclude it** from the delete operation.
    ```sh
    rm -rf wiki/*
    ```

4. Download the latest version of Wiki.js:
    ```sh
    wget https://github.com/requarks/wiki/releases/latest/download/wiki-js.tar.gz
    ```

5. Extract the package to the original location:
    ```sh
    tar xzf wiki-js.tar.gz -C ./wiki
    cd ./wiki
    ```

6. Restore your `config.yml` back to its original location:
    ```sh
    cp ~/config.yml.bak ./config.yml
    ```

7. Run Wiki.js
    ```sh
    node --no-experimental-webstorage backend
    ```
::

::

::block-tab{label="macOS" header="2" icon="mdi:apple"}

> [!NOTE]
> The steps below assume an installation in a subdirectory named `wiki`.

::block-steps
1. Stop the running Wiki.js instance.
2. Make a backup of your config.yml file:
    ```sh
    cp wiki/config.yml ~/config.yml.bak
    ```

3. Delete the application folder:
    > [!WARNING]
    > If you're storing assets on disk in a subdirectory of the installation (using the [Local File System](/admin/storage/disk) storage option), make sure to either **create a backup** of it first, or **exclude it** from the delete operation.
    ```sh
    rm -rf wiki/*
    ```

4. Download the latest version of Wiki.js:
    ```sh
    wget https://github.com/requarks/wiki/releases/latest/download/wiki-js.tar.gz
    ```

5. Extract the package to the original location:
    ```sh
    tar xzf wiki-js.tar.gz -C ./wiki
    cd ./wiki
    ```

6. Restore your `config.yml` back to its original location:
    ```sh
    cp ~/config.yml.bak ./config.yml
    ```

7. Run Wiki.js
    ```sh
    node --no-experimental-webstorage backend
    ```
::

::

::block-tab{label="Windows" header="2" icon="mdi:microsoft-windows"}

> [!NOTE]
> The steps below assume an installation at folder location `C:\wiki`.

::block-steps
1. Open a **Powershell** prompt in administrator mode.
2. Make a backup of `config.yml` file.
    ```powershell
    Copy-Item "C:\wiki\config.yml" -Destination "C:\config.yml.bak"
    ```

3. Delete the application folder contents.
    > [!WARNING]
    > If you're storing assets on disk in a subdirectory of the installation (using the [Local File System](/admin/storage/disk) storage option), make sure to either **create a backup** of it first, or **exclude it** from the delete operation.
    ```powershell
    Clear-Content "C:\wiki\*"
    ```

4. Download the latest version of Wiki.js:
    ```powershell
    Invoke-WebRequest -Uri "https://github.com/requarks/wiki/releases/latest/download/wiki-js.tar.gz" -OutFile "wiki-js.tar.gz"
    ```

5. Extract the package to the original location:
    ```powershell
    tar xzf wiki-js.tar.gz -C "C:\wiki"
    cd C:\wiki
    ```

6. Copy your `config.yml` backup file back to it's original location.
    ```powershell
    Copy-Item "C:\config.yml.bak" -Destination "C:\wiki\config.yml"
    ```
7. Run Wiki.js
    ```powershell
    node --no-experimental-webstorage backend
    ```
::

::
:::

# Upgrade from 2.x

## Migration Process

Because of the major differences between 2.x and 3.x, an in-place upgrade is not possible. Instead, a migration process is provided to easily transfer all data between your old 2.x installation and a new 3.x installation.

::block-steps
1. **Create a .wkbackup migration package**
    1. Upgrade your Wiki.js 2.x installation to the latest version.
    2. Under **Administration Area** :la:arrow-right: **Utilities**, click the **Export for Wiki.js 3.x** tool.
    3. Leave all checkboxes checked and click the **Create Package** button.
    4. Download the package upon completion.

2. **Install Wiki.js 3.x**
    1. Install a new Wiki.js 3.x instance using the [installation instructions](/setup/installation).
    2. Login using the root administrator account.
    3. On the welcome screen, click the **Administration Area** button.
    4. Go to **Utilities** and click **Proceed** next to the **Import from Wiki.js 2.x** utility.

3. **Import the migration package**
    1. Leave all options to their defaults, and browse to your .wkbackup file you downloaded earlier by clicking the **Select archive...** button.
    2. Click the **Start Import** button to begin the import.
    3. Follow the progress on the right. Look out for any error.
    4. Review site settings and system configuration to ensure everything matches your expectations.
::

> [!IMPORTANT]
> Some settings are deliberatly **NOT** imported:
> - Module settings *(like storage, authentication, comments, analytics, etc.)* to avoid unwanted conflicts with your old Wiki.js 2.x installation.
> - Security settings because of potential differences in behavior.
> - Site logo, as it's uploaded rather than linked externally in 3.x.
> - Site hostname to avoid locking you out of your new installation by pointing to the 2.x installation hostname.

> [!TIP]
> The import is idempotent and can safely be performed multiple times. Existing items will be skipped unless the **Overwrite on conflict** option is checked.

## Markdown Changes

### Admonitions

While the 2.x syntax (using CSS classes) is still supported, admonitions should now be written using the [more widely accepted syntax](/guide/markdown#admonitions). This brings compatibility with multiple providers, like GitHub.

```md title="2.x Syntax"
> Some warning text here
{.is-warning}
```

```md title="3.x Syntax"
> [!WARNING]
> Some warning text here
```

### Diagrams

Diagrams previously defined using a code block must be enclosed into their respective content block to be rendered:

| Type | Content Block |
| :-- | :-- |
| katex | [block-katex](/guide/blocks/katex) |
| kroki | [block-kroki](/guide/blocks/kroki) |
| mermaid | [block-diagram](/guide/blocks/diagram) |
| plantuml | [block-plantuml](/guide/blocks/plantuml) |
{.table-leading-col}

### Draw.io

Draw.io diagrams must be converted to the XML format used by the [draw.io content block](/guide/blocks/drawio).

**Existing diagrams must first be exported to XML from a Wiki.js 2.x instance:**

::block-steps
1. Edit the page containing the diagram and click the **Edit Diagram** button on the desired diagram to open the Draw.io editor.
2. In the menu bar, go to **File** :la:arrow-right: **Export as** :la:arrow-right: **XML**
3. Click **Export**
4. Change the **Where** option to **Open in New Window**, then click **OK**.
5. Copy the XML source code.
::

**On the new Wiki.js 3.x instance:**
::block-steps
1. Edit the page containing the old diagram and delete the old code block.
2. In it's place, insert a Draw.io content block and replace the `INSERT XML CODE HERE` placeholder with the XML code you copied earlier:
    ````md
    ::block-drawio
    ```xml
    INSERT XML CODE HERE
    ```
    ::
    ````
3. Save the page.
::

### Tabsets

Tabs are now declared using the [tabs content block](/guide/markdown#tabs). Existing tabsets using the older CSS syntax will be displayed as standard text rather than tabs.

```md title="2.x Syntax"
## Tabs {.tabset}
### First Tab

Any content here will go into the first tab...

### Second Tab

Any content here will go into the second tab...

### Third Tab

Any content here will go into the third tab...
```

```md title="3.x Syntax"
:::block-tabs
::block-tab{label="First Tab"}
Any content here will go into the first tab...
::

::block-tab{label="Second Tab"}
Any content here will go into the second tab...
::

::block-tab{label="Third Tab"}
Any content here will go into the third tab...
::
:::
```

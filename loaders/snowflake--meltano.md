---
title: Snowflake (`meltano` variant)
layout: plugin_page
description: Use Meltano to pull data from various sources and load it into Snowflake
---

The `target-snowflake` [loader](https://meltano.com/plugins/loaders/) loads [extracted](https://meltano.com/plugins/extractors/) data into a [Snowflake](https://www.snowflake.com/) data warehouse.

- **Repository**: <https://github.com/meltano/target-snowflake>
- **Maintainer**: Meltano Community
- **Maintenance status**: Active

#### Alternative variants

Multiple [variants](https://docs.meltano.com/concepts/plugins#variants) of `target-snowflake` are available.
This document describes the `meltano` variant.

Alternative options are [`transferwise`](./snowflake.html) (default) and [`datamill-co`](./snowflake--datamill-co.html).

## Getting Started

### Prerequisites

If you haven't already, follow the initial steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Install Meltano](https://docs.meltano.com/getting-started.html#install-meltano)
1. [Create your Meltano project](https://docs.meltano.com/getting-started.html#create-your-meltano-project)
1. [Add an extractor to pull data from a source](https://docs.meltano.com/getting-started.html#add-an-extractor-to-pull-data-from-a-source)

### Installation and configuration

#### Using the Command Line Interface

1. Add the `meltano` variant of the `target-snowflake` loader to your project using [`meltano add`](https://docs.meltano.com/command-line-interface.html#add):

    ```bash
    meltano add loader target-snowflake --variant meltano
    ```

1. Configure the [settings](#settings) below using [`meltano config`](https://docs.meltano.com/command-line-interface.html#config).

#### Using Meltano UI

1. Start [Meltano UI](https://docs.meltano.com/ui.html) using [`meltano ui`](https://docs.meltano.com/command-line-interface.html#ui):

    ```bash
    meltano ui
    ```

1. Open the Loaders interface at <http://localhost:5000/loaders>.
1. Click the arrow next to the "Add to project" button for "Snowflake".
1. Choose "Add variant 'meltano'".
1. Configure the [settings](#settings) below in the "Configuration" interface that opens automatically.

### Next steps

Follow the remaining step of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Run a data integration (EL) pipeline](https://docs.meltano.com/getting-started.html#run-a-data-integration-el-pipeline)

If you run into any issues, chat with us in [#troubleshooting](https://meltano.slack.com/archives/C01TCRBBJD7) on [Slack](https://meltano.com/slack).

## Settings

`target-snowflake` requires the [configuration](https://docs.meltano.com/configuration.html) of the following settings:

- [Account](#account)
- [Username](#username)
- [Password](#password)
- [Role](#role)
- [Database](#database)
- [Warehouse](#warehouse)
- [Schema](#schema)

These and other supported settings are documented below.
To quickly find the setting you're looking for, use the Table of Contents in the sidebar.

#### Minimal configuration

A minimal configuration of `target-snowflake` in your [`meltano.yml` project file](https://docs.meltano.com/concepts/project#meltano-yml-project-file) will look like this:

```yml{5-13}
plugins:
  loaders:
  - name: target-snowflake
    variant: meltano
    config:
      account: my_account
      username: my_username
      role: MY_ROLE
      database: MY_DATABASE
      warehouse: MY_WAREHOUSE
      # schema: MY_SCHEMA    # override if default (see below) is not appropriate
```

Sensitive values are most appropriately stored in [the environment](https://docs.meltano.com/configuration.html#configuring-settings) or your project's [`.env` file](https://docs.meltano.com/concepts/project#env):

```bash
export TARGET_SNOWFLAKE_PASSWORD=my_password
```

### Account

- Name: `account`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_ACCOUNT`, alias: `SF_ACCOUNT`, `SNOWFLAKE_ACCOUNT`

Account Name in Snowflake (`https://<account>.snowflakecomputing.com`)

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set account <account>

export TARGET_SNOWFLAKE_ACCOUNT=<account>
```

### Username

- Name: `username`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_USERNAME`, alias: `SF_USER`, `SNOWFLAKE_USER`

The username you use for logging in

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set username <username>

export TARGET_SNOWFLAKE_USERNAME=<username>
```

### Password

- Name: `password`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_PASSWORD`, alias: `SF_PASSWORD`, `SNOWFLAKE_PASSWORD`

The password you use for logging in

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set password <password>

export TARGET_SNOWFLAKE_PASSWORD=<password>
```

### Role

- Name: `role`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_ROLE`, alias: `SF_ROLE`, `SNOWFLAKE_ROLE`

Role to be used for loading the data, e.g. `LOADER`. Also this role is GRANTed usage to all tables and schemas created

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set role <role>

export TARGET_SNOWFLAKE_ROLE=<role>
```

### Database

- Name: `database`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_DATABASE`, alias: `SF_DATABASE`, `SNOWFLAKE_DATABASE`

The name of the Snowflake database you want to use

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set database <database>

export TARGET_SNOWFLAKE_DATABASE=<database>
```

### Warehouse

- Name: `warehouse`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_WAREHOUSE`, alias: `SF_WAREHOUSE`, `SNOWFLAKE_WAREHOUSE`

The name of the Snowflake warehouse you want to use

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set warehouse <warehouse>

export TARGET_SNOWFLAKE_WAREHOUSE=<warehouse>
```

### Schema

- Name: `schema`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_SCHEMA`, alias: `SF_SCHEMA`, `SNOWFLAKE_SCHEMA`
- Default: `$MELTANO_EXTRACT__LOAD_SCHEMA`, which [will expand to](https://docs.meltano.com/configuration.html#expansion-in-setting-values) the value of the [`load_schema` extra](https://docs.meltano.com/concepts/plugins#load-schema-extra) for the extractor used in the pipeline, which defaults to the extractor's namespace, e.g. `tap_gitlab` for [`tap-gitlab`](https://meltano.com/plugins/extractors/gitlab.html). Values are automatically converted to uppercase before they're passed on to the plugin, so `tap_gitlab` becomes `TAP_GITLAB`.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set schema <schema>

export TARGET_SNOWFLAKE_SCHEMA=<schema>
```

### Batch Size

- Name: `batch_size`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_BATCH_SIZE`
- Default: `5000`

How many records are sent to Snowflake at a time?

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set batch_size 10000

export TARGET_SNOWFLAKE_BATCH_SIZE=10000
```

### Timestamp Column

- Name: `timestamp_column`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TARGET_SNOWFLAKE_TIMESTAMP_COLUMN`
- Default: `__loaded_at`

Name of the column used for recording the timestamp when Data are uploaded to Snowflake.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config target-snowflake set timestamp_column <column>

export TARGET_SNOWFLAKE_TIMESTAMP_COLUMN=<column>
```

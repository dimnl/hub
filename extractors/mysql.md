---
title: MySQL / MariaDB
layout: plugin_page
description: Use Meltano to pull data from a MySQL or MariaDB database and load it into Snowflake, PostgreSQL, and more
---


The `tap-mysql` [extractor](https://meltano.com/plugins/extractors/) pulls data from a [MySQL](https://www.mysql.com/) or [MariaDB](https://mariadb.org/) database.

- **Repository**: <https://github.com/transferwise/pipelinewise-tap-mysql>
- **Documentation**: <https://transferwise.github.io/pipelinewise/connectors/taps/mysql.html>
- **Maintainer**: [Wise](https://wise.com/)
- **Maintenance status**: Active

## Getting Started

### Prerequisites

If you haven't already, follow the initial steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Install Meltano](https://docs.meltano.com/getting-started.html#install-meltano)
1. [Create your Meltano project](https://docs.meltano.com/getting-started.html#create-your-meltano-project)

Then, follow the steps in the ["Setup requirements" section of the documentation](https://transferwise.github.io/pipelinewise/connectors/taps/mysql.html#mysql-setup-requirements).

### Installation and configuration

#### Using the Command Line Interface

1. Add the `tap-mysql` extractor to your project using [`meltano add`](https://docs.meltano.com/command-line-interface.html#add):

    ```bash
    meltano add extractor tap-mysql
    ```

1. Configure the [settings](#settings) below using [`meltano config`](https://docs.meltano.com/command-line-interface.html#config).

#### Using Meltano UI

1. Start [Meltano UI](https://docs.meltano.com/ui.html) using [`meltano ui`](https://docs.meltano.com/command-line-interface.html#ui):

    ```bash
    meltano ui
    ```

1. Open the Extractors interface at <http://localhost:5000/extractors>.
1. Click the "Add to project" button for "MySQL".
1. Configure the [settings](#settings) below in the "Configuration" interface that opens automatically.

### Next steps

Follow the remaining steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Select entities and attributes to extract](https://docs.meltano.com/getting-started.html#select-entities-and-attributes-to-extract)
1. [Choose how to replicate each entity](https://docs.meltano.com/getting-started.html#choose-how-to-replicate-each-entity)

    Supported [replication methods](https://docs.meltano.com/integration.html#replication-methods):
    [`LOG_BASED`](https://docs.meltano.com/integration.html#log-based-incremental-replication),
    [`INCREMENTAL`](https://docs.meltano.com/integration.html#key-based-incremental-replication),
    [`FULL_TABLE`](https://docs.meltano.com/integration.html#full-table-replication)

1. [Add a loader to send data to a destination](https://docs.meltano.com/getting-started.html#add-a-loader-to-send-data-to-a-destination)

    Note that this extractor is incompatible with the default `datamill-co` [variants](https://docs.meltano.com/concepts/plugins#variants)
    of [`target-postgres`](https://meltano.com/plugins/loaders/postgres.html) and [`target-snowflake`](https://meltano.com/plugins/loaders/snowflake.html),
    because they don't support stream names that include the source schema in addition to the table name: `<schema>-<table>`, e.g. `public-accounts`.

    Instead, use the `transferwise` variants that were made to be used with this extractor:
    [`target-postgres`](https://meltano.com/plugins/loaders/postgres--transferwise.html) and [`target-snowflake`](https://meltano.com/plugins/loaders/snowflake--transferwise.html).

1. [Run a data integration (EL) pipeline](https://docs.meltano.com/getting-started.html#run-a-data-integration-el-pipeline)

If you run into any issues, chat with us in [#troubleshooting](https://meltano.slack.com/archives/C01TCRBBJD7) on [Slack](https://meltano.com/slack).

## Settings

`tap-mysql` requires the [configuration](https://docs.meltano.com/configuration.html) of the following settings:

- [Host](#host)
- [Port](#port)
- [User](#user)
- [Password](#password)

These and other supported settings are documented below.
To quickly find the setting you're looking for, use the Table of Contents in the sidebar.

#### Minimal configuration

A minimal configuration of `tap-mysql` in your [`meltano.yml` project file](https://docs.meltano.com/concepts/project#meltano-yml-project-file) will look like this:

```yml{5-8}
plugins:
  extractors:
  - name: tap-mysql
    variant: transferwise
    config:
      host: mysql.example.com
      port: 3306
      user: my_user
```

Sensitive values are most appropriately stored in [the environment](https://docs.meltano.com/configuration.html#configuring-settings) or your project's [`.env` file](https://docs.meltano.com/concepts/project#env):

```bash
export TAP_MYSQL_PASSWORD=my_password
```

### Host

- Name: `host`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_HOST`
- Default: `localhost`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set host <host>

export TAP_MYSQL_HOST=<host>
```

### Port

- Name: `port`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_PORT`
- Default: `3306`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set port 3307

export TAP_MYSQL_PORT=3307
```

### User

- Name: `user`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_USER`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set user <user>

export TAP_MYSQL_USER=<user>
```

### Password

- Name: `password`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_PASSWORD`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set password <password>

export TAP_MYSQL_PASSWORD=<password>
```

### Database

- Name: `database`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_DATABASE`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set database <database>

export TAP_MYSQL_DATABASE=<database>
```

### SSL

- Name: `ssl`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_SSL`
- Default: `false`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set ssl true

export TAP_MYSQL_SSL=true
```

### Filter DBs

- Name: `filter_dbs`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_FILTER_DBS`

Comma separated list of schemas to extract tables only from particular schemas and to improve data extraction performance

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set filter_dbs <schema1>,<schema2>

export TAP_MYSQL_FILTER_DBS=<schema1>,<schema2>
```

### Session SQLs

- Name: `session_sqls`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_MYSQL_SESSION_SQLS`
- Default:

  ```json
  [
    "SET @@session.time_zone='+0:00'",
    "SET @@session.wait_timeout=28800",
    "SET @@session.net_read_timeout=3600",
    "SET @@session.innodb_lock_wait_timeout=3600"
  ]
  ```

List of SQL commands to run when a connection made. This allows to set session variables dynamically, like timeouts.

#### How to use

Manage this setting directly in your [`meltano.yml` project file](https://docs.meltano.com/concepts/project#meltano-yml-project-file):

```yml{5-8}
plugins:
  extractors:
  - name: tap-mysql
    variant: transferwise
    config:
      session_sqls:
        - SET @@session.<variable>=<value>
        # ...
```

Alternatively, manage this setting using [`meltano config`](https://docs.meltano.com/command-line-interface.html#config) or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-mysql set session_sqls '["SET @@session.<variable>=<value>", ...]'

export TAP_MYSQL_SESSION_SQLS='["SET @@session.<variable>=<value>", ...]'
```

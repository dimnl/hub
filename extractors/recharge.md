---
title: ReCharge
layout: plugin_page
description: Use Meltano to pull data from the ReCharge API and load it into Snowflake, PostgreSQL, and more
---


The `tap-recharge` [extractor](https://meltano.com/plugins/extractors/) pulls data from the [ReCharge API](https://rechargepayments.com/developers/).

- **Repository**: <https://github.com/singer-io/tap-recharge>
- **Maintainer**: [Stitch](https://www.stitchdata.com/)
- **Maintenance status**: Unresponsive to community issues and contributions
  - A [more active fork](https://github.com/singer-io/tap-recharge/network) may be available that you can [use instead](https://docs.meltano.com/plugin-management.html#using-a-custom-fork-of-a-plugin).
  - This plugin is [up for adoption](https://docs.meltano.com/contributor-guide.html#adopting-a-plugin)!

## Getting Started

### Prerequisites

If you haven't already, follow the initial steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Install Meltano](https://docs.meltano.com/getting-started.html#install-meltano)
1. [Create your Meltano project](https://docs.meltano.com/getting-started.html#create-your-meltano-project)

### Installation and configuration

#### Using the Command Line Interface

1. Add the `tap-recharge` extractor to your project using [`meltano add`](https://docs.meltano.com/command-line-interface.html#add):

    ```bash
    meltano add extractor tap-recharge
    ```

1. Configure the [settings](#settings) below using [`meltano config`](https://docs.meltano.com/command-line-interface.html#config).

#### Using Meltano UI

1. Start [Meltano UI](https://docs.meltano.com/ui.html) using [`meltano ui`](https://docs.meltano.com/command-line-interface.html#ui):

    ```bash
    meltano ui
    ```

1. Open the Extractors interface at <http://localhost:5000/extractors>.
1. Click the "Add to project" button for "ReCharge".
1. Configure the [settings](#settings) below in the "Configuration" interface that opens automatically.

### Next steps

Follow the remaining steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Select entities and attributes to extract](https://docs.meltano.com/getting-started.html#select-entities-and-attributes-to-extract)
1. [Add a loader to send data to a destination](https://docs.meltano.com/getting-started.html#add-a-loader-to-send-data-to-a-destination)
1. [Run a data integration (EL) pipeline](https://docs.meltano.com/getting-started.html#run-a-data-integration-el-pipeline)

If you run into any issues, chat with us in [#troubleshooting](https://meltano.slack.com/archives/C01TCRBBJD7) on [Slack](https://meltano.com/slack).

## Settings

`tap-recharge` requires the [configuration](https://docs.meltano.com/configuration.html) of the following settings:

- [Access Token](#access-token)
- [Start Date](#start-date)

These and other supported settings are documented below.
To quickly find the setting you're looking for, use the Table of Contents in the sidebar.

#### Minimal configuration

A minimal configuration of `tap-recharge` in your [`meltano.yml` project file](https://docs.meltano.com/concepts/project#meltano-yml-project-file) will look like this:

```yml{5-6}
plugins:
  extractors:
  - name: tap-recharge
    variant: singer-io
    config:
      start_date: '2020-10-01T00:00:00Z'
```

Sensitive values are most appropriately stored in [the environment](https://docs.meltano.com/configuration.html#configuring-settings) or your project's [`.env` file](https://docs.meltano.com/concepts/project#env):

```bash
export TAP_RECHARGE_ACCESS_TOKEN=my_access_token
```

### Access Token

- Name: `access_token`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_RECHARGE_ACCESS_TOKEN`

Private API token

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-recharge set access_token <token>

export TAP_RECHARGE_ACCESS_TOKEN=<token>
```

### Start Date

- Name: `start_date`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_RECHARGE_START_DATE`

This property determines how much historical data will be extracted.

Please be aware that the larger the time period and amount of data, the longer the initial extraction can be expected to take.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-recharge set start_date YYYY-MM-DDTHH:MM:SSZ

export TAP_RECHARGE_START_DATE=YYYY-MM-DDTHH:MM:SSZ

# For example:
meltano config tap-recharge set start_date 2020-10-01T00:00:00Z

export TAP_RECHARGE_START_DATE=2020-10-01T00:00:00Z
```

### User Agent

- Name: `user_agent`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_RECHARGE_USER_AGENT`
- Default: `tap-recharge via Meltano`

User agent to send to ReCharge along with API requests. Typically includes name of integration and an email address you can be reached at, e.g. `tap-recharge via Meltano <user@example.com>`.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-recharge set user_agent <user_agent>

export TAP_RECHARGE_USER_AGENT=<user_agent>
```

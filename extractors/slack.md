---
title: Slack
layout: plugin_page
description: Use Meltano to pull data from the Slack API and load it into Snowflake, PostgreSQL, and more
---


The `tap-slack` [extractor](https://meltano.com/plugins/extractors/) pulls data from the [Slack API](https://api.slack.com/).

- **Repository**: <https://github.com/Mashey/tap-slack>
- **Maintainer**: [Mashey](https://www.mashey.com/)
- **Maintenance status**: Active

## Getting Started

### Prerequisites

If you haven't already, follow the initial steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Install Meltano](https://docs.meltano.com/getting-started.html#install-meltano)
1. [Create your Meltano project](https://docs.meltano.com/getting-started.html#create-your-meltano-project)

### Installation and configuration

#### Using the Command Line Interface

1. Add the `tap-slack` extractor to your project using [`meltano add`](https://docs.meltano.com/command-line-interface.html#add):

    ```bash
    meltano add extractor tap-slack
    ```

1. Configure the [settings](#settings) below using [`meltano config`](https://docs.meltano.com/command-line-interface.html#config).

#### Using Meltano UI

1. Start [Meltano UI](https://docs.meltano.com/ui.html) using [`meltano ui`](https://docs.meltano.com/command-line-interface.html#ui):

    ```bash
    meltano ui
    ```

1. Open the Extractors interface at <http://localhost:5000/extractors>.
1. Click the "Add to project" button for "Slack".
1. Configure the [settings](#settings) below in the "Configuration" interface that opens automatically.

### Next steps

Follow the remaining steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Select entities and attributes to extract](https://docs.meltano.com/getting-started.html#select-entities-and-attributes-to-extract)
1. [Add a loader to send data to a destination](https://docs.meltano.com/getting-started.html#add-a-loader-to-send-data-to-a-destination)
1. [Run a data integration (EL) pipeline](https://docs.meltano.com/getting-started.html#run-a-data-integration-el-pipeline)

If you run into any issues, chat with us in [#troubleshooting](https://meltano.slack.com/archives/C01TCRBBJD7) on [Slack](https://meltano.com/slack).

## Settings

`tap-slack` requires the [configuration](https://docs.meltano.com/configuration.html) of the following setting:

- [API Token](#api-token)

This and other supported settings are documented below.
To quickly find the setting you're looking for, use the Table of Contents in the sidebar.

#### Minimal configuration

A minimal configuration of `tap-slack` in your [`meltano.yml` project file](https://docs.meltano.com/concepts/project#meltano-yml-project-file) will look like this:

```yml
plugins:
  extractors:
  - name: tap-slack
    variant: mashey
      start_date: '2020-10-01T00:00:00Z'
```

Sensitive values are most appropriately stored in [the environment](https://docs.meltano.com/configuration.html#configuring-settings) or your project's [`.env` file](https://docs.meltano.com/concepts/project#env):

```bash
export TAP_SLACK_TOKEN=my_api_token
```

### API Token

- Name: `token`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_SLACK_TOKEN`

Your Slack API Token. To obtain a token for a single workspace you will need to create a [Slack App](https://api.slack.com/apps?new_app=1) in your workspace and assigning it the relevant scopes. The minimum required scopes for the tap are:

* `channels:history`
* `channels:join`
* `channels:read`
* `files:read`
* `groups:read`
* `links:read`
* `reactions:read`
* `remote_files:read`
* `remote_files:write`
* `team:read`
* `usergroups:read`
* `users.profile:read`
* `users:read`

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-slack set token <token>

export TAP_SLACK_TOKEN=<token>
```

### Channels

- Name: `channels`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_SLACK_CHANNELS`

Optionally specify specific channels to sync. By default the tap will sync all channels it has been invited to, but this can be overriden using this configuration. Note that the values need to be channel ID, not the name, as [recommended by the Slack API](https://api.slack.com/types/conversation#other_attributes). To get the ID for a channel, either use the Slack API or find it in the [URL](https://www.wikihow.com/Find-a-Channel-ID-on-Slack-on-PC-or-Mac).

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-slack set channels '["<channelid>", ...]'

export TAP_SLACK_CHANNELS='["<channelid>", ...]'
```

### Private Channels

- Name: `private_channels`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_SLACK_PRIVATE_CHANNELS`
- Default: `true`

Specifies whether to sync private channels or not. Default is true.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-slack set private_channels false

export TAP_SLACK_PRIVATE_CHANNELS=false
```

### Public Channels

- Name: `join_public_channels`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_SLACK_JOIN_PUBLIC_CHANNELS`
- Default: `false`

Specifies whether to have the tap auto-join all public channels in your ogranziation. Default is false.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-slack set join_public_channels true

export TAP_SLACK_JOIN_PUBLIC_CHANNELS=true
```

### Archived Channels

- Name: `archived_channels`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_SLACK_ARCHIVED_CHANNELS`
- Default: `false`

Specifies whether the tap will sync archived channels or not. Note that a bot cannot join an archived channel, so unless the bot was added to the channel prior to it being archived it will not be able to sync the data from that channel. Default is false.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-slack set archived_channels true

export TAP_SLACK_ARCHIVED_CHANNELS=true
```

### Date Window Size

- Name: `date_window_size`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_SLACK_DATE_WINDOW_SIZE`
- Default: `7`

Specifies the window size for syncing certain streams (messages, files, threads). The default is 7 days.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-slack set date_window_size <integer>

export TAP_SLACK_DATE_WINDOW_SIZE=<integer>
```

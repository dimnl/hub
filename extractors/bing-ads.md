---
title: Bing Ads
layout: plugin_page
description: Use Meltano to pull data from the Bing Ads API and load it into Snowflake, PostgreSQL, and more
---

The `tap-bing-ads` [extractor](https://meltano.com/plugins/extractors/) pulls data from the [Bing Ads API](https://docs.microsoft.com/en-us/advertising/guides/).

- **Repository**: <https://github.com/singer-io/tap-bing-ads>
- **Maintainer**: [Stitch](https://www.stitchdata.com/)
- **Maintenance status**: Unresponsive to community issues and contributions
  - A [more active fork](https://github.com/singer-io/tap-bing-ads/network) may be available that you can [use instead](https://docs.meltano.com/plugin-management.html#using-a-custom-fork-of-a-plugin).
  - This plugin is [up for adoption](https://docs.meltano.com/contributor-guide.html#adopting-a-plugin)!

## Getting Started

### Prerequisites

If you haven't already, follow the initial steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Install Meltano](https://docs.meltano.com/getting-started.html#install-meltano)
1. [Create your Meltano project](https://docs.meltano.com/getting-started.html#create-your-meltano-project)

### Installation and configuration

#### Using the Command Line Interface

1. Add the `tap-bing-ads` extractor to your project using [`meltano add`](https://docs.meltano.com/command-line-interface.html#add):

    ```bash
    meltano add extractor tap-bing-ads
    ```

1. Configure the [settings](#settings) below using [`meltano config`](https://docs.meltano.com/command-line-interface.html#config).

#### Using Meltano UI

1. Start [Meltano UI](https://docs.meltano.com/ui.html) using [`meltano ui`](https://docs.meltano.com/command-line-interface.html#ui):

    ```bash
    meltano ui
    ```

1. Open the Extractors interface at <http://localhost:5000/extractors>.
1. Click the "Add to project" button for "Bing Ads".
1. Configure the [settings](#settings) below in the "Configuration" interface that opens automatically.

### Next steps

Follow the remaining steps of the [Getting Started guide](https://docs.meltano.com/getting-started.html):

1. [Select entities and attributes to extract](https://docs.meltano.com/getting-started.html#select-entities-and-attributes-to-extract)
1. [Add a loader to send data to a destination](https://docs.meltano.com/getting-started.html#add-a-loader-to-send-data-to-a-destination)
1. [Run a data integration (EL) pipeline](https://docs.meltano.com/getting-started.html#run-a-data-integration-el-pipeline)

If you run into any issues, chat with us in [#troubleshooting](https://meltano.slack.com/archives/C01TCRBBJD7) on [Slack](https://meltano.com/slack).

## Settings

`tap-bing-ads` requires the [configuration](https://docs.meltano.com/configuration.html) of the following settings:

- [Developer Token](#developer-token)
- [OAuth Client ID](#oauth-client-id)
- [OAuth Client Secret](#oauth-client-secret)
- [Refresh Token](#refresh-token)
- [Customer ID](#customer-id)
- [Account IDs](#account-ids)
- [Start Date](#start-date)
- [Require Live Connect](#require-live-connect)

#### Minimal configuration

A minimal configuration of `tap-bing-ads` in your [`meltano.yml` project file](https://docs.meltano.com/concepts/project#meltano-yml-project-file) will look like this:

```yml{5-8}
plugins:
  extractors:
  - name: tap-bing-ads
    variant: singer-io
    config:
      customer_id: 163875182
      account_ids: 163078754
      start_date: '2020-10-01T00:00:00Z'
```

Sensitive values are most appropriately stored in [the environment](https://docs.meltano.com/configuration.html#configuring-settings) or your project's [`.env` file](https://docs.meltano.com/concepts/project#env):

```bash
export OAUTH_BING_ADS_DEVELOPER_TOKEN=my_developer_token
export OAUTH_BING_ADS_CLIENT_ID=my_client_id
export OAUTH_BING_ADS_CLIENT_SECRET=my_client_secret
export TAP_BING_ADS_REFRESH_TOKEN=my_refresh_token
```

### Developer Token

- Name: `developer_token`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `OAUTH_BING_ADS_DEVELOPER_TOKEN`

See <https://docs.microsoft.com/en-us/advertising/guides/get-started#get-developer-token>.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set developer_token <token>

export OAUTH_BING_ADS_DEVELOPER_TOKEN=<token>
```

### OAuth Client ID

- Name: `oauth_client_id`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `OAUTH_BING_ADS_CLIENT_ID`

See <https://docs.microsoft.com/en-us/advertising/guides/get-started#quick-start-production>.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set oauth_client_id <id>

export OAUTH_BING_ADS_CLIENT_ID=<id>
```

### OAuth Client Secret

- Name: `oauth_client_secret`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `OAUTH_BING_ADS_CLIENT_SECRET`

See <https://docs.microsoft.com/en-us/advertising/guides/get-started#quick-start-production>.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set oauth_client_secret <secret>

export OAUTH_BING_ADS_CLIENT_SECRET=<secret>
```

### Refresh Token

- Name: `refresh_token`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_BING_ADS_REFRESH_TOKEN`

See <https://docs.microsoft.com/en-us/advertising/guides/get-started#quick-start-production>.
If you're using a Refresh Token you should not need a redirect URI in the request.
Note that you'll need to include the OAuth Scopes when requesting the token.
The recommended scopes are `scope=openid%20profile%20https://ads.microsoft.com/ads.manage%20offline_access`.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set refresh_token <token>

export TAP_BING_ADS_REFRESH_TOKEN=<token>
```

### Customer ID

- Name: `customer_id`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_BING_ADS_CUSTOMER_ID`

See <https://docs.microsoft.com/en-us/advertising/guides/get-started#get-ids>.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set customer_id <id>

export TAP_BING_ADS_CUSTOMER_ID=<id>
```

### Account IDs

- Name: `account_ids`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_BING_ADS_ACCOUNT_IDS`

See <https://docs.microsoft.com/en-us/advertising/guides/get-started#get-ids>.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set account_ids <id>

export TAP_BING_ADS_ACCOUNT_IDS=<id>
```

### Require Live Connect

- Name: `require_live_connect`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_BING_REQUIRE_LIVE_CONNECT`
- Default: 'True'

Note that the default is not a boolean, but a string set to 'True'. Setting the configuration to a boolean `false` will work to disable this setting.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set require_live_connect false

export TAP_BING_REQUIRE_LIVE_CONNECT=false
```

### Start Date

- Name: `start_date`
- [Environment variable](https://docs.meltano.com/configuration.html#configuring-settings): `TAP_BING_ADS_START_DATE`

This property determines how much historical data will be extracted.

Please be aware that the larger the time period and amount of data, the longer the initial extraction can be expected to take.

#### How to use

Manage this setting using [Meltano UI](#using-meltano-ui), [`meltano config`](https://docs.meltano.com/command-line-interface.html#config), or an [environment variable](https://docs.meltano.com/configuration.html#configuring-settings):

```bash
meltano config tap-bing-ads set start_date YYYY-MM-DDTHH:MM:SSZ

export TAP_BING_ADS_START_DATE=YYYY-MM-DDTHH:MM:SSZ

# For example:
meltano config tap-bing-ads set start_date 2020-10-01T00:00:00Z

export TAP_BING_ADS_START_DATE=2020-10-01T00:00:00Z
```

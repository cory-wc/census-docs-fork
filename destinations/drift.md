---
description: This page describes how to use Census with Drift.
---

# Drift

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Drift to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Drift account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Connect Census to Drift

In the **Connections** page in Census, click the **Add Service** button under the **Service Connections** section, and select Drift.

You will be redirected to a page to log in to Drift to authorize your account to Census. You will be prompted to enter your email and then your password. Once you click the **Sign In** button, you'll see a page like the image below, confirming you want to authorize Census.

![](../.gitbook/assets/screen-shot-2021-04-22-at-4.02.13-pm.png)

Once you've authorized Census, you'll be redirected back to the **Connections** page in Census and you should see your Drift connection there.

If you want to see your integrations in Drift in the future, simply navigate to the **Settings** page, and click on **Integrations** in the left side navigation \(close to the bottom, right above **Help**\).

## 🗄 Supported Objects

| **Object Name** | **Supported?** | Identifiers |
| ---: | :---: | :--- |
| Contact | ✅ | Object ID, any Text/Number |

[Contact us](mailto:support@getcensus.com) if you want Census to support more supported objects for Drift.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | All |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Drift.

## 🚑 Need help connecting to Drift?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


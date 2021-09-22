---
description: This page describes how to use Census with Outreach.
---

---
description: Learn how to use Census with Outreach.
---

# Outreach

## 🏃‍♂️ Getting Started

This guide shows you how to use Census to connect your Outreach account to your data warehouse and create your first sync.

### **Prerequisites**

Before you begin, you'll need the following:

* Census account: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* Outreach account: {Add details on what type of access is needed and link to Required Permissions section below.}
* Credentials for your data warehouse: For details, see the guide for your specific technology.
  * [Redshift](../source-warehouse/redshift.md)
  * [Snowflake](../source-warehouse/snowflake.md)
  * [Google BigQuery](../source-warehouse/google-bigquery.md)
  * [Databricks](../source-warehouse/databricks.md)
  * [Postgres](../source-warehouse/postgres.md)

### Step 1: Connect Outreach

1. Log into Census and navigate to [Connections](https://app.getcensus.com/connections).
2. Click **Add Service**.
3. Select **Outreach** from the dropdown list.
4. Follow the Outreach authentication flow.

Your end state should look something like this. 👇

![{SCREEN}]({image%20URL})

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

After connecting your warehouse, your **Connections** page will look something like this: 👇

![{SCREEN}]({image%20URL})

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Outreach. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the [**Models**](https://app.getcensus.com/models) page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save**.

![{SCREEN}](image%20URL)

### Step 4: Create your first sync

The sync will move data from your warehouse to Outreach. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Outreach as the **Connection** and an **Object** in Outreach. \(See [Supported Objects](./#supported-objects).\)
4. Under **How should changes to the source be synced?**, choose **Update or Create**. \(See [Supported Sync Behaviors](./#supported-sync-behaviors).\)
5. Under **How are source and destination records matched?**, select a mapping key. We recommend using an internal ID when possible. \(See [Supported Objects](./#supported-objects) for details.\)
6. Under **Which fields should be updated?**, select the fields you want to update by mapping a field in Outreach to a column in your model.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![{SCREEN}]({image%20URL})

### Step 5: Confirm the synced data in Outreach

Once your sync is complete, it's time to check your data. Open Outreach and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Outreach! 🎉

And if anything went wrong, [contact the Census support team](mailto:support@getcensus.com) to get some help.

### 🏎 Sync Speed

Sync speeds can be affected by API rate limiting from the destination app. Outreach allows an API call rate of up to 10,000 calls per hour, per user. \(See [Outreach API Documentation](https://api.outreach.io/api/v2/docs) for details.\)

In most cases, you won't run into any issue with sync speed based on rate limiting unless:

* You're running an initial sync action that will update many records in Outreach.
* You have another integration or service that's making API calls to Outreach and using the same user account.

### 🗄 Supported Objects

| **Object Name** | **Supported** | **Identifiers** |
| ---: | :---: | :--- |
| Account | ✅  | any Text field |
| Prospect | ✅ | Email \(recommended\), any Text field |
| User | ✅ | Email \(recommended\), any Text field |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Outreach.

### 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](../basics/core-concept#sync-behaviors).
{% endhint %}

| **Behavior** | **Supported** | **Objects** |
| ---: | :---: | :--- |
| Update or Create | ✅ | All |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Outreach.

### 🔑 Required Permissions

{CWC: Add details here. What type of Outreach account settings are needed? Based on their UI, I suspect you need an account with the Admin profile.}

### 🚑 Need Help Connecting to Outreach?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

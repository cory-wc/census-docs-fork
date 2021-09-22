---
description: This page describes how to use Census with Airtable.
---

# Airtable

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Airtable to Census and create your first sync.

{% embed url="https://www.youtube.com/watch?v=-NRDgN65rrg" caption="" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Airtable account ready, with write access to your target Airtable base.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Create or get the Airtable API key

1. From within Airtable, click the profile icon in the top right and select **Account**. Or click [_here_](https://airtable.com/account)_._  ![](../.gitbook/assets/screely-1629998696109.png) 
2. Scroll to the **API** section. If this is your first time using the API, you'll need to create an API key. Once created, click the box and copy the API key. You'll need that in a minute.   ![](../.gitbook/assets/screely-1629998745164.png) 

Note: Census's permissions will be the same as this Airtable user. If you think this Airtable user's permissions may change or the account is removed, you may want to create a special Airtable account just for Census to use.

### 2. Add an Airtable Connection

1. Now back to Census! Navigate to the [Connections page](https://app.getcensus.com/connections).
2. Click the **Add Service** button.
3. Select **Airtable** from the list. ![](../.gitbook/assets/screely-1629998477683.png) 
4. Add your API key to the modal and give your connection a memorable name. Save once you've got both! ![](../.gitbook/assets/screely-1629999170323.png) 

### 3. Connect your data warehouse

If you don't already have a data warehouse connected, follow one of our short guides depending on your data warehouse service:

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)
* [Databricks](../sources/databricks.md)

You should now have a connection to Airtable and to your data warehouse! Let's start syncing data.

### 4. Create your first Model <a id="3-create-your-first-model"></a>

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models).​‌

Here you will have to write SQL queries to select the data you want to see in Airtable. Here are some ideas of data you should select‌.

* Orders that to fulfill
* Expenses to review
* Customer feature requests to prioritize

Once you have created your model, click **Save**.‌

### 5. Create your first Sync <a id="4-create-your-first-sync"></a>

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button‌.

In the " **What data do you want to sync?"** section‌

* For the **Connection**, select the data warehouse you connected in step 3
* For the **Source,** select the model you created in step 4

Next up is the **"Where do you want to sync data to?"** section‌

* Pick the name of Airtable from step 2 as **the Connection**
* For Object, pick the table you want to sync data to

For the " **How should changes to the source be synced?"** section‌

* Select your preferred behavior. **Update only** is a great place to start if you have data in Airtable! **Update or Create** is great for sending data from the warehouse into Airtable.
* Pick the right mapping key, Airtable only allows a text type from their tables. We recommend you use your own unique id from the database if possible.

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section‌.

* Here simply map the field from your Airtable instance to the column from your model.

The end result should look something like this​:

![](../.gitbook/assets/screen-shot-2021-08-27-at-11.34.46-am.png)

![](../.gitbook/assets/screen-shot-2021-08-27-at-11.34.57-am%20%281%29.png)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync‌.

### 6. Confirm the data is in Airtable <a id="5-confirm-the-data-is-in-intercom"></a>

Now go back to your Airtable and go view the table object that should have been updated. If everything went well, you should see your data in the table​

That's it! In 6 steps, you've connected Airtable and started syncing orders data from your warehouse 🎉

## 🗄 Supported Objects

Airtable support is pretty straight forward!

| **Object Name** | **Supported?** |
| ---: | :---: |
| Table | ✅ |

{% hint style="info" %}
Airtable needs a primary key that is a short text field for Census to be able to join from a source table. On the SQL side, it can be a numeric type, but this is a quirk of this integration that's worth calling out.
{% endhint %}

**Column types**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Airtable Field Types</th>
      <th style="text-align:left">Source SQL Types</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Short Text</td>
      <td style="text-align:left">
        <p>String</p>
        <p>Numeric</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Single Select</td>
      <td style="text-align:left">
        <p>String</p>
        <p>Numeric</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Checkbox</td>
      <td style="text-align:left">
        <p>Boolean</p>
        <p>Numeric (nonzero = checked, 0 = unchecked)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">The Rest</td>
      <td style="text-align:left">
        <p>Census will give an informative error</p>
        <p>message if rejected by Airtable &#x1F600;</p>
      </td>
    </tr>
  </tbody>
</table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Airtable.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | All |
| **Update Only** | ✅ | All |
| **Mirror** | 🔜 | All |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Airtable.

## 🚑 Need help connecting to Airtable?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


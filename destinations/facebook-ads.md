---
description: >-
  This page describes how to use Census with Facebook Ads (Audiences and
  Conversions).
---

# Facebook Ads

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Facebook Ads to Census and create your first sync.

{% embed url="https://www.youtube.com/watch?v=0\_jr7dv-FWE" caption="" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Facebook Ads account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

## Audiences

### 1. Collect the Facebook Audience ID

The first step is finding the audience you'd like to sync data into. You can do that by visiting the [Audiences section of Facebook's Ads Manager](https://business.facebook.com/adsmanager/audiences). Make a note of the ID \(name will work too\) of the audience you want to sync to from Census.

If you'd like to use a new Facebook Audience with Census, go ahead and create it now. Facebook Audiences makes it a bit confusing to create a new empty audience for Census. You'll need to create a new Customer List Custom Audience and then upload a CSV with the columns that you'll be using.

### 2. Create a SQL Model from your source data

The results of the View, Table, or Census Model should contain a row per user. Each row will have three or more columns:

1. A unique identifier for the user, Facebook calls this the External ID. This is usually a unique ID from your application database, but could be email as well if that also uniquely identifies each row. 
2. A column indicating what Facebook Audience the user should be synced to \(can be the audience name or audience ID\).
3. Any other identifying fields that Facebook can use to match your audience. Facebook requires these fields to be formatted in a certain way. For example, email must be lower-case. You can read more about each of the formatting requirements in the[ Facebook Documentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#hash).

Example Facebook Audience Model:

```sql
SELECT
    user_id, 
    LOWER(email_address) AS email, 
    'active users audience' AS fb_audience
FROM user_activity_table;
```

### 3. Create a sync

Now that your data is prepared and in the correct format, we're ready to start syncing users to Facebook.

#### **A. Select your model from above as a data source and Facebook Audiences as a destination.**

![](../.gitbook/assets/fb_setup1.png)

#### **B. Choose the appropriate sync behavior**

Update or Create will add or update users to the audience, but will never remove users. Mirror will also remove users that have disappeared from the source. Note: If you're reusing an existing Facebook Audience, Census will not remove any users already added to that audience through other means. Census only removes users that it created initially.

![](../.gitbook/assets/fb_setup2.png)

#### **C. Select an external identifier to match rows uniquely in Facebook**

This should be the user id or other external ID you selected when you created the model.

![](../.gitbook/assets/fb_setup3.png)

#### **D. Associate users with the Audience**

Let Census know which column should be used to assign users to their audience. Select the Audience's ID or Name to correspond to the type of identifier you're providing with your model.

![](../.gitbook/assets/fb_setup4.png)

#### **E. Map the remaining identifying fields**

You can then map any user identifying fields that are present in your source data \(e.g. phone number, email, first name, last name, etc\).

## Conversions

Send web events directly to Facebook from your warehouse, exactly as if they were pixel events using the Facebook Conversions API.

### 1. Choose or create a conversion event in Facebook, Collect the Pixel ID

To view all your Facebook Ads accounts' Pixel IDs go to the [Events Manager](https://www.facebook.com/business/help/898185560232180): [https://business.facebook.com/events\_manager2/list/](https://business.facebook.com/events_manager2/list/).

Be sure to select the specific ads account you want to work on. You can switch ad accounts in the navigation bar on the left side of the screen.

In the events manager, you can view all your ad account's pixels and view or create conversion events.

### 2. Create a sync

In your SQL model, dbt model, or table -- ensure that you have all required fields for your conversion sync, and any user identifiers so that Facebook can perform ad attribution. Facebook Conversion syncs require the following fields:

#### A. Event ID

Census requires the model to have a column that stores a unique identifier for each row so that Census never sends any duplicate records. We'll call this unique identifier column "Event ID". If you have an identifier that you are already passing via your pixel on the website for online versions of this conversion event, use this identifier. Some common examples include `user_id`, `lead_id`, and `order_id`.

#### B. Minimum Event Parameters

The Facebook Conversions API requires 4 fields for every event:

* Pixel ID - see above to find.
* [Action Source](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#action-source) - This field allows you to specify where your conversions occurred. It accepts one of the following values: "email", "website", "phone\_call", "chat", "physical\_store",  "system\_generated", and "other".
* [Event Name](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#event-name) - A Facebook pixel [Standard Event](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking#standard-events) or [Custom Event](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking#custom-events) name.
* [Event Time](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#event-time) - can be up to 7 days before you send an event to Facebook. This date must be sent in GMT timezone.

#### C. Customer Information Parameters

Facebook attributes conversions back to ad campaigns by identifying the users that saw or interacted with ad content. To do so, they accept the following user identifiers and will attempt to match each conversion to a facebook user. **Sending more identifiers will improve match rates**.

For a more complete description of each identifier, please see [Facebook's API documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters). When Facebook requires a field's value to be hashed, you may choose to use a pre-hashed value \(if you have one\), or for Census to perform the hashing for you.

* Email
* Phone
* Gender
* Date of Birth
* Last Name
* First Name
* City
* State
* Zip
* Country
* External ID
* Client IP address
* Client user agent
* Click ID
* Browser ID
* Subscription ID
* Facebook Login ID
* Lead ID

#### Putting it all together...

Your final sync configuration will look like the following!

![](../.gitbook/assets/screely-1626208532062%20%281%29.png)

## 🗄 Supported Objects

| **Object Name** | **Supported?** | Identifiers |
| ---: | :---: | :--- |
| Customer | ✅ | [External ID](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/external-id/) |
| Conversions | ✅ | Any unique ID |
| Product Catalog | 🔜 |  |

Please [contact us](mailto:support@getcensus.com) if there are additional Facebook Ads objects you'd like us to support.

#### Data Normalization

Facebook Audiences and Conversions are a bit unique from other services. We do not upload the data you provide directly. Instead, it's "matched" to Facebook's audience. To do this, both sides "hash" their data so users can be compared without revealing the actual personally identifiable information.

Census automatically takes care of this hashing step for you.

**However, all values provided to Census must be lowercase**. You can use this standard SQL function `LOWER()`that works across all data warehouses.

## 🔄 Supported Sync Behaviors

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | Audiences |
| **Mirror** | ✅ | Audiences |
| **Append** | ✅ | Conversions |

Update or Create will add or update users to the audience, but will never remove users. Mirror will also remove users that have been removed from the source.

Note: If you're reusing an existing Facebook Audience, Census will not remove any users already added to that audience through other means. Census only removes users that it created initially.

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

## 🚑 Need help connecting to Facebook?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


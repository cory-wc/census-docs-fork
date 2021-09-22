---
description: Maintain audience lists in Google Ads to retarget and re-engage your users.
---

# Customer Match Lists \(Audiences\)

## Connect your Google Ads Account

Follow the [set-up instructions here!](https://docs.getcensus.com/destinations/google-ads)

## Sync a Customer Match List with Census

### 1. Create your Google Ads Customer Match Model <a id="3-create-your-first-model"></a>

Navigate to the [Models](https://app.getcensus.com/models) page.​

Here you can write SQL queries or select dbt models that contain the data you want to send to Google Ads.

Right now, we're going to send data to an existing Customer Match list, which requires a specific set of properties. We'll create a model that has:

* The email of the Customer
* A list of the target Customer Match lists
* Any other properties about the Customer that can assist in the match.

Once you have created your model, click save.

### 2. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the " **What data do you want to sync?"** section

* For the **Connection**, select the data warehouse you connected in the Prerequisites Step 2
* For the **Source,** select the model you created in step 1 of this section

Next up is the **"Where do you want to sync data to?"** section

* Pick **Google Ads** as the Connection
* For Object, pick **Customer**

For the " **How should changes to the source be synced?"** section

* **Update or Create** will be selected by default
* Pick the right mapping key, in this case, we'll use **Email**

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section. Here simply map the field from your model to the properties of the Customer Match List.

The end result should look something like this

![](../../.gitbook/assets/screely-1619138106154.png)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync.

### 3. Confirm the data is in your Customer Match List

Now go back to your Google Ads account and view the list. If everything went well, you should see that the list has been updated with your data. Because this is an Audience Matching mechanism, Google will not tell you the exact number of matches it found, but should tell you that it was updated.

![](../../.gitbook/assets/screely-1619138538677.png)

That's it! In 3 steps, you connected your data warehouse to Google Ads and built live Customer Match audiences Google Ads 🎉

## **Best Practices and Notes**

Google Customer Match, as its name implies, is a matching service rather than the usual direct upload. In order to protect user data, we do not upload the data you provide directly. Instead, records are "matched" against Google's existing user base. To do this, both sides perform a "hash" -- or consistent, but irreversible conversion -- of data so users can be compared without revealing the actual personally identifiable information. Census automatically takes care of this hashing step for you.

We recommend you do not use Google's Customer Match expiration setting. Census-synced records are subject to the same expiration and will not be re-uploaded unless they are changed in your source data.

## 🔄 Supported Sync Behaviors

| **Behaviors** | **Supported?** |
| ---: | :---: |
| **Update or Create** | ✅ |
| **Mirror** | ✅ |

_**Identifiers**: User ID, Mobile ID, Email, Phone Number_

[Contact us](mailto:support@getcensus.com) if you're looking for additional Sync Behaviors!

Note: If you're reusing an existing Customer Match List, Census will not remove any users already added to those lists through other means.

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}


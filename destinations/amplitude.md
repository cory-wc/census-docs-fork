---
description: This page describes how to use Census with Amplitude.
---

# Amplitude

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Amplitude to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Amplitude account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### **1. Get API key from Amplitude**

Census needs only one piece of information to connect to your Amplitude project:

* The API Key for an HTTP API data source for your Amplitude project

### **2. Create a HTTP API Data Source in Amplitude, and copy the API key**

Amplitude lets you pull data from a number of different sources, including via HTTP API. If you don't have this data source set up in Amplitude already, you'll need to create one. The same steps below will also allow you to find the API key for a pre-existing HTTP API data source, as Amplitude will only permit one per project.

1. Within Amplitude’s left navigation bar, scroll down to the very bottom. **Click on Sources & Destinations.**  

![](https://lh6.googleusercontent.com/IldQDvHh30Q3BQTJI1tAjTdnYaoLgkALhEYU9wpXfMAbmPe0Qu8eUavNYVzRNGT3Chjpr_G-SODK6pRQluXA44WkdKpjUESz8lItwWdkWUVGE60gJfLHJdFrnEd8lJwdiD_nvvph)

1. ‌Once here, navigate to the top-right of the screen and click to **Add Data Source**. _\*\*_![](https://lh3.googleusercontent.com/Xt-bGTekukUBgNGE-d805HzLvnODAgkuC7JCO_uiW_3gpE7-oFBID3fgEjkHfRkdlyXtEGG_wubzXWH8EBss8sJ-Ce_i9CGAnD5oy-L9F1rvn9YyQlcsxzY4ms5K8guaGWru4MlL)
2. Select **“HTTP API”** as the type of data source, and click **Next**.![](https://lh6.googleusercontent.com/3oT5uRNYeOJCVX6v9h7I4zwmp0P6z2H0NTocMnaOTwauCi01GFLjVZNYdjoYLK_AxvmMVIxK-Ec8o9xDZGExO9YYlh-T2i055heRbi-VWU5B-0MsR1bDXwfOEaIkAmIr5jIokemj)
3. **Copy the API Key** \(it will be a long string of numbers and characters\), click **Next.** 
4. If you are setting up the HTTP API data source for the first time, Amplitude will require you to POST an event to their API to complete set-up. Amplitude provides instructions to send a sample event and complete set-up at this stage.
5. When the event is received by Amplitude, click **Finish** to finish setting up this source within Amplitude.

### 3. **Create the Census Connection**

Now that we have the API Key from Amplitude, we can now set up Amplitude as a Destination in Census.

1. In the **Settings** tab of Census, create a new Amplitude Service Connection. _\*\*_![](https://lh5.googleusercontent.com/TYNs2uji9P65wu4JR-3bU3k_0svIJ7dAdaS9I25gzHHY0U-kxlQ6twBRFPIwrUzsNGOnamNJT-8ygYqnyPsuGW51k2EGWhghMJGpur6Ewde5Rw5xaoevAyr6_CkUSZ_OiY-58b7D)
2. You can provide whatever name you like.
3. Provide the copied API Key from Amplitude.
4. Save.

### 4. Create your first Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you will have to write SQL queries to select the data you want to see in Amplitude. Here are some ideas of data you should select

* The Lifetime Value of a customer
* The end date of a user's trial
* The date a user became active in your product
* The number of key activities a user did in your app in the last 7/30 days

Once you have created your model, click save.

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f6563834cedfd00173b9a49/file-zg53SxxpoO.png)

### 5. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the Add Sync button

In the "What data do you want to sync?" section.

* For the Connection, select the data warehouse you've already connected \(See Prerequisites\).
* For the Source, select the model you created in step 4.

Next up is the "Where do you want to sync data to?" section.

* Pick the Amplitude connection you created in step 3.
* For Object, Select Device or User. If Devices can be associated with Users, then select Device. If no Device information is collected, select User.

For the "How should changes to the source be synced?" section.

* Select Update Or Create
* Pick the right mapping key; Amplitude only supports Distinct ID.

Finally, select the fields you want to update in the Mapper in the "Which Fields should be updated?" section. Here simply map the field from your Amplitude instance to the column from your model.

![](../.gitbook/assets/screenshot-2021-04-23-at-1.17.38-pm.png)

Click the Next button to see the final preview, which will have a recap of what will happen when you start the sync.

## 🗄️ Supported Objects

| Object Name | Supported? | Identifiers |
| :--- | :---: | :--- |
| Devices | ✅ | Device ID |
| Users | ✅ | User ID |
| Groups | ✅ | Group Value |
| Events | ✅ | Insert ID |

Both User and Device objects will resolve to a single User Profile in Amplitude. If Devices can be associated with Users, then select Device and map the User field to an appropriate value in your model. If no Device information is collected, select User.

🎒 [Contact us](mailto:support@getcensus.com) if you want Census to support more Objects for this destination

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | Device, User, Group |
| **Create Only** | ✅ | Event |

‌ 🔋 [Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination

‌

## 🚑 Need help connecting to Amplitude?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


# Core Concepts

## 🔌 Sources and Destinations

Census at its core is about connecting and coordinating across your business's software stack. And so, one of the very first steps to using Census will be connecting your Data Warehouse Sources and Destination Services.

### Data Warehouse Sources

Source data for all Census Syncs come from your Data Warehouse. Historically, a data warehouse was the end of the line, where data went to collect dust. But modern cloud data warehouses enable a huge variety of data sources and data size, as well as the flexibility to define how data should be aggregated, joined, and organized specifically for your business. It's this flexibility and scalability that make it the perfect data hub for your operations.

Census can use anything you grant access to in your data warehouse as a sync source, whether that is a table, a view, a SQL query, or a dbt model. We'll cover the process of building models in the next section.

{% hint style="info" %}
For more details on connecting your data warehouse, take a look at the Data Sources section on the left.
{% endhint %}

### Destination Services

Census helps you keep your data in sync across all the business apps you use to engage with your customers, from advertising and marketing, through sales, all the way to finance. The goal is to keep all of those apps in sync, powered by the exact same set of data.

The process of connecting a service is a little different for each. Sometimes, it's as simple as an OAuth confirmation flow or a straightforward API key. Other times, a few more steps are required.

Once you've connected a source, we'll be able to access a set of objects that service makes available. Typically this is a Contact or a Company, but there are often others and in some cases, even custom defined objects are supported.

All of the connection steps, the objects, and other details for each service are covered here in the docs.

And don't forget, our library of connections grows every week! Keep an eye on our [integrations page](https://www.getcensus.com/integrations) for all of our available destinations and let us know if we're missing something you need!

## 🪚 Building Models

At Census, we call individual data source sets Models. Models usually represent a single type of "thing" like a person \(or a lead or a contact\) or a company \(or an account or organization\). They can also be other things like invoices, campaigns, events, or devices.

A model is usually a list or a set of those things. It can be the full set of every person you know or it can be be a subset \(often called a list or segment\).

Models can come in a variety of forms:

* Tables or Views already in your data warehouse – This is the most common. If you've a data warehouse at your company, chances are, you've already built some tables that act as your models.
* Models built with data transform tools like [dbt](https://www.getdbt.com/). – We're big fans of dbt here at Census. It's why we have a built in [dbt integration](native-dbt-integration.md). These tools make it easy to build and maintain sophisticated data transforms that keep your models up to date.
* SQL queries – Yes, even a SQL query can work as a model. It's a handy way to start when you're just getting going. Just plan to eventually evolve to data transform tools like dbt as you create more models!

A model is a table in a data warehouse that looks an awful lot like a spreadsheet. The rows are individual records of that model, and all rows have the same set of columns. Typically, if you look at the columns, you'll have one or two unique identifier columns, and then a bunch of details for each of the records, things like name, last event date, or number of actions they took.

The actual set of properties/columns your model have can be anything. The only important thing is that they're the properties that matter to you and your business. The benefit of building models is that you can define them one time, The Right Way™ and then use that as the authoritative source for all of your apps.

## 🧮 Creating Syncs

The most important action in Census is defining Syncs. A Sync defines the rules of how data should be synced, from your selected source to your destination.

Syncs are also what makes Census so unique. Unlike most integration tools that are event-based, Census works to keep your source and destination "in sync" \(just like Dropbox or other cloud storage service\). The benefit is that you don't have to worry about dropped events or backfills anymore. If you change your data in the model, Census just syncs it, easy as that!

### 🔀 Sync Behaviors

{% hint style="success" %}
All of our syncs are incremental, which means we only sync records that are new or have their data changed since the previous sync.
{% endhint %}

Sync Behaviors tell Census the types of change it should apply to your data when a sync finds a matching \(or not\) record in a source and a destination. We support a few different sync behaviors:

|  |  |
| :--- | :--- |
| Update or Create \(aka Upsert\) | Update existing destination records when IDs match, otherwise create new ones if they're missing. |
| Update Only | Update existing objects in the destination, don't create any new ones. |
| Create Only | Create a new object if it doesn't exist in the destination. |
| Mirror | Keep the destination in sync with the source. If a row is added or edited, update the destination. If a row is deleted, remove the matching object from the destination. |
| Append Only | Append every new record in the source to the destination. This is unique to Customer.io, Mixpanel and other destinations that have the concept of Events. |
| Delete | ⚠️Here be dragons! Delete syncs takes the list of provided IDs and deletes them from the destination. Be careful! Providing an incorrect set of IDs can result in data loss! Census recommends you backup data if you're concerned about accidentally deleting the wrong records. |

{% hint style="warning" %}
Please note that some of these behaviors are only available for certain destinations. Visit our individual integration pages to view what's supported.
{% endhint %}

### 🔎 Matching Identifiers

Matching Identifiers let Census know how to associate data in the source with the destination. Both the source and destination need to provide a single, unique per record, identifying field. Census uses the identifiers to look for matches. When a match is found, or not found, it then can use your selected Sync Behavior to decide what to do.

For example, if Census sees your source and destination both have records with the identifier ABCD1234, it knows that it should update that record with data from the source when you've got an Update Only, Update or Create, or Mirror Sync Behavior configured.

### 🖇 Field Mappings

Once you've defined _how_ data is related between your source and destination, the next step is to let Census know _what_ properties should be updated. The field mapping step lets you specify how fields should be mapped from your source model to the destination object's fields. You can automatically add all matching fields, but even if names don't match, you can also provide the matching manually.

#### Creating new fields on your destination object

For some destinations, such as Customer.io, Iterable, or Klaviyo, you can create new fields directly from the Census app. This means the next time a sync runs, Census will create new properties or attributes for that object in the destination. This is useful if you want to automatically create new fields based on the columns in your source data.

### ⏱ Running Syncs: Schedules and API

You can happily run a sync manually, but that's not all that useful on its own. The real power of Census is having your syncs run automatically. Once you've got your sync up and running, you can configure your sync to run automatically in three ways:

* [Schedules](triggering-syncs.md#schedule)
* [Programmatically via API or Orchestration tool](triggering-syncs.md)
* [Automatically with dbt Cloud](native-dbt-integration.md#integrating-with-dbt-cloud)

Pick the sync execution trigger that makes for your connection and Census will keep the data flowing to your schedule.

## Wrapping things up

That's it! Now you've got everything you need to know to get the most out of Census, but don't worry, you can still get into the nitty gritty on individual data warehouses or service destinations. And we're always here to help. If you have any questions, just let us know!


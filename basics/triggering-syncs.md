# Triggering Syncs

You can happily run a sync manually, but that's not all that useful on its own. The real power of Census is having your syncs run automatically. Once you've got your sync up and running, you can configure your sync to run automatically in several ways:

* Schedule
* Programmatically via API
* Via Airflow
* Via dbt Cloud

## ⏱ Schedule

Schedules let you specify a time and frequency that Census can use to run your sync automatically. You can choose options from weekly all the way to Continuous, which means Census checks your source roughly every minute for new changes.

![](../.gitbook/assets/screely-1621265385900.png)

## **🏎 Sync Trigger API**

Each sync can also be triggered via API. On the configuration page, you can access the trigger API endpoint for the sync.

![](../.gitbook/assets/screely-1621265332761.png)

Here's a quick video of how to find and use it

{% embed url="https://www.loom.com/share/fa2e1c1120c346a785aff318bf615cda" caption="" %}

An empty HTTP POST call to this endpoint will trigger the sync \(no need to provide any data in the body\). You can use this API to automatically trigger Census syncs as part of your data pipeline, running syncs once the models they depend on have been rebuilt.

### `POST /syncs/[ID]/trigger`

{% tabs %}
{% tab title="Request" %}
```text
curl -X POST https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/syncs/[SYNC_ID]/trigger
```
{% endtab %}

{% tab title="Response" %}
```text
{
    "status": "success",
    "data": {
        "sync_run_id": 1234567890
    }
}
```
{% endtab %}
{% endtabs %}

| Response Property | Description |
| :--- | :--- |
| status | `success` or `error` indicating whether the sync was triggered. |
| data | Present if successful. An object containing the `sync_run_id` |
| message | Present if error. Contains message describing the error. |

### `GET /sync_runs/[ID]`

You can use the `sync_run_id` returned when successfully triggering a sync execution and get status on its progress or determine when it has completed.

{% tabs %}
{% tab title="Request" %}
```text
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sync_runs/[SYNC_RUN_ID]
```
{% endtab %}

{% tab title="Response" %}
```text
{
    "status": "success",
    "data": {
        "error_message": null,
        "records_failed": 15,
        "records_invalid": 5,
        "records_processed": 100,
        "records_updated": 80,
        "status": "completed"
    }
}
```
{% endtab %}
{% endtabs %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Response Property</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left"><code>success</code> if sync_run was found</td>
    </tr>
    <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">Present if successful. Contains the following properties:</td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">
        <ul>
          <li><code>working</code> if the sync is currently executing</li>
          <li><code>completed</code> if the sync finished successfully</li>
          <li><code>failed</code> if the sync failed during execution</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">records_processed</td>
      <td style="text-align:left">Number of new or updated records retrieved from the source</td>
    </tr>
    <tr>
      <td style="text-align:left">records_updated</td>
      <td style="text-align:left">Number of records successfully sent to the destination</td>
    </tr>
    <tr>
      <td style="text-align:left">records_invalid</td>
      <td style="text-align:left">Number of records skipped by Census because of data quality issues.</td>
    </tr>
    <tr>
      <td style="text-align:left">records_failed</td>
      <td style="text-align:left">Number of records rejected by the destination.</td>
    </tr>
  </tbody>
</table>

## 🛩 Airflow

{% embed url="https://www.loom.com/share/3437c30c24fb44c09aa0d81f79cf99e6" caption="" %}

{% hint style="info" %}
Heads up: Unlike Airflow 2, Airflow 1 doesn't show any non-"core" providers \(i.e. Census!\) in the connections UI. If you're using Airflow 1, Census should be configured as an "HTTP" Conn Type, [as documented here](https://github.com/sutrolabs/airflow-provider-census#configuration-in-airflow-110).
{% endhint %}

Whether you're using [Astronomer](https://astronomer.io) or self-hosting your own instance, you can use Census's Airflow Provider to trigger and monitor Census syncs.

Visit the [Census Airflow Provider GitHub repository](https://github.com/sutrolabs/airflow-provider-census) for more details on how to use it for your project.

## 🔌 dbt Cloud Integration

If you're using dbt Cloud to run your dbt project, you can configure Census to automatically run syncs whenever your models have been rebuilt.

Read more to learn how to [configure Cenus's dbt Cloud integration](native-dbt-integration.md#setting-it-up).


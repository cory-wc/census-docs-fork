---
description: >-
  This page describes how to configure Databricks credentials for use by Census
  and why those permissions are needed.
---

# Databricks

## Configuring a new Databricks connection

{% embed url="https://www.youtube.com/watch?v=uI9YORQ6DFs" caption="" %}

1. Visit the **Connections** section on Census, and press **Add Data Warehouse Connection**, selecting **Databricks** from the list.
2. Enter the **hostname, port, and HTTP Path** for your cluster. These can be found in the Databricks UI under **Clusters** → **\[Your Cluster\]** → **Advanced Options** **→ JDBC/ODBC.** The [Databricks documentation](https://docs.databricks.com/integrations/bi/jdbc-odbc-bi.html#workspace-cluster) covers this in more detail.

![](../.gitbook/assets/screely-1619627622845.png)

1. Enter your Databricks **Access Token.** A token can be generated in the   

   👤→ **User Settings** page in the Databricks UI.

![](../.gitbook/assets/screely-1619628186696.png)

1. Add the following configuration parameters to your cluster. This can be done under **Clusters** → **\[Your Cluster\]** → **Advanced Options** _→_ **Spark.**

```text
spark.hadoop.fs.s3n.impl.disable.cache true
spark.hadoop.fs.s3.impl.disable.cache true
spark.hadoop.fs.s3a.impl.disable.cache true
```

1. After the connection is saved, go ahead and press the **Test** button. This will validate that you've completed the above steps correctly. Once you've got a checkmark for all four steps, you're good to go!

![](../.gitbook/assets/screely-1619628263455.png)

## 🚑 Need help connecting to Databricks?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


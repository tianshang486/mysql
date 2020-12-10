# Manage storage space

Alibaba Cloud Database Autonomy Service \(DAS\) allows you to reclaim petabytes of storage space. You can manage the storage space of your database instance by using the storage analysis, capacity assessment, and cluster management features of DAS.

## Storage analysis

-   This feature displays the storage usage of your database instance and the number of remaining days with available storage. This feature also displays the storage usage, fragmentation, and exception diagnostic results of each specific table.
-   This feature is supported only for database instances that run MySQL or MongoDB. MySQL-running database instances are ApsaraDB RDS for MySQL instances or PolarDB clusters. MongoDB-running database instances are ApsaraDB for MongoDB instances or self-managed MongoDB instances. This topic describes how to use the storage analysis feature on an ApsaraDB RDS for MySQL instance.
-   If more than one database instance is created within your Alibaba Cloud account, you can view the storage usage of all the database instances on the **Global Storage Usage** page in the DAS console. Then, you can identify the database instance with the highest storage usage.

For more information about how to use the storage analysis feature, see [t1915630.dita\#multiTask701]().

## Capacity assessment

-   This feature displays capacity suggestions in the **Capacity Suggestion** section. This feature also displays the capacity trends over the last day, week, or month in the **Capacity Assessment** section. The capacity trends cover the following metrics: **CPU Utilization Watermark**, **Memory Usage Watermark**, **IOPS Usage**, **Active Sessions**, and **Storage Usage**. For more information, see [t1915631.md\#]().
-   This feature predicts storage usage by using machine learning and capacity algorithms. For more information, see [t1915631.md\#]().

**Note:** The capacity assessment feature is supported only for ApsaraDB RDS for MySQL.

## Cluster management

This feature allows you to group database instances that run the same database engine into a cluster. For example, you can group all MySQL-running database engines into a cluster. This way, this feature can display information such as the performance trends, slow SQL statement trends, and storage usage rankings of these databases instances from the cluster perspective. Based on the preceding information, this feature provides the **Data Space Usage**, **Daily Growth in Last 7 Days**, and **Available Days** of these database instances in the cluster.

For more information about how to manage clusters, see [t1915559.dita\#multiTask767]() and [t1915561.dita\#multiTask231]().


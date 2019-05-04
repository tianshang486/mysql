# Disaster tolerance {#concept_c3s_4y5_tdb .concept}

## Backup and recovery {#section_w3n_ry5_tdb .section}

-   RDS supports automatic and manual backups. You can set the automatic backup frequency or manually create backups at any time. For more information, see [Backup and recovery](https://www.alibabacloud.com/help/doc-detail/53622.htm).
-   RDS supports data recovery by time or backup set. You can restore data of any point in time within the log retention period to a new instance, verify the data, and then transfer the data to the original instance. For more information, see [Backup and recovery](https://www.alibabacloud.com/help/doc-detail/53622.htm).

## Disaster tolerance {#section_z3n_ry5_tdb .section}

|Series|Disaster tolerance|
|------|------------------|
|Basic Edition| -   Data backups are stored as multiple copies on OSS or distributed cloud disks to prevent data loss. \(This applies to all RDS series.\)
-   The Basic Edition consists of a single node without a slave node as hot backup. Therefore, if fault occurs, the restoration time is long. Choose Basic Edition if you do not require high availability.

 |
|High-availability Edition|The High-availability Edition adopts the high-availability architecture with one master node and one slave node. It is applicable to over 80% of scenarios. If the master node fails, a switchover occurs within seconds without affecting your applications. If the slave node fails, a new slave node is automatically generated to ensure high availability. -   **Single-zone instance**: The master and slave nodes are in the same zone but on different physical servers. All cabinets, air conditioners, electricity, and networks in the zone are redundant to ensure high availability.
-   **Multi-zone instance**

 **Note:** You can switch between single-zone instances and multi-zone instances. For details, see [Instance migration across zones](../../../../intl.en-US/User Guide/Instance management/Migrate instance across zones.md#).

 |
|Cluster \(AlwaysOn\) Edition|Based on the AlwaysOn technology, it provides one master node, one slave node, and up to seven read-only nodes that horizontally scale read capabilities. The slave and read-only nodes synchronize data from the master node. The Cluster Edition provides the same availability as the High-availability Edition. Besides, the read-only nodes can be deployed in zones different from those of the master and slave nodes. **Note:** 

-   Only RDS for SQL Server 2017 provides the Cluster Edition. For more information, see [Cluster Edition \(AlwaysOn Edition\)](intl.en-US/Product Introduction/Product series/Cluster Edition (AlwaysOn Edition).md#).
-   For information about RDS for MySQL read-only instances, see [Introduction to read-only instances](../../../../intl.en-US/Quick Start for MySQL/Scale instances/Read-only instance/Introduction to read-only instances.md#).
-   For information about RDS for PostgreSQL read-only instances, see [Introduction to PostgreSQL read-only instances](../../../../intl.en-US/Quick Start for PostgreSQL/Read-only instances/Introduction to PostgreSQL read-only instances.md#).
-   For information about RDS for PPAS read-only nodes, see [Introduction to PPAS read-only instances](../../../../intl.en-US/Quick Start for PPAS/Read-only instances/Introduction to PPAS read-only instances.md#).

 |

## Get started {#section_pe5_30b_j4a .section}

-   [Quick start](../../../../intl.en-US/User Guide/Quick start.md#)
-   [Learning path](https://www.alibabacloud.com/getting-started/learningpath/rds)

**Related topics**

-   [Low costs and easy-to-use](intl.en-US/Product Introduction/Benefits/Low costs and easy-to-use.md#)
-   [High performance](intl.en-US/Product Introduction/Benefits/High performance.md#)
-   [High Security](intl.en-US/Product Introduction/Benefits/High security.md#)
-   [Comparison between ApsaraDB for RDS and local databases](intl.en-US/Product Introduction/Benefits/Comparisons between ApsaraDB for RDS and self-hosted databases.md#)


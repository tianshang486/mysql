# Basic Edition {#concept_nyq_cvw_5db .concept}

## General introduction {#section_m4m_3vw_5db .section}

The Basic Edition is based on the single-node architecture and separates computing from storage, providing a cost-effective database service.

**Note:** The Basic Edition consists of a single node without a salve node as hot backup, so the database service becomes unavailable for some time when the node fails unexpectedly or is performing configuration changes. If you require high availability, choose High-availability or Cluster Edition.

The following picture shows the architecture of the Basic Edition and High-availability Edition.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7788/15567873221359_en-US.png)

## Comparative advantages {#section_wh5_tvw_5db .section}

**Performance**

The Basic Edition does not provide a slave node, so it has no performance decrease caused by real-time replication. In this aspect, the Basic Edition is superior to the High-availability Edition of the same specifications.

**Reliability**

-   Computing is separated from storage, so the failure of the compute node does not cause data loss.
-   The large-scale underlying Apsara distributed storage provides multiple replicas to ensure data reliability.

**Costs**

With the number of database nodes reduced, the price is only half that of the High-availability Edition.

## Functions {#section_xh5_tvw_5db .section}

The Basic Edition provides basic functions such as IP whitelists, monitoring, alarms, backup, and recovery, but does not provide the following functions:

-   Master/slave failover
-   Migrate to another zone
-   Log management
-   Read-only instances

For the specific functions supported by different database engines, see [Product series overview](intl.en-US/Product Introduction/Product series/Product series overview.md#).

## Applicable scenarios {#section_n2s_t7m_smo .section}

-   Small websites or applications

    You can buy cost-effective RDS instances and focus on your business without worrying about database O&M.

-   Personal learning

    You can use the Basic Edition to test and learn about databases.

-   Development and test

    RDS instances can be created within minutes. If they are Pay-As-You-Go instances, they can also be released at any time. Therefore, your development effeciency is greatly improved.


## Get started {#section_8l7_b5c_euk .section}

Currently, RDS for MySQL, SQL Server, and PostgreSQL provide the Basic Edition. Use the Quick Start to quickly create and connect to an RDS instance.

-   [Quick Start for MySQL](../../../../intl.en-US/Quick Start for MySQL/Create an instance.md#)
-   [Quick Start for SQL Server](../../../../intl.en-US/Quick Start for SQL Server/Create an instance.md#)
-   [Quick Start for PostgreSQL](../../../../intl.en-US/Quick Start for PostgreSQL/Create an instance.md#)


# Basic Edition {#concept_nyq_cvw_5db .concept}

The Basic Edition is based on the single-node architecture and separates computing from storage, providing a cost-effective database service.

**Note:** The Basic Edition consists of a single node without a salve node as hot backup, so the database service becomes unavailable for some time when the node fails unexpectedly or is performing configuration changes. If you require high availability, choose High-availability or Cluster Edition.

The following picture shows the architecture of the Basic Edition and High-availability Edition.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7788/15632090011359_en-US.png)

## Advantages {#section_wh5_tvw_5db .section}

**Performance**

The Basic Edition does not provide a slave node, so it has no performance decrease caused by real-time replication. In this aspect, the Basic Edition is superior to the High-availability Edition of the same specifications.

**Reliability**

-   Computing is separated from storage, so the failure of the compute node does not cause data loss.

    **Note:** When the log backup interval is set to 30 minutes for an SQL Server Basic Edition instance, the instance can be restored to the nearest time point with 30 minutes in the event of underlying SSD damage or force majeure. For more information, see [Back up RDS data](../../../../intl.en-US/User Guide/Backup/Back up RDS data.md#).

    ![计算与存储分离](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7788/156320900146129_en-US.png)

-   The large-scale underlying Apsara distributed storage provides multiple replicas to ensure data reliability.

**Costs**

With the number of database nodes reduced, the price is only half that of the High-availability Edition.

## Functions {#section_xh5_tvw_5db .section}

The Basic Edition provides basic functions such as IP whitelists, monitoring, alarms, backup, and recovery, but does not provide the following functions:

-   [Switch between master and slave instances](../../../../intl.en-US/User Guide/Instance management/Switch between master and slave instances.md)
-   [Migrate instance across zones](../../../../intl.en-US/User Guide/Instance management/Migrate instances across zones.md)
-   [Log management](../../../../intl.en-US/User Guide/Log management.md)
-   [Introduction to MySQL read-only instances](../../../../intl.en-US/Quick Start for MySQL/Scale instances/Read-only instance/Introduction to MySQL read-only instances.md)

For functions supported by different database engines, see [Product series overview](intl.en-US/Product Introduction/Product series/Product series overview.md#).

## Scenarios {#section_n2s_t7m_smo .section}

-   Small websites or applications

    You can buy cost-effective RDS instances and focus on your business without worrying about database O&M.

-   Personal learning

    You can use the Basic Edition to test and learn about databases.

-   Development and test

    RDS instances can be created within minutes. If they are Pay-As-You-Go instances, they can also be released at any time. Therefore, your development effeciency is greatly improved.


## Get started {#section_8l7_b5c_euk .section}

Currently, RDS for MySQL, SQL Server, and PostgreSQL provide the Basic Edition. Use Quick Start to quickly create and connect to an RDS instance.

-   [Quick Start for MySQL](../../../../intl.en-US/Quick Start for MySQL/Create an RDS for MySQL instance.md#)
-   [Quick Start for SQL Server](../../../../intl.en-US/Quick Start for SQL Server/Create an instance.md#)
-   [Quick Start for PostgreSQL](../../../../intl.en-US/Quick Start for PostgreSQL/Create an instance.md#)


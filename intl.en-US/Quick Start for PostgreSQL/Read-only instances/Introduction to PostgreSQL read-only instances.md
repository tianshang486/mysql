# Introduction to PostgreSQL read-only instances {#concept_rst_2z1_ygb .concept}

## Background {#section_lkt_qp5_vdb .section}

For services that involve a small number of write requests but a great number of read requests, a single instance may not be able to resist the read pressure. As a result, services may be affected. To achieve the elastic expansion of the read ability and share the pressure of the database, you can create one or more read-only instances in a region. The read-only instances can handle massive read requests and increase the application throughput.

## Read-only instances {#section_iw3_zqc_zdb .section}

A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances.

**Note:** 

-   RDS for PostgreSQL 10.0 supports read-only instances while PostgreSQL 9.4 does not.
-   The configuration of the master instance must be at least 8-core 32 GB \(dedicated or dedicated-host instance\).
-   Each read-only instance adopts a single-node architecture \(without slave nodes\).

The following topology shows the read-only instances.

![pgsql拓扑图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133899/155314349139776_en-US.png)

## Pricing {#section_fwf_5p5_vdb .section}

The billing method of read-only instances is Pay-As-You-Go. For more information, see [Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15K8Buqg#pricing).

## Features {#section_zx1_zp5_vdb .section}

Read-only instances offer the following features:

-   Billing method: Pay-As-You-Go. This method is more flexible and cost-effective.
-   Region and zone: Read-only instances are in the same region as the master instance, but can be in a different zone from the master instance.
-   Specifications and storage: Specifications and storage of read-only instances cannot be lower than those of the master instance.
-   [Network type](../../../../../intl.en-US/User Guide/Connection management/Set network type.md#): The network type of read-only instances can be different from that of the master instance.
-   Account and database management: Users manage accounts and databases through the master instance rather than read-only instances.
-   Whitelist: When read-only instances are created, they automatically copy the whitelist of the master instance, but the whitelists of read-only instances are independent. You can modify the whitelists of the read-only instances by referring to [EN-US\_TP\_7860.md\#](intl.en-US/Quick Start for PPAS/Initial configuration/Set a whitelist.md#).
-   Monitoring and alarms: You can monitor system performance indicators, including the disk capacity, IOPS, number of connections, and CPU usage.

## Restrictions {#section_kzn_jb1_1hb .section}

-   Number of read-only instances: Each master instance can have up to five read-only instances.
-   Backup: Read-only instances do not support backup settings or manual backups.
-   You cannot migrate data to read-only instances.
-   You cannot create or delete databases for read-only instances.
-   You cannot create or delete accounts for read-only instances.
-   You cannot authorize accounts or modify account passwords for read-only instances.


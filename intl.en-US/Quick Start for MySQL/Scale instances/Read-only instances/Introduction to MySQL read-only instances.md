# Introduction to MySQL read-only instances {#concept_cst_z45_vdb .concept}

This topic introduces MySQL read-only instances. If your application initiates a small number of write requests but a large number of read requests, a single instance may not be able to resist the read pressure. As a result, services may be affected. To achieve the elastic expansion of the read ability and share the pressure of the database, you can create one or more read-only instances in a region. The read-only instances can handle massive read requests and increase the application throughput.

## Overview {#section_iw3_zqc_zdb .section}

A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances. The synchronization works even when the master and read-only instances have different network types. Read-only instances and the master instance must be in the same region, but they can be in different zones.

**Note:** 

-   Currently the following MySQL DB engine versions and editions support read-only instances:
    -   MySQL 5.7 High-availability Edition \(with local SSDs\)
    -   MySQL 5.6
    -   SQL Server 2017
-   Each read-only instance adopts a single-node architecture \(without slave nodes\).

## Pricing {#section_fwf_5p5_vdb .section}

The billing method of read-only instances is Pay-As-You-Go. For more information, see [Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15K8Buqg#pricing).

**Note:** For information about data retention policies for read-only instances, see [Impact of expiration and overdue payment](../../../../intl.en-US/Purchase Guide/Impact of expiration and overdue payment.md).

## Features {#section_zx1_zp5_vdb .section}

Read-only instances offer the following features:

-   The specifications of a read-only instance differ from those of the master instance, and can be changed at any time, to facilitate easy elastic upgrade and downgrade.
-   Read-only instances support billing measured per hour, which is user-friendly and cost-efficient.
-   No account or database maintenance is required for a read-only instance. Both the account and database are synchronized through the master instance.
-   Read-only instances support independent whitelist configuration.
-   Read-only instances support system performance monitoring.

    Up to 20 system performance monitoring views can be used, which includes disk capacity, IOPS, connections, CPU utilization, and network traffic. Users can view the load of instances at ease.

-   Read-only instances provide optimization suggestions.

    Optimization tools support storage engine check, primary key check, large table check, and excessive indexing and missing indexing checks.


## Restrictions {#section_50t_f70_mln .section}

-   Quantity of read-only instances

    |Database type|Memory|Max number of read-only instances|
    |-------------|------|---------------------------------|
    |MySQL|≥ 64 GB|10|
    |< 64 GB|5|

-   Read-only instances do not support backup settings or temporary backup.
-   Instance recovery:
    -   Read-only instances do not support the creation of temporary instances through backup files or backups at any point in time. Read-only instances do not support the overwriting of instances using backup sets.
    -   After creating a read-only instance, the master instance does not support data recovery through the direct overwriting of instances using backup sets.
-   You cannot migrate data to read-only instances.
-   You cannot create or delete databases for read-only instances.
-   You cannot create or delete accounts for read-only instances.
-   You cannot authorize accounts or modify account passwords for read-only instances.

## FAQs {#section_3az_3n6_ej9 .section}

Can the accounts on the master instance be used on the read-only instances?

Answer: Accounts on the master instance are synchronized to the read-only instances. You can use the accounts to read data from the read-only instances but cannot write data into the read-only instances.


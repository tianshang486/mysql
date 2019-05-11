# Introduction to SQL Server read-only instances {#concept_cst_z45_vdb .concept}

## Scenario {#section_lkt_qp5_vdb .section}

For services that involve a small number of write requests but a great number of read requests, a single instance may not be able to resist the read pressure. As a result, services may be affected. To achieve the elastic expansion of the read ability and share the pressure of the database, you can create one or more read-only instances in a region. The read-only instances can handle massive read requests and increase the application throughput.

## Overview {#section_iw3_zqc_zdb .section}

A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances.

**Note:** 

-   For RDS SQL Server, only the SQL Server 2017 Cluster \(AlwaysOn\) Edition supports read-only instances.
-   Each read-only instance adopts a single-node architecture \(without slave nodes\).

The following topology shows the positioning of the read-only instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7826/15575537096089_en-US.png)

## Pricing {#section_fwf_5p5_vdb .section}

The billing method of read-only instances is Pay-As-You-Go. The following table lists the prices of common instances.

**Hourly prices of specifications and storage**

|Region| rds.mssql.s2.large

 2-core 4 GB

 | rds.mssql.s2.xlarge

 2-core 8 GB

 | rds.mssql.s3.large

 4-core 8 GB

 | rds.mssql.m1.medium

 4-core 16 GB

 | rds.mssql.c1.large

 8-core 16 GB

 | rds.mssql.c1.xlarge

 8-core 32 GB

 | rds.mssql.c2.xlarge

 16-core 64 GB

 |Storage|
|------|------------------------------------|-------------------------------------|------------------------------------|--------------------------------------|-------------------------------------|--------------------------------------|---------------------------------------|-------|
|China mainland's regions|$0.225|$0.447|$0.459|$0.851|$0.888|$1.732|$3.389|$0.0003/GB|
|Hong Kong|$0.264|$0.522|$0.537|$0.993|$1.035|$2.02|$3.954|$0.0004/GB|
|US \(Virginia\)|$0.273|$0.542|$0.556|$1.028|$1.072|$2.093|$4.096|$0.0003/GB|
|US \(Sillicon Vally\)|$0.292|$0.579|$0.595|$1.099|$1.146|$2.237|$4.378|$0.0003/GB|
|Singapore|$0.311|$0.616|$0.632|$1.170|$1.220|$2.381|$4.661|$0.0004/GB|
|Australia|$0.315|$0.622|$0.646|$1.209|$1.259|$2.415|$4.829|$0.0005/GB|
|Malaysia|$0.296|$0.586|$0.601|$1.112|$1.159|$2.262|$4.428|$0.0004/GB|
|Indonesia|$0.311|$0.616|$0.632|$1.170|$1.220|$2.381|$4.661|$0.0004/GB|
|Japan|$0.311|$0.615|$0.632|$1.171|$1.221|$2.381|$4.660|$0.0005/GB|
|Germany \(Frankfurt\)|$0.311|$0.615|$0.632|$1.171|$1.221|$2.381|$4.660|$0.0005/GB|
|UK \(London\)|$0.311|$0.615|$0.632|$1.171|$1.221|$2.381|$4.660|$0.0005/GB|
|UAE \(Dubai\)|$0.327|$0.646|$0.665|$1.230|$1.283|$2.500|$4.895|$0.0007/GB|
|India \(Mumbai\)|$0.296|$0.586|$0.601|$1.112|$1.159|$2.262|$4.428|$0.0004/GB|

## Features {#section_zx1_zp5_vdb .section}

Read-only instances offer the following features:

-   Account and database management: No account or database maintenance is required for a read-only instance. Both the account and database are synchronized through the master instance.
-   Billing: Read-only instances support billing measured per hour, which is user-friendly and cost-efficient.
-   Specifications: The specifications of a read-only instance can differ from those of the master instance, and can be changed at any time. It is recommended that the specifications of the read-only instance be equal to or higher than those of the master instance; otherwise the read-only instance may have high latency or workloads.
-   Network type: can differ from that of the master instance.
-   Whitelist: When a read-only instance is created, it automatically copies the whitelist of the master instance. However, the whitelist of the read-only instance is independent from that of the master instance. You can modify the whitelist of the read-only instance by referring to [Set the whitelist](intl.en-US/Quick Start for SQL Server/Initial configuration/Set the whitelist.md#).
-   Monitoring and alarms: Up to 20 system performance monitoring views can be used, which includes disk capacity, IOPS, connections, CPU utilization, and network traffic. Users can view the load of instances at ease.

## Restrictions { .section}

-   Quantity of read-only instances:

    |Database|Quantity|
    |--------|--------|
    |SQL Server|Up to 7 read-only instances can be created for each master instance.|

-   Read-only instances do not support backup settings or manual backup.
-   Instance recovery:
    -   Read-only instances do not support the creation of temporary instances through backup files or a point in time. Read-only instances do not support the overwriting of instances using backup sets.
    -   After creating a read-only instance, the master instance does not support data recovery through the direct overwriting of instances using backup sets.
-   You cannot migrate data to read-only instances.
-   You cannot create or delete databases for read-only instances.
-   You cannot create or delete accounts for read-only instances.
-   You cannot authorize accounts or modify account passwords for read-only instances.

## FAQs {#section_znt_2jv_fhb .section}

Can the accounts on the master instance be used on the read-only instances?

Answer: Accounts on the master instance are synchronized to the read-only instances. You can use the accounts to read data from the read-only instances but cannot write data into the read-only instances.


# Preface {#concept_gws_2dh_wdb .concept}

## Overview {#section_nkl_hdh_wdb .section}

ApsaraDB for Relational Database Service \(RDS\) is a stable and reliable online database service with auto-scaling capabilities. Based on Apsara distributed file system and high-performance SDD storage, RDS supports the MySQL, SQL Server, PostgreSQL, and PPAS \(compatible with Oracle\) database engines, and provides a complete set of solutions for disaster recovery, backup, recovery, monitoring, migration, and others. This helps you operate and manage your own database. For the benefits of RDS, see [Benefits](../../../../intl.en-US/Product Introduction/Benefits/Low costs and easy-to-use.md#).

This document describes RDS features and functions and further explains the procedure to configure RDS through the [RDS console](https://rds.console.aliyun.com/). You can also manage RDS through APIs and SDKs.

If you need technical assistance, you can call 95187. Alternatively, you can open the [RDS console](https://rds.console.aliyun.com/) and in the upper-right corner, choose **More** \> **Support** \> **Open a new ticket** to submit a ticket. If your business is complex, you can purchase a [support plan](https://www.alibabacloud.com/support/after-sales) to your exclusive support from IM enterprise groups, technical assistance managers \(TAMs\), and service managers.

For more information, visit [ApsaraDB RDS for MySQL](https://www.alibabacloud.com/product/apsaradb-for-rds) .

## Disclaimer {#section_hnn_3dh_wdb .section}

Some features or services described in this document may be unavailable for certain regions. See the relevant commercial contracts for specific terms and conditions. This document serves as a user guide only. No content in this document can constitute any express or implied warranty.

## General terms {#section_n8e_yta_o06 .section}

-   Instance: A database service process that takes up physical memory independently. You can set different memory size, disk space, and database type, among which the memory specification determines the performance of the instance. After the instance is created, you can change the instance configuration and delete the instance at any time.
-   Database: A logical unit created in an instance. Multiple databases that each have a unique name can be created in an instance.
-   Region and zone: A region is a physical data center. A zone is a physical area that has independent power supply and network within a region. For more information, see [Alibaba Cloud Global Infrastructure](https://www.alibabacloud.com/global-locations).

## Common conventions {#section_pyp_ndh_wdb .section}

|Term|Description|
|----|-----------|
|On-premises database|A database deployed in your on-premises equipment room or one that is not on ApsaraDB.|
|RDS for XX \(MySQL, SQL Server, PostgreSQL, PPAS, or MariaDB\)|A type of RDS instance that runs on a specific database engine. For example, RDS for MySQL refers to RDS instances that run on the MySQL database engine.|


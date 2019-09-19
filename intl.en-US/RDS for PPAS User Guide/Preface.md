# Preface {#concept_gws_2dh_wdb .concept}

This topic provides an overview of RDS for MySQL, including a disclaimer, terms, and concepts.

## Overview {#section_rv4_dmj_nvx .section}

Alibaba Cloud ApsaraDB for RDS \(short for Relational Database Service\) is a stable, reliable, and scalable online database service. Based on Alibaba Cloud distributed file system and high-performance SSD storage, ApsaraDB for RDS supports the MySQL, SQL Server, PostgreSQL, and PPAS \(compatible with Oracle\) database engines and provides a portfolio of solutions to disaster tolerance, backup, recovery, monitoring, and migration to facilitate database operation and maintenance. For information about the benefits of ApsaraDB for RDS, see [Low costs and easy-to-use](../../../../intl.en-US/Product Introduction/Benefits/Low costs and easy-to-use.md#).

This document describes how to configure and manage RDS through the [RDS console](https://rds.console.aliyun.com/), helping you better understand the features and functions of ApsaraDB for RDS. Additionally, you can configure and manage RDS through API and SDK.

If you need technical support, you can call 95187. Alternatively, you can open the [RDS console](https://rds.console.aliyun.com/) and in the upper-right corner choose **More** \> **Support** \> **Open a new ticket**. If your business is complex, you can purchase a [support plan](https://www.alibabacloud.com/support/after-sales) to obtain your exclusive support service from IM enterprise groups, technical service managers \(TAM\), and service managers.

For more information about ApsaraDB for RDS, visit [ApsaraDB RDS for MySQL](https://www.alibabacloud.com/product/apsaradb-for-rds).

## Disclaimer {#section_2sd_yi8_a83 .section}

Some product features or services described in this document may be unavailable for certain regions. See the relevant commercial contracts for specific Terms and Conditions. This document serves as a user guide only. No content in this document can constitute any express or implied warranty.

## Terms {#section_ind_zgf_th1 .section}

-   Instance: A database service process that takes up physical memory independently. You can specify the memory size, disk space, and database type of an instance, but only the memory specification determines the performance of the instance. After an instance is created, you can delete it or change its configuration as needed.
-   Database: A logical unit created in an instance. Multiple databases that each have a unique name can be created in one instance.
-   Region and zone: A region is a physical data center. A zone is a physical area that has independent power supply and network in a region. For more information, visit [Alibaba Cloud's Global Infrastructure](https://www.alibabacloud.com/global-locations).

## Concepts {#section_0bf_13q_iqb .section}

|Item|Description|
|----|-----------|
|On-premises database|A database that is deployed in your on-premises equipment room or on a cloud other than ApsaraDB for RDS.|
| RDS for XX \(XX is MySQL, SQL Server, PostgreSQL, or PPAS.\)

 |A type of RDS instance. For example, RDS for MySQL refers to the type of RDS instance that runs in the MySQL database engine.|


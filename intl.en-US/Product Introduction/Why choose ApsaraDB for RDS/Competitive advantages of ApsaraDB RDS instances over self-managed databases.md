# Competitive advantages of ApsaraDB RDS instances over self-managed databases

ApsaraDB RDS provides highly available, reliable, secure, and scalable cloud-hosted databases that are comparable to commercial databases, but at prices approximately two thirds lower than self-managed databases hosted on ECS instances and nine tenths lower than self-managed databases deployed on third-party database servers.

## Price comparison between ApsaraDB RDS instances and self-managed databases

|Item|ApsaraDB RDS instance|Self-managed database on ECS instance|Self-managed database on third-party database server|
|----|---------------------|-------------------------------------|----------------------------------------------------|
|Hardware, spare parts, and accessories|You only need to pay for the RDS instances that you create. For example, an RDS instance that provides two CPUs, 4 GB of memory, and 100 GB of storage to deliver up to 6,800 input/output operations per second \(IOPS\) costs USD 1,000 per year.|You must purchase at least two ECS instances to set up a primary/secondary architecture. Two ECS instances that each provide two CPUs, 4 GB of memory, and 100 GB of storage to deliver up to 6,800 IOPS costs USD 900 per year.|-   You must purchase at least two database servers. A database server that delivers up to 6,800 IOPS costs about USD 1,200.
-   You must purchase one internal switch to connect to the frontend web server. A 1U non-hosted switch costs about USD 140.
-   You must purchase spare parts and accessories for future repairs and replacements. These spare parts and accessories cost at least 30% of the initial hardware fee.
-   The total fee is about USD 3,300 based on the following formula: \(1200 × 2 + 140\) × 130% ≈ 3300.

If the hardware, spare parts, and accessories are deprecated in three years, the annual fee is USD 1,100 based on the following formula: 3300/3 = 1100. |
|Data center hosting|The cloud service provider pays the hosting fee. No fees are required from you.|The cloud service provider pays the hosting fee. No fees are required from you.|Every 1U of rack space costs USD 400 per year. The annual fee required to host two 1U database servers and one 1U internal switch is USD 1,200 based on the following formula: 400 × 3 = 1200.|
|Bandwidth|-   ECS and RDS instances in the same region can communicate over an internal network free of charge.
-   ECS and RDS instances in different regions can communicate over the Internet, but you must pay for the Internet traffic that you consume. For more information, see [ApsaraDB RDS pricing](https://www.alibabacloud.com/zh/product/apsaradb-for-rds?spm=a2c63.o282931.a3.1.11fb6ddbLf1nuC#pricing).

|-   ECS instances in the same region can communicate over an internal network free of charge.
-   ECS instances in different regions can communicate over the Internet, but you must pay for the Internet traffic that you consume. For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).

|Your databases can communicate only over an internal network. You do not need to pay for Internet traffic, because you do not consume Internet traffic.|
|Database operations and maintenance \(O&M\)|The cloud service provider pays the O&M fee. No fees are required from you.|The monthly salary of a junior database administrator is USD 5,000 or more. If a database project accounts for 30% of the total workload that a junior database administrator needs to complete, the annual fee required to maintain that database project is at least USD 18,000 based on the following formula: 5000 × 12 × 30% = 18000.|The monthly salary of a junior database administrator is USD 5,000 or more. If a database project accounts for 30% of the total workload that a junior database administrator needs to complete, the annual fee required to maintain that database project is at least USD 18,000 based on the following formula: 5000 × 12 × 30% = 18000.|
|Total|USD 1,000/year|USD 18,900/year|USD 20,300/year|

## Advantages of ApsaraDB RDS for MySQL instances over self-managed databases

|Item|ApsaraDB RDS for MySQL instance|Self-managed database on ECS instance|Self-managed database on third-party database server|
|----|-------------------------------|-------------------------------------|----------------------------------------------------|
|Cost-effectiveness|-   Scalable resources are provided.
-   AliSQL is an independent MySQL branch that is developed by Alibaba Cloud. It provides a number of similar features that you can find in the MySQL Enterprise edition. These features allow you to improve user experience. For more information, see [Features of AliSQL](/intl.en-US/Proprietary AliSQL/Features of AliSQL.md).
-   A free quota for backup storage that is equal to half the total storage capacity of your ApsaraDB RDS for MySQL instance is offered to store backups. For more information, see [View the free quota for backup storage of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md).
-   Internet traffic is free of charge.
-   User-provided domain names are supported free of charge.
-   Updates to ApsaraDB RDS for MySQL are released by Alibaba Cloud sequentially with the latest MySQL releases.

|-   Scalable resources are provided.
-   The open source MySQL edition is used, and no optimization is provided.
-   You must pay for the backup storage that you use.
-   You must pay for the Internet traffic that you consume.

|-   The initial investment is high.
-   The open source MySQL edition is used, and no optimization is provided.
-   You must allocate independent backup resources, which incur high costs.
-   You must pay for the Internet traffic that you consume and the domain names that you use, which are charged at high rates. |
|Availability|-   In the Basic Edition, your database system takes about 15 minutes to complete a failover.
-   In the High-availability and Cluster Editions, your database system takes 30 seconds or less to complete a failover.
-   You can create read-only instances to balance loads in your database system. For more information, see [Overview of read-only ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md).
-   Read/write splitting allows your database system to distribute read and write requests by using a unified read/write splitting endpoint. For more information, see [Read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md)
-   Analytic instances that are used to analyze the data of various businesses are under development.

|-   In the Basic Edition, your databases take about 30 minutes to complete a failover.
-   You must purchase additional software or hardware to set up a high availability architecture.
-   You must purchase additional software or hardware to balance loads among your databases.
-   If you want to analyze data, you must create analytic databases, which is time-consuming and costly.

|-   Your databases are standalone. If a database server breaks down, repairs can take hours to weeks.
-   You must purchase additional software or hardware to set up a high availability architecture.
-   You must purchase additional software or hardware to balance loads among your databases.
-   If you want to analyze data, you must create analytic databases, which is time-consuming and costly. |
|Reliability|-   Automated replication of data between primary and secondary instances, data backup, and log backup are provided to ensure high data reliability.
-   The Enterprise Edition with MySQL 5.7 supports MySQL Group Replication \(MGR\) and delivers a Recovery Point Objective \(RPO\) of 0 and a Recovery Time Objective \(RTO\) of less than 1 minute.

|-   Your databases are highly available only if they are deployed in an optimal high availability architecture.
-   To deliver an RPO of 0, you must purchase independent research and development \(R&D\) services, which incur high costs.

|-   Data reliability is moderate and varies based on the corruption probability of individual disks.
-   To deliver an RPO of 0, you must purchase independent R&D services, which incur high costs. |
|Usability|-   Automated backup and restoration support streaming backup, point in time recovery \(PITR\), and backup and restoration at the database level to minimize impacts on the performance of your database system. For more information, see [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).
-   Automated monitoring and alerting allow you to monitor all of the supported instance- and database-level performance metrics in seconds, and send alerts to you by using Short Message Service \(SMS\), email, and DingTalk. In addition, you are offered a free quota for SMS alerts based on your purchase details. For more information, see [Configure an alert rule for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md).
-   You can update a minor engine version with a few clicks. For more information, see [Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md).

|-   Automated backup is not supported. You must purchase or configure the streaming backup and PITR features. This incurs high costs.
-   You must purchase an independent monitoring system and configure it in the Cloud Monitor console.
-   Usability faces technical challenges.
-   Version updates are costly.

|-   Automated backup is not supported. You must purchase or configure the streaming backup and PITR features. This incurs high costs.
-   You must purchase or configure an independent monitoring system, which incurs high costs.
-   Remote data centers are costly and difficult to set up.
-   Version updates are costly. |
|Performance|-   ApsaraDB RDS for MySQL instances with local SSDs excel in performance.
-   ApsaraDB RDS for MySQL instances perform better with enhanced SSDs than with local or standard SSDs.
-   You can create read-only instances to increase performance and balance loads.
-   The SQL explorer feature meets your business requirements in most of the database monitoring and performance optimization scenarios. For more information, see [SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md).

|-   If you choose local disks, data reliability is reduced. However, if you choose cloud disks, you must plan a disk architecture, which incurs high costs.
-   If the same enhanced SSDs are used, ECS-hosted self-managed MySQL databases are inferior to ApsaraDB RDS for MySQL instances.
-   The Cluster Edition is difficult to deploy due to high consultancy and maintenance costs.
-   You must recruit experienced database administrators. This incurs high costs.

|-   Database servers are updated at lower speeds than cloud computing hardware. Therefore, self-managed databases on these servers are inferior to ApsaraDB RDS for MySQL instances.
-   Computing-storage separation is difficult and can cost millions of US dollars on advanced storage media.
-   The Cluster Edition is difficult to deploy due to high consultancy and maintenance costs.
-   You must recruit experienced database administrators. This incurs high costs. |
|Security|-   The whitelist, security group, and virtual private cloud \(VPC\) isolation mechanisms are provided. For more information, see [IP address whitelists](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md), [Security groups](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.mdsection_dsr_nt4_ydb), and [VPC](https://www.alibabacloud.com/help/zh/doc-detail/34217.htm).
-   The link encryption and disk encryption protection mechanisms are provided, with Bring Your Own Keys \(BYOKs\) supported for various storage media. For more information, see [Configure SSL encryption on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure SSL encryption on an ApsaraDB RDS for MySQL instance.md) and [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md).
-   The SQL explorer audit mechanism is provided. For more information, see [SQL Explorer](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md).

|-   The whitelist, security group, and VPC isolation mechanisms are provided.
-   You must purchase or configure the link encryption and disk encryption protection mechanisms. This incurs high consultancy costs due to difficulties in the rotation of BYOKs.
-   SQL audit is difficult because you must store SQL logs separately.

|-   You must configure the whitelist and VPC isolation mechanisms. This incurs high consultancy costs.
-   You must purchase or configure the link encryption and disk encryption protection mechanisms. This incurs high consultancy costs due to difficulties in the rotation of BYOKs.
-   SQL audit is difficult because you must store SQL logs separately. |

## Advantages of ApsaraDB RDS for SQL Server instances over self-managed databases

|Item|ApsaraDB RDS for SQL Server instance|Self-managed database on ECS instance|Self-managed database on third-party database server|
|----|------------------------------------|-------------------------------------|----------------------------------------------------|
|Cost-effectiveness|-   Scalable resources are provided.
-   SQL Server Web editions are offered to increase cost-effectiveness.
-   A free quota for backup storage that is equal to half the total storage capacity of your ApsaraDB RDS for SQL Server instance is offered to store backups. For more information, see [View the free quota for backup storage of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/View the free quota for backup usage of an ApsaraDB RDS for SQL Server instance.md).
-   Internet traffic is free of charge.

|-   Scalable resources are provided.
-   No SQL Server Web editions are offered.
-   You must pay for the backup storage that you use.
-   You must pay for the Internet traffic that you consume.

|-   The initial investment is high.
-   No SQL Server Web editions are offered.
-   You must allocate independent backup resources, which incur high costs.
-   You must pay for the Internet traffic that you consume and the domain names that you use, which are charged at high rates. |
|Availability|-   In the Basic Edition, your database system takes about 15 minutes to complete a failover.
-   In the High-availability and Cluster Editions, your database system takes 30 seconds or less to complete a failover.
-   In the Cluster Edition, you can create read-only instances to balance loads in your database system. For more information, see [Overview of read-only ApsaraDB RDS for SQL Server instances](/intl.en-US/RDS SQL Server Database/Quick start/Read-only instances/Overview of read-only ApsaraDB RDS for SQL Server instances.md).
-   In the Cluster Edition, you can use read/write splitting to distribute read and write requests by using a unified read/write splitting endpoint. For more information, see [Read/write splitting overview](/intl.en-US/RDS SQL Server Database/Read/write splitting/Read/write splitting overview.md).

|-   In the Basic Edition, your databases take about 30 minutes to complete a failover.
-   You must purchase additional software or hardware to set up a high availability architecture.
-   You must purchase additional software or hardware to balance loads among your databases.

|-   Your databases are standalone. If a database server breaks down, repairs can take hours to weeks.
-   You must purchase additional software or hardware to set up a high availability architecture.
-   You must purchase additional software or hardware to balance loads among your databases. |
|Reliability|-   Automated replication of data between primary and secondary instances, data backup, and log backup are provided to ensure high data reliability.
-   The Cluster Edition delivers an RPO of 0.

|-   Your databases are highly available only if they are deployed in an optimal high availability architecture.
-   To deliver an RPO of 0, you must purchase independent R&D services, which incur high costs.

|-   Data reliability is moderate and varies based on the corruption probability of individual disks.
-   To deliver an RPO of 0, you must purchase independent R&D services, which incur high costs. |
|Usability|-   Automated backup and restoration support streaming backup, PITR, and backup and restoration at the database level to minimize impacts on the performance of your database system. For more information, see [Back up an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Backup/Back up an ApsaraDB RDS for SQL Server instance.md).
-   Automated monitoring and alerting allow you to monitor all of the supported instance- and database-level performance metrics in seconds, and send alerts to you by using SMS, email, and DingTalk. In addition, you are offered a free quota for SMS alerts based on your purchase details. For more information, see [Configure an alert rule for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Configure an alert rule for an ApsaraDB RDS for MySQL instance.md).
-   Geo-disaster recovery is under development.

|-   Automated backup is not supported. You must purchase or configure the streaming backup and PITR features. This incurs high costs.
-   You must purchase an independent monitoring system and configure it in the Cloud Monitor console.
-   Usability faces technical challenges.

|-   Automated backup is not supported. You must purchase or configure the streaming backup and PITR features. This incurs high costs.
-   You must purchase or configure an independent monitoring system, which incurs high costs.
-   Remote data centers are costly and difficult to set up. |
|Performance|-   Instances that run SQL Server 2008 R2 with local SSDs excel in performance. Instances that run SQL Server 201x support next-generation computing-storage separation, which benefits from hardware dividends.
-   ApsaraDB RDS for SQL Server instances perform better with enhanced SSDs than with local or standard SSDs.
-   You can create read-only instances to increase performance and balance loads.

|-   If you choose local disks, data reliability is reduced. However, if you choose cloud disks, you must plan a disk architecture, which incurs high costs.
-   If the same enhanced SSDs are used, ECS-hosted self-managed SQL Server databases are inferior to ApsaraDB RDS for SQL Server instances.
-   The Cluster Edition is difficult to deploy due to high consultancy and maintenance costs.
-   You must recruit experienced database administrators. This incurs high costs.

|-   Database servers are updated at lower speeds than cloud computing hardware. Therefore, self-managed databases on these servers are inferior to ApsaraDB RDS for SQL Server instances.
-   Computing-storage separation is difficult and can cost millions of US dollars on advanced storage media.
-   The Cluster Edition is difficult to deploy due to high consultancy and maintenance costs.
-   You must recruit experienced database administrators. This incurs high costs. |
|Security|-   The whitelist and VPC isolation mechanisms are provided. For more information, see [Configure a whitelist for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Configure a whitelist for an ApsaraDB RDS for SQL Server instance.md) and [What is a VPC?](https://www.alibabacloud.com/help/zh/doc-detail/34217.htm)
-   The link encryption and disk encryption protection mechanisms are provided. For more information, see [Configure SSL encryption on an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure SSL encryption on an ApsaraDB RDS for SQL Server instance.md) and [Configure TDE for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md).
-   Updates to ApsaraDB RDS for SQL Server are released by Alibaba Cloud sequentially with the latest Microsoft releases.

|-   The whitelist, security group, and VPC isolation mechanisms are provided.
-   You must purchase or configure the link encryption and disk encryption protection mechanisms. This incurs high consultancy costs.
-   SQL audit is difficult because you must store SQL logs separately.

|-   You must configure the whitelist and VPC isolation mechanisms. This incurs high consultancy costs.
-   You must purchase or configure the link encryption and disk encryption protection mechanisms. This incurs high consultancy costs.
-   SQL audit is difficult because you must store SQL logs separately. |
|Legal liability|-   ApsaraDB RDS for SQL Server is provided with a valid license. You do not need to bear any legal liabilities.
-   User-provided licenses will be supported soon. These licenses reduce your overall expenditure.

|You must purchase a valid license.|You must purchase a valid license. Otherwise, you may bear legal liabilities.|

## Advantages of ApsaraDB RDS for PostgreSQL instances over self-managed databases

|Item|ApsaraDB RDS for PostgreSQL instance|Self-managed database on ECS instance|Self-managed database on third-party database server|
|----|------------------------------------|-------------------------------------|----------------------------------------------------|
|Cost-effectiveness|-   Scalable resources are provided.
-   AliPG is compatible with open source PostgreSQL. It provides various features to improve user experience, including a number of Alibaba Cloud-proprietary features. For more information, see [AliPG overview](/intl.en-US/Proprietary AliPG/AliPG benefits.md).
-   A free quota for backup storage that is equal to half the total storage capacity of your ApsaraDB RDS for PostgreSQL instance is offered to store backups. For more information, see [View the free quota for backup storage of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for PostgreSQL instance.md).
-   Internet traffic is free of charge.
-   User-provided domain names are supported free of charge.
-   Updates to ApsaraDB RDS for PostgreSQL are released by Alibaba Cloud sequentially with the latest PostgreSQL releases.

|-   Scalable resources are provided.
-   The open source PostgreSQL edition is used, and no optimization is provided.
-   You must pay for the backup storage that you use.
-   You must pay for the Internet traffic that you consume.

|-   The initial investment is high.
-   The open source PostgreSQL edition is used, and no optimization is provided.
-   You must allocate independent backup resources, which incur high costs.
-   You must pay for the Internet traffic that you consume and the domain names that you use, which are charged at high rates. |
|Availability|-   In the Basic Edition, your database system takes about 15 minutes to complete a failover.
-   In the High-availability Edition, your database system takes 30 seconds or less to complete a failover.
-   You can create read-only instances to balance loads in your database system. For more information, see [Overview of read-only ApsaraDB RDS for PostgreSQL instances](/intl.en-US/RDS PostgreSQL Database/Quick start/RDS for PostgreSQL read-only instances/Overview of read-only ApsaraDB RDS for PostgreSQL instances.md).

|-   In the Basic Edition, your databases take about 30 minutes to complete a failover.
-   You must purchase additional software or hardware to set up a high availability architecture.
-   You must purchase additional software or hardware to balance loads among your databases.

|-   Your databases are standalone. If a database server breaks down, repairs can take hours to weeks.
-   You must purchase additional software or hardware to set up a high availability architecture.
-   You must purchase additional software or hardware to balance loads among your databases. |
|Reliability|-   Automated replication of data between primary and secondary instances, data backup, and log backup are provided to ensure high data reliability.
-   RPO customization allows you to specify an RPO of 0.

|-   Your databases are highly available only if they are deployed in an optimal high availability architecture.
-   To deliver an RPO of 0, you must purchase independent R&D services, which incur high costs.

|-   Data reliability is moderate and varies based on the corruption probability of individual disks.
-   To deliver an RPO of 0, you must purchase independent R&D services, which incur high costs. |
|Usability|-   Automated backup and restoration support streaming backup, PITR, and backup and restoration at the database level to minimize impacts on the performance of your database system. For more information, see [Back up an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Backup/Back up an ApsaraDB RDS for PostgreSQL instance.md).
-   Automated monitoring and alerting allow you to monitor all of the supported instance- and database-level performance metrics, and send alerts to you by using SMS, email, and DingTalk. In addition, you are offered a free quota for SMS alerts based on your purchase details. For more information, see [Configure an alert rule for an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Monitoring and alerts/View resource and engine monitoring data.md).

|-   Automated backup is not supported. You must purchase or configure the streaming backup and PITR features. This incurs high costs.
-   You must purchase an independent monitoring system and configure it in the Cloud Monitor console.

|-   Automated backup is not supported. You must purchase or configure the streaming backup and PITR features. This incurs high costs.
-   You must purchase or configure an independent monitoring system, which incurs high costs. |
|Performance|-   ApsaraDB RDS for PostgreSQL instances with local SSDs excel in performance.
-   ApsaraDB RDS for PostgreSQL instances perform better with enhanced SSDs than with local or standard SSDs.
-   You can create read-only instances to increase performance and balance loads.
-   The SQL explorer feature meets your business requirements in most of the database monitoring and performance optimization scenarios. For more information, see [Enable and disable SQL Audit \(database audit\) on an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Audit/Enable and disable SQL Audit (database audit) on an ApsaraDB RDS for PostgreSQL instance.md).

|-   If you choose local disks, data reliability is reduced. However, if you choose cloud disks, you must plan a disk architecture, which incurs high costs.
-   If the same enhanced SSDs are used, ECS-hosted self-managed PostgreSQL databases are inferior to ApsaraDB RDS for PostgreSQL instances.
-   You must recruit experienced database administrators. This incurs high costs.

|-   Database servers are updated at lower speeds than cloud computing hardware. Therefore, self-managed databases on these servers are inferior to ApsaraDB RDS for PostgreSQL instances.
-   Computing-storage separation is difficult and can cost millions of US dollars on advanced storage media.
-   You must recruit experienced database administrators. This incurs high costs. |
|Security|-   The whitelist, security group, and VPC isolation mechanisms are provided. For more information, see [IP address whitelists](/intl.en-US/RDS PostgreSQL Database/Data security/Configure a whitelist for an ApsaraDB RDS for PostgreSQL instance.md), [Security groups](/intl.en-US/RDS PostgreSQL Database/Quick start/Configure a whitelist for an ApsaraDB RDS for PostgreSQL instance.md), and [VPC](https://www.alibabacloud.com/help/zh/doc-detail/34217.htm).
-   The link encryption and disk encryption protection mechanisms are provided. For more information, see [Configure SSL encryption](/intl.en-US/RDS PostgreSQL Database/Data security/Configure data encryption for an RDS PostgreSQL instance.md) and [Configure disk encryption](/intl.en-US/RDS PostgreSQL Database/Data security/Configure data encryption for an RDS PostgreSQL instance.mdsection_ffo_jzy_q7z).
-   The SQL audit mechanism is provided. For more information, see [Enable and disable SQL Audit \(database audit\) on an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Audit/Enable and disable SQL Audit (database audit) on an ApsaraDB RDS for PostgreSQL instance.md).

|-   The whitelist, security group, and VPC isolation mechanisms are provided.
-   You must purchase or configure the link encryption protection mechanism.
-   SQL audit is difficult because you must store SQL logs separately.

|-   You must configure the whitelist and VPC isolation mechanisms. This incurs high consultancy costs.
-   You must purchase or configure the link encryption protection mechanism.
-   SQL audit is difficult because you must store SQL logs separately. |

## Get started with ApsaraDB RDS

-   [Quick Start](/intl.en-US/Quick Start/Quick Start.md)
-   [RDS Learning Path](https://www.alibabacloud.com/getting-started/learningpath/rds)

For more information, see the following topics:

-   [Quick Start](/intl.en-US/Quick Start/Quick Start.md)
-   [Cost effective and easy to use](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/Cost effective and easy to use.md)
-   [High performance](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/High performance.md)
-   [High security](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/High security.md)
-   [High availability and disaster tolerance](/intl.en-US/Product Introduction/Why choose ApsaraDB for RDS/High availability and disaster tolerance.md)


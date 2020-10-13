# Read-only instance types

This topic introduces the read-only instance types supported by ApsaraDB for RDS.

You can add [read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md) to scale the read capability of your database system.

For more information about primary instance types, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).

## Prices of RDS read-only instances

Please download the following files to check the price of RDS read-only instances.

[Monthly prices of RDS read-only instance specifications](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/141303/cn_zh/1595215398287/RDS_read_only_instance_specifications_monthly_price.xlsx)

For prices of pay-as-you-go specifications and capacities, see:

-   [RDS MySQL](https://www.alibabacloud.com/product/apsaradb-for-rds-mysql/pricing)
-   [RDS SQL Server](https://www.alibabacloud.com/product/apsaradb-for-rds-sql-server/pricing)
-   [RDS PostgreSQL](https://www.alibabacloud.com/product/apsaradb-for-rds-postgresql/pricing)
-   [RDS PPAS](https://www.alibabacloud.com/product/apsaradb-for-rds-ppas/pricing)

## ApsaraDB RDS for MySQL read-only instances

|Category|MySQL version|Instance family|Instance type|CPU and memory|Maximum number of connections|Maximum IOPS|Storage capacity|
|--------|-------------|---------------|-------------|--------------|-----------------------------|------------|----------------|
|Read-only instance|5.6, 5.7, and 8.0|General-purpose instance|rds.mysql.t1.small|1 core, 1 GB|300|600|5 GB to 2,000 GB|
|rds.mysql.s1.small|1 core, 2 GB|600|1,000|
|rds.mysql.s2.large|2 cores, 4 GB|1,200|2,000|
|rds.mysql.s2.xlarge|2 cores, 8 GB|2,000|4,000|
|rds.mysql.s3.large|4 cores, 8 GB|2,000|5,000|
|rds.mysql.m1.medium|4 cores, 16 GB|4,000|7,000|
|rds.mysql.c1.large|8 cores, 16 GB|4,000|8,000|
|rds.mysql.c1.xlarge|8 cores, 32 GB|8,000|12,000|
|rds.mysql.c2.xlarge|16 cores, 64 GB|16,000|14,000|5 GB to 3,000 GB|
|rds.mysql.c2.xlp2|16 cores, 96 GB|24,000|16,000|
|Dedicated instance \(with a large memory capacity\)|mysqlro.x8.medium.1|2 cores, 16 GB|2,500|4,500|50 GB to 2,000 GB|
|mysqlro.x8.large.1|4 cores, 32 GB|5,000|9,000|50 GB to 2,000 GB|
|mysqlro.x8.xlarge.1|8 cores, 64 GB|10,000|18,000|500 GB to 3,000 GB|
|mysqlro.x8.2xlarge.1|16 cores, 128 GB|20,000|36,000|500 GB to 3,000 GB|
|mysqlro.x8.4xlarge.1|32 cores, 256 GB|40,000|72,000|1,000 GB to 6,000 GB|
|mysqlro.x8.8xlarge.1|64 cores, 512 GB|80,000|144,000|1,000 GB to 6,000 GB|
|Dedicated instance \(with a large number of CPU cores\)|mysqlro.x4.large.1|4 cores, 16 GB|2,500|4,500|50 GB to 2,000 GB|
|mysqlro.x4.xlarge.1|8 cores, 32 GB|5,000|9,000|500 GB to 3,000 GB|
|mysqlro.x4.2xlarge.1|16 cores, 64 GB|10,000|18,000|500 GB to 3,000 GB|
|mysqlro.x4.4xlarge.1|32 cores, 128 GB|20,000|36,000|1,000 GB to 6,000 GB|

## ApsaraDB RDS for SQL Server read-only instances

|Category|SQL Server version|Instance family|Instance type|CPU and memory|Maximum number of connections|Maximum IOPS|Storage capacity|
|--------|------------------|---------------|-------------|--------------|-----------------------------|------------|----------------|
|Read-only instance|2017 EE|General-purpose instance|rds.mssql.s2.large|2 cores, 4 GB|Unlimited|See [IOPS](/intl.en-US/Product Introduction/Product specifications/Primary instance types.mdsection_ire_dbl_kzm).|20 GB to 4,000 GB|
|rds.mssql.s3.large|4 cores, 8 GB|
|rds.mssql.c1.large|8 cores, 16 GB|
|rds.mssql.s2.xlarge|2 cores, 8 GB|
|rds.mssql.m1.medium|4 cores, 16 GB|
|rds.mssql.c1.xlarge|8 cores, 32 GB|
|rds.mssql.c2.xlarge|16 cores, 64 GB|
|Dedicated instance|mssql.x4.medium.ro|2 cores, 8 GB|
|mssql.x4.large.ro|4 cores, 16 GB|
|mssql.x4.xlarge.ro|8 cores, 32 GB|
|mssql.x4.2xlarge.ro|16 cores, 64 GB|
|mssql.x4.4xlarge.ro|32 cores, 128 GB|
|mssql.x4.8xlarge.ro|64 cores, 256 GB|
|mssql.x8.medium.ro|2 cores, 16 GB|
|mssql.x8.large.ro|4 cores, 32 GB|
|mssql.x8.xlarge.ro|8 cores, 64 GB|
|mssql.x8.2xlarge.ro|16 cores, 128 GB|
|mssql.x8.4xlarge.ro|32 cores, 256 GB|
|mssql.x8.7xlarge.ro|56 cores, 480 GB|
|mssql.x8.8xlarge.ro|64 cores, 512 GB|

## ApsaraDB RDS for PostgreSQL read-only instances \(with local SSDs\)

|Category|PostgreSQL version|Instance family|Instance type|CPU and memory|Maximum number of connections|Maximum IOPS|Storage capacity|
|--------|------------------|---------------|-------------|--------------|-----------------------------|------------|----------------|
|Read-only instance|10

|Dedicated instance \(with a large memory capacity\)|pg.x8.xlarge.2|8 cores, 64 GB|10,000|18,000|20 GB to 6,000 GB|
|pg.x8.2xlarge.2|16 cores, 128 GB|12,000|36,000|
|Dedicated instance \(with a large number of CPU cores\)|pg.x4.xlarge.2|8 cores, 32 GB|5,000|9,000|
|pg.x4.2xlarge.2|16 cores, 64 GB|10,000|18,000|
|pg.x4.4xlarge.2|32 cores, 128 GB|12,000|36,000|
|Dedicated host|rds.pg.st.h43|60 cores, 470 GB|4,000|50,000|

## ApsaraDB RDS for PPAS read-only instances

|Category|PPAS version|Instance family|Instance type|CPU and memory|Maximum number of connections|Maximum IOPS|Storage capacity|
|--------|------------|---------------|-------------|--------------|-----------------------------|------------|----------------|
|Read-only instance|10

|General-purpose instance|rds.ppas.t1.small|1 core, 1 GB|100|1,200|150 GB|
|Dedicated instance|ppas.x4.small.2|1 core, 4 GB|200|5,000|250 GB|
|ppas.x4.medium.2|2 cores, 8 GB|400|10,000|
|ppas.x8.medium.2|2 cores, 16 GB|2,500|15,000|
|ppas.x4.large.2|4 cores, 16 GB|2,500|20,000|250 GB or 500 GB|
|ppas.x8.large.2|4 cores, 32 GB|5,000|30,000|
|ppas.x4.xlarge.2|8 cores, 32 GB|5,000|40,000|500 GB or 1,000 GB|
|ppas.x8.xlarge.2|8 cores, 64 GB|10,000|60,000|
|ppas.x4.2xlarge.2|16 cores, 64 GB|10,000|80,000|1,000 GB or 2,000 GB|
|ppas.x8.2xlarge.2|16 cores, 128 GB|12,000|120,000|
|ppas.x4.4xlarge.2|32 cores, 128 GB|12,000|160,000|2,000 GB or 3,000 GB|
|ppas.x8.4xlarge.2|32 cores, 256 GB|12,000|240,000|
|Dedicated host|rds.ppas.st.h43|60 cores, 470 GB|12,000|450,000|3,000 GB, 4,000 GB, 5,000 GB, or 6,000 GB|


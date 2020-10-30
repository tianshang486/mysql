# Read-only instance types

This topic provides an overview of read-only ApsaraDB RDS instance types. You can view the latest and historical specifications of each type.

ApsaraDB RDS allows you to create [read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md) to scale the read capability of your database system.

For more information about primary instance types, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).

## Read-only instance prices

Download the following files to obtain detailed prices:

[Subscription Prices for Read-only ApsaraDB RDS Instances \(Specifications\)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/141303/cn_zh/1595212336565/%E5%9B%BD%E9%99%85%E7%AB%99RDS%E5%8F%AA%E8%AF%BB%E5%AE%9E%E4%BE%8B%E5%8C%85%E5%B9%B4%E5%8C%85%E6%9C%88%E5%AE%9A%E4%BB%B7%EF%BC%88%E8%A7%84%E6%A0%BC%EF%BC%89.xlsx)

For more information about prices of pay-as-you-go instances and storage capacities, visit the following pages:

-   [RDS MySQL](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-mysql/pricing)
-   [RDS SQL Server](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-sql-server/pricing)
-   [RDS PostgreSQL](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-postgresql/pricing)
-   [RDS PPAS](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-ppas/pricing)

## Read-only ApsaraDB RDS for MySQL instances

|Category|MySQL version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|--------|-------------|---------------|-------------|--------------|-------------------|------------|----------------|
|Read-only instance|5.6, 5.7, and 8.0|General-purpose instance family|rds.mysql.t1.small|1 CPU core, 1 GB|300|600|5GB-2000GB|
|rds.mysql.s1.small|1 CPU core, 2 GB|600|1000|
|rds.mysql.s2.large|2 CPU cores, 4 GB|1200|2000|
|rds.mysql.s2.xlarge|2 CPU cores, 8 GB|2000|4000|
|rds.mysql.s3.large|4 CPU cores, 8 GB|2000|5000|
|rds.mysql.m1.medium|4 CPU cores, 16 GB|4000|7000|
|rds.mysql.c1.large|8 CPU cores, 16 GB|4000|8000|
|rds.mysql.c1.xlarge|8 CPU cores, 32 GB|8000|12000|
|rds.mysql.c2.xlarge|16 CPU cores, 64 GB|16000|14000|5GB-3000GB|
|rds.mysql.c2.xlp2|16 CPU cores, 96 GB|24000|16000|
|Dedicated instance family \(with a large memory capacity\)|mysqlro.x8.medium.1|2 CPU cores, 16 GB|2500|4500|50GB-2000GB|
|mysqlro.x8.large.1|4 CPU cores, 32 GB|5000|9000|50GB-2000GB|
|mysqlro.x8.xlarge.1|8 CPU cores, 64 GB|10000|18000|500GB-3000GB|
|mysqlro.x8.2xlarge.1|16 CPU cores, 128 GB|20000|36000|500GB-3000GB|
|mysqlro.x8.4xlarge.1|32 CPU cores, 256 GB|40000|72000|1000GB-6000GB|
|mysqlro.x8.8xlarge.1|64 CPU cores, 512 GB|80000|144000|1000GB-6000GB|
|Dedicated instance family \(with a large number of CPU cores\)|mysqlro.x4.large.1|4 CPU cores, 16 GB|2500|4500|50GB-2000GB|
|mysqlro.x4.xlarge.1|8 CPU cores, 32 GB|5000|9000|500GB-3000GB|
|mysqlro.x4.2xlarge.1|16 CPU cores, 64 GB|10000|18000|500GB-3000GB|
|mysqlro.x4.4xlarge.1|32 CPU cores, 128 GB|20000|36000|1000GB-6000GB|

## Read-only ApsaraDB RDS for SQL Server instances

|Category|SQL Server version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|--------|------------------|---------------|-------------|--------------|-------------------|------------|----------------|
|Read-only instance|2017 EE|General-purpose instance family|rds.mssql.s2.large|2 CPU cores, 4 GB|Unlimited|See [IOPS](/intl.en-US/Product Introduction/Product specifications/Primary instance types.mdsection_ire_dbl_kzm).|20GB-4000GB|
|rds.mssql.s3.large|4 CPU cores, 8 GB|
|rds.mssql.c1.large|8 CPU cores, 16 GB|
|rds.mssql.s2.xlarge|2 CPU cores, 8 GB|
|rds.mssql.m1.medium|4 CPU cores, 16 GB|
|rds.mssql.c1.xlarge|8 CPU cores, 32 GB|
|rds.mssql.c2.xlarge|16 CPU cores, 64 GB|
|Dedicated instance family|mssql.x4.medium.ro|2 CPU cores, 8 GB|
|mssql.x4.large.ro|4 CPU cores, 16 GB|
|mssql.x4.xlarge.ro|8 CPU cores, 32 GB|
|mssql.x4.2xlarge.ro|16 CPU cores, 64 GB|
|mssql.x4.4xlarge.ro|32 CPU cores, 128 GB|
|mssql.x4.8xlarge.ro|64 CPU cores, 256 GB|
|mssql.x8.medium.ro|2 CPU cores, 16 GB|
|mssql.x8.large.ro|4 CPU cores, 32 GB|
|mssql.x8.xlarge.ro|8 CPU cores, 64 GB|
|mssql.x8.2xlarge.ro|16 CPU cores, 128 GB|
|mssql.x8.4xlarge.ro|32 CPU cores, 256 GB|
|mssql.x8.7xlarge.ro|56 CPU cores, 480 GB|
|mssql.x8.8xlarge.ro|64 CPU cores, 512 GB|

## Read-only ApsaraDB RDS for PostgreSQL instances \(with local SSDs\)

|Category|PostgreSQL version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|--------|------------------|---------------|-------------|--------------|-------------------|------------|----------------|
|Read-only instance|10

|Dedicated instance family \(with a large memory capacity\)|pg.x8.xlarge.2|8 CPU cores, 64 GB|10000|18000|20GB-6000GB|
|pg.x8.2xlarge.2|16 CPU cores, 128 GB|12000|36000|
|Dedicated instance family \(with a large number of CPU cores\)|pg.x4.xlarge.2|8 CPU cores, 32 GB|5000|9000|
|pg.x4.2xlarge.2|16 CPU cores, 64 GB|10000|18000|
|pg.x4.4xlarge.2|32 CPU cores, 128 GB|12000|36000|
|Dedicated host instance family|rds.pg.st.h43|60 CPU cores, 470 GB|4000|50000|

## Read-only ApsaraDB RDS for PPAS instances

|Category|PPAS version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|--------|------------|---------------|-------------|--------------|-------------------|------------|----------------|
|Read-only instance|10

|General-purpose instance family|rds.ppas.t1.small|1 CPU core, 1 GB|100|1200|150GB|
|Dedicated instance family|ppas.x4.small.2|1 CPU core, 4 GB|200|5000|250GB|
|ppas.x4.medium.2|2 CPU cores, 8 GB|400|10000|
|ppas.x8.medium.2|2 CPU cores, 16 GB|2500|15000|
|ppas.x4.large.2|4 CPU cores, 16 GB|2500|20000|250GB/500GB|
|ppas.x8.large.2|4 CPU cores, 32 GB|5000|30000|
|ppas.x4.xlarge.2|8 CPU cores, 32 GB|5000|40000|500GB/1000GB|
|ppas.x8.xlarge.2|8 CPU cores, 64 GB|10000|60000|
|ppas.x4.2xlarge.2|16 CPU cores, 64 GB|10000|80000|1000GB/2000GB|
|ppas.x8.2xlarge.2|16 CPU cores, 128 GB|12000|120000|
|ppas.x4.4xlarge.2|32 CPU cores, 128 GB|12000|160000|2000GB/3000GB|
|ppas.x8.4xlarge.2|32 CPU cores, 256 GB|12000|240000|
|Dedicated host instance|rds.ppas.st.h43|60 CPU cores, 470 GB|12000|450000|3000GB/4000GB/5000GB/6000GB|


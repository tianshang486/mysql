---
keyword: [specifications, configuration]
---

# Primary instance types

This topic provides an overview of primary ApsaraDB RDS instance types. You can view the latest and historical specifications of each instance type.

ApsaraDB RDS allows you to create [read-only instances](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md) to scale the read capability of your database system. For more information about read-only instance types, see [Read-only instance types](/intl.en-US/Product Introduction/Product specifications/Read-only instance types.md).

After you select a primary instance type, you can [create an instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md) and perform subsequent operations.

## IOPS

The maximum input/output operations per second \(IOPS\) of an RDS instance equipped with local SSDs varies based on the instance type. The maximum IOPS of an RDS instance equipped with standard SSDs or enhanced SSDs \(ESSDs\) varies based on the instance type and storage capacity. The following table provides formulas to calculate the maximum IOPS of an RDS instance equipped with standard SSDs or ESSDs.

**Note:** If the throughput of an RDS instance equipped with standard SSDs or ESSDs reaches the upper limit, the IOPS of the RDS instance also decreases.

|Storage type|ESSD|Standard SSD|
|Performance level|PL3|PL2|PL1|-|
|------------|----|------------|
|-----------------|---|---|---|--|
|Maximum IOPS

\(The storage capacity is measured in GB.\)

|min\{1800 + 50 × Storage capacity, 1000000\}|min\{1800 + 50 × Storage capacity, 100000\}|min\{1800 + 50 × Storage capacity, 50000\}|min\{1800 + 30 × Storage capacity, 25000\}|

## Throughput

RDS instances equipped with standard SSDs or ESSDs are deployed on the sixth-generation ECS instances. In this situation, the maximum throughput of an RDS instance equipped with standard SSDs or ESSDs varies based on the ECS instance type. For more information, see [Storage I/O performance of the new generation of enterprise-level instance families](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

**Note:** If the IOPS of an RDS instance equipped with standard SSDs or ESSDs reaches the upper limit, the throughput of the RDS instance also decreases.

## Primary ApsaraDB RDS for MySQL instances

|RDS edition|PostgreSQL version|Instance family|Instance type|CPU and memory specifications|Maximum connections|Maximum IOPS|Storage capacity|
|-----------|------------------|---------------|-------------|-----------------------------|-------------------|------------|----------------|
|Basic|5.7, 8.0|General purpose instance families|mysql.n1.micro.1|1 core, 1 GB|2000|For more information, see the "IOPS" section in [Primary instance types]().|20GB-6000GB|
|mysql.n2.small.1|1 CPU core, 2 GB|2000|
|mysql.n2.medium.1|2 CPU cores, 4 GB|4000|
|mysql.n4.medium.1|2 CPU cores, 8 GB|6000|
|mysql.n4.large.1|4 CPU cores, 16 GB|8000|
|mysql.n4.xlarge.1|8 CPU cores, 32 GB|10000|
|High-availability Edition|5.5, 5.6, 5.7, and 8.0|General purpose instance families|rds.mysql.t1.small|1 core, 1 GB|300|600|5GB-2000GB|
|rds.mysql.s1.small|1 CPU core, 2 GB|600|1000|
|rds.mysql.s2.large|2 CPU cores, 4 GB|1200|2000|
|rds.mysql.s2.xlarge|2 CPU cores, 8 GB|2000|4000|
|rds.mysql.s3.large|4 CPU cores, 8 GB|2000|5000|
|rds.mysql.m1.medium|4 CPU cores, 16 GB|4000|7000|
|rds.mysql.c1.large|8 CPU cores, 16 GB|4000|8000|
|rds.mysql.c1.xlarge|8 CPU cores, 32 GB|8000|12000|
|rds.mysql.c2.xlarge|16 CPU cores, 64 GB|16000|14000|5GB-3000GB|
|rds.mysql.c2.xlp2|16 cores, 96 GB|24000|16000|
|rds.mysql.c2.2xlarge|16 CPU cores, 128 GB|32000|16000|
|Dedicated instance \(with a large memory size\)|mysql.x8.medium.2|2 CPU cores, 16 GB|2500|4500|50GB-1000GB|
|mysql.x8.large.2|4 CPU cores, 32 GB|5000|9000|50GB-1000GB|
|mysql.x8.xlarge.2|8 CPU cores, 64 GB|10000|18000|500GB-3000GB|
|mysql.x8.2xlarge.2|16 CPU cores, 128 GB|20000|36000|500GB-3000GB|
|mysql.x8.4xlarge.2|32 CPU cores, 256 GB|40000|72000|1000GB-6000GB|
|mysql.x8.8xlarge.2|64 CPU cores, 512 GB|80000|144000|1000GB-6000GB|
|Dedicated instance \(with a large number of CPU cores\)|mysql.x4.large.2|4 CPU cores, 16 GB|2500|4500|50GB-2000GB|
|mysql.x4.xlarge.2|8 CPU cores, 32 GB|5000|9000|500GB-3000GB|
|mysql.x4.2xlarge.2|16 CPU cores, 64 GB|10000|18000|500GB-3000GB|
|mysql.x4.4xlarge.2|32 CPU cores, 128 GB|20000|36000|1000GB-6000GB|
|Dedicated host|rds.mysql.st.h43|60 CPU cores, 470 GB|100000|120000|3000GB/4000GB/5000GB/6000GB|
|rds.mysql.st.v52|90 cores, 720 GB|100000|140000|1000GB-6000GB|
|Supported for the RDS Enterprise Edition|5.7, 8.0|General purpose instance families|mysql.n2.small.25|1 CPU core, 2 GB|600|1000|5GB-2000GB|
|mysql.n2.medium.25|2 CPU cores, 4 GB|1200|2000|5GB-2000GB|
|mysql.n4.medium.25|2 CPU cores, 8 GB|2000|4000|5GB-2000GB|
|mysql.n2.large.25|4 CPU cores, 8 GB|2000|5000|5GB-2000GB|
|mysql.n4.large.25|4 CPU cores, 16 GB|4000|7000|5GB-2000GB|
|mysql.n2.xlarge.25|8 CPU cores, 16 GB|4000|8000|5GB-2000GB|
|mysql.n4.xlarge.25|8 CPU cores, 32 GB|8000|12000|5GB-2000GB|
|mysql.n4.2xlarge.25|16 CPU cores, 64 GB|16000|14000|5GB-3000GB|
|mysql.n8.2xlarge.25|16 CPU cores, 128 GB|32000|16000|5GB-3000GB|
|Dedicated instance \(with a large number of CPU cores\)|mysql.x4.large.25|4 CPU cores, 16 GB|2500|4500|50GB-2000GB|
|mysql.x4.xlarge.25|8 CPU cores, 32 GB|5000|9000|500GB-3000GB|
|mysql.x4.2xlarge.25|16 CPU cores, 64 GB|10000|18000|500GB-3000GB|
|mysql.x4.4xlarge.25|32 CPU cores, 128 GB|20000|36000|1000GB-6000GB|
|Dedicated instance \(with a large memory capacity\)|mysql.x8.medium.25|2 CPU cores, 16 GB|2500|4500|50GB-2000GB|
|mysql.x8.large.25|4 CPU cores, 32 GB|5000|9000|50GB-2000GB|
|mysql.x8.xlarge.25|8 CPU cores, 64 GB|10000|18000|500GB-3000GB|
|mysql.x8.2xlarge.25|16 CPU cores, 128 GB|20000|36000|500GB-3000GB|
|mysql.x8.4xlarge.25|32 CPU cores, 256 GB|40000|72000|1000GB-6000GB|
|Dedicated host instance|mysql.st.8xlarge.25|60 CPU cores, 470 GB|100000|120000|3000GB/4000GB/5000GB/6000GB|
|mysql.st.12xlarge.25|90 cores, 720 GB|100000|140000|1000GB-6000GB|

## Primary ApsaraDB RDS for SQL Server instances

|RDS edition|SQL Server version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-----------|------------------|---------------|-------------|--------------|-------------------|------------|----------------|
|Basic Edition|2012 EE|General-purpose instance|rds.mssql.s2.large|2 cores, 4 GB|Unlimited|See [IOPS]().|20 GB to 3,000 GB|
|rds.mssql.s2.xlarge|2 cores, 8 GB|
|rds.mssql.s3.large|4 cores, 8 GB|
|rds.mssql.m1.medium|4 cores, 16 GB|
|rds.mssql.c1.large|8 cores, 16 GB|
|rds.mssql.c1.xlarge|8 cores, 32 GB|
|rds.mssql.c2.xlarge|16 cores, 64 GB|
|2012 Web and 2016 Web|Dedicated instance|mssql.x2.medium.w1|2 cores, 4 GB|Unlimited|See [IOPS]().|20 GB to 3,000 GB|
|mssql.x4.medium.w1|2 cores, 8 GB|
|mssql.x2.large.w1|4 cores, 8 GB|
|mssql.x4.large.w1|4 cores, 16 GB|
|mssql.x2.xlarge.w1|8 cores, 16 GB|
|mssql.x4.xlarge.w1|8 cores, 32 GB|
|mssql.x2.2xlarge.w1|16 cores, 32 GB|
|mssql.x4.2xlarge.w1|16 cores, 64 GB|
|High-availability Edition|2008 R2|General-purpose instance|rds.mssql.s2.large|2 cores, 4 GB|1,200|2,000|10 GB to 2,000 GB|
|rds.mssql.s2.xlarge|2 cores, 8 GB|2,000|4,000|
|rds.mssql.s3.large|4 cores, 8 GB|2,000|5,000|
|rds.mssql.m1.medium|4 cores, 16 GB|4,000|7,000|
|rds.mssql.c1.large|8 cores, 16 GB|4,000|8,000|
|rds.mssql.c1.xlarge|8 cores, 32 GB|8,000|12,000|
|rds.mssql.c2.xlarge|16 cores, 64 GB|16,000|14,000|
|Dedicated instance|mssql.x8.medium.2|2 cores, 16 GB|2,500|4,500|250 GB|
|mssql.x8.large.2|4 cores, 32 GB|5,000|9,000|500 GB|
|mssql.x8.xlarge.2|8 cores, 64 GB|10,000|18,000|1,000 GB|
|mssql.x8.2xlarge.2|16 cores, 128 GB|20,000|36,000|2,000 GB|
|Dedicated host|rds.mssql.st.d13|30 cores, 220 GB|64,000|20,000|2,000 GB|
|rds.mssql.st.h43|60 cores, 470 GB|100,000|50,000|2,000 GB|
|2008 R2 with SSD, 2012 EE and 2016 EE|Dedicated instance|mssql.x4.medium.e2|2 cores, 8 GB|Unlimited|See [IOPS]().|20 GB to 4,000 GB|
|mssql.x8.medium.e2|2 cores, 16 GB|
|mssql.x4.large.e2|4 cores, 16 GB|
|mssql.x8.large.e2|4 cores, 32 GB|
|mssql.x4.xlarge.e2|8 cores, 32 GB|
|mssql.x8.xlarge.e2|8 cores, 64 GB|
|mssql.x4.2xlarge.e2|16 cores, 64 GB|
|mssql.x8.2xlarge.e2|16 cores, 128 GB|
|mssql.x4.3xlarge.e2|24 cores, 96 GB|
|mssql.x4.4xlarge.e2|32 cores, 128 GB|
|mssql.x8.4xlarge.e2|32 cores, 256 GB|
|mssql.x8.7xlarge.e2|56 cores, 480 GB|
|mssql.x4.8xlarge.e2|64 cores, 256 GB|
|mssql.x8.8xlarge.e2|64 cores, 512 GB|
|2012 SE, 2016 SE, 2017 SE and 2019 SE|General-purpose instance|mssql.s2.medium.s2|2 cores, 4 GB|
|mssql.s2.large.s2|4 cores, 8 GB|
|mssql.s2.xlarge.s2|8 cores, 16 GB|
|mssql.s2.2xlarge.s2|16 cores, 32 GB|
|mssql.s4.2xlarge.s2|16 cores, 64 GB|
|mssql.s8.2xlarge.s2|16 cores, 128 GB|
|Dedicated instance|mssql.x4.medium.s2|2 cores, 8 GB|
|mssql.x8.medium.s2|2 cores, 16 GB|
|mssql.x4.large.s2|4 cores, 16 GB|
|mssql.x8.large.s2|4 cores, 32 GB|
|mssql.x4.xlarge.s2|8 cores, 32 GB|
|mssql.x8.xlarge.s2|8 cores, 64 GB|
|mssql.x4.2xlarge.s2|16 cores, 64 GB|
|mssql.x8.2xlarge.s2|16 cores, 128 GB|
|mssql.x4.3xlarge.s2|24 cores, 96 GB|
|Cluster Edition|2017 EE|Dedicated instance|mssql.x4.medium.e2|2 cores, 8 GB|Unlimited|See [IOPS]().|20 GB to 4,000 GB|
|mssql.x4.large.e2|4 cores, 16 GB|
|mssql.x4.xlarge.e2|8 cores, 32 GB|
|mssql.x4.2xlarge.e2|16 cores, 64 GB|
|mssql.x4.4xlarge.e2|32 cores, 128 GB|
|mssql.x4.8xlarge.e2|64 cores, 256 GB|
|mssql.x8.medium.e2|2 cores, 16 GB|
|mssql.x8.large.e2|4 cores, 32 GB|
|mssql.x8.xlarge.e2|8 cores, 64 GB|
|mssql.x8.2xlarge.e2|16 cores, 128 GB|
|mssql.x8.4xlarge.e2|32 cores, 256 GB|
|mssql.x8.8xlarge.e2|64 cores, 512 GB|

## Primary ApsaraDB RDS for PostgreSQL instances \(with local SSDs\)

|RDS edition|PostgreSQL version|Instance family|Instance type|CPU and memory specifications|Maximum number of connections|Maximum IOPS|Storage capacity|
|-----------|------------------|---------------|-------------|-----------------------------|-----------------------------|------------|----------------|
|High-availability Edition|9.4 and 10

|General-purpose instance|rds.pg.s1.small|1 CPU core, 2 GB|200|1,000|20 GB to 6,000 GB|
|rds.pg.s2.large|2 CPU cores, 4 GB|400|2,000|
|rds.pg.s3.large|4 CPU cores, 8 GB|800|5,000|
|rds.pg.c1.large|8 CPU cores, 16 GB|1,500|8,000|
|rds.pg.c1.xlarge|8 CPU cores, 32 GB|2,000|12,000|
|rds.pg.c2.xlarge|16 CPU cores, 64 GB|2,000|14,000|
|Dedicated instance \(with a large memory capacity\)|pg.x8.medium.2|2 CPU cores, 16 GB|2,500|4,500|
|pg.x8.large.2|4 CPU cores, 32 GB|5,000|9,000|
|pg.x8.xlarge.2|8 CPU cores, 64 GB|10,000|18,000|
|pg.x8.2xlarge.2|16 CPU cores, 128 GB|12,000|36,000|
|Dedicated host instance|rds.pg.st.h43|60 CPU cores, 470 GB|4,000|50,000|

## Primary ApsaraDB RDS for PostgreSQL instances \(with standard or enhanced SSDs\)

|RDS edition|PostgreSQL version|Instance family|Instance type|CPU and memory specifications|Maximum number of connections|Maximum IOPS|Storage capacity|
|-----------|------------------|---------------|-------------|-----------------------------|-----------------------------|------------|----------------|
|Basic Edition|10, 11, and 12|General-purpose instance|pg.n2.small.1|1 CPU core, 2 GB|200|For more information, see the "IOPS" section in [Primary instance types]().|Standard SSD: 20 GB to 6,000 GB

Enhanced SSD: 50 GB to 32,000 GB |
|pg.n2.medium.1|2 CPU cores, 4 GB|400|
|pg.n4.medium.1|2 CPU cores, 8 GB|800|
|pg.n2.large.1|4 CPU cores, 8 GB|800|
|pg.n4.large.1|4 CPU cores, 16 GB|1,600|
|pg.n2.xlarge.1|8 CPU cores, 16 GB|1,600|
|pg.n4.xlarge.1|8 CPU cores, 32 GB|3,200|
|pg.n2.2xlarge.1|16 CPU cores, 32 GB|3,200|
|pg.n4.2xlarge.1|16 CPU cores, 64 GB|6,400|
|pg.n8.2xlarge.1|16 CPU cores, 128 GB|10,000|
|pg.n4.4xlarge.1|32 CPU cores, 128 GB|12,800|
|pg.n8.4xlarge.1|32 CPU cores, 256 GB|20,000|
|pg.n4.8xlarge.1|56 CPU cores, 224 GB|22,000|
|pg.n8.8xlarge.1|56 CPU cores, 480 GB|48,000|
|High-availability Edition|10, 11, and 12

|General-purpose instance|pg.n2.small.2c|1 CPU core, 2 GB|50|For more information, see the "IOPS" section in [Primary instance types]().|Standard SSD: 20 GB to 6,000 GB

Fully encrypted standard SSD: 50 GB to 6,000GB

Enhanced SSD: 50 GB to 32,000 GB

Enhanced SSD of PL2: 500 GB to 32,000 GB

Enhanced SSD of PL3: 1,500 GB to 32,000 GB |
|pg.n2.medium.2c|2 CPU core, 4 GB|100|
|Dedicated instance|pg.x2.medium.2c|2 CPU cores, 4 GB|400|
|pg.x4.medium.2c|2 CPU cores, 8 GB|800|
|pg.x8.medium.2c|2 CPU cores, 16 GB|1,600|
|pg.x2.large.2c|4 CPU cores, 8 GB|800|
|pg.x4.large.2c|4 CPU cores, 16 GB|1,600|
|pg.x8.large.2c|4 CPU cores, 32 GB|3,200|
|pg.x2.xlarge.2c|8 CPU cores, 16 GB|1,600|
|pg.x4.xlarge.2c|8 CPU cores, 32 GB|3,200|
|pg.x8.xlarge.2c|8 CPU cores, 64 GB|6,400|
|pg.x2.3large.2c|12 CPU cores, 24 GB|2,400|
|pg.x4.3large.2c|12 CPU cores, 48 GB|4,800|
|pg.x8.3large.2c|12 CPU cores, 96 GB|9,600|
|pg.x2.2xlarge.2c|16 CPU cores, 32 GB|3,200|
|pg.x4.2xlarge.2c|16 CPU cores, 64 GB|6,400|
|pg.x8.2xlarge.2c|16 CPU cores, 128 GB|12,800|
|pg.x2.3xlarge2c|24 CPU cores, 48 GB|4,800|
|pg.x4.3xlarge.2c|24 CPU cores, 96 GB|9,600|
|pg.x8.3xlarge.2c|24 CPU cores, 192 GB|19,200|
|pg.x2.4xlarge.2c|32 CPU cores, 64 GB|6,400|
|pg.x4.4xlarge.2c|32 CPU cores, 128 GB|12,800|
|pg.x8.4xlarge.2c|32 CPU cores, 256 GB|25,600|
|pg.x2.13large.2c|52 CPU cores, 104 GB|10,400|
|pg.x4.13large.2c|52 CPU cores, 192 GB|19,200|
|pg.x8.13large.2c|52 CPU cores, 384 GB|38,400|
|pg.x2.8xlarge.2c|64 CPU cores, 128 GB|12,800|
|pg.x4.8xlarge.2c|64 CPU cores, 256 GB|25,600|
|pg.x8.8xlarge.2c|64 CPU cores, 512 GB|51,200|
|pg.x2.13xlarge.2c|104 CPU cores, 192 GB|19,200|
|pg.x4.13xlarge.2c|104 CPU cores, 384 GB|38,400|
|pg.x8.13xlarge.2c|104 CPU cores, 768 GB|76,800|

## ApsaraDB RDS for PPAS instances

|RDS edition|PPAS version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-----------|------------|---------------|-------------|--------------|-------------------|------------|----------------|
|High-availability Edition|10

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

## ApsaraDB RDS for MariaDB TX instances

|RDS edition|Instance family|Instance type|CPU and memory|Maximum connections|Storage|
|Maximum IOPS|Storage capacity|
|-----------|---------------|-------------|--------------|-------------------|-------|
|------------|----------------|
|High-availability Edition|General-purpose instance|mariadb.n2.small.2c|1 core, 2 GB|2,000|See [IOPS]().|20 GB to 1,000 GB|
|mariadb.n2.medium.2c|2 cores, 4 GB|4,000|
|Dedicated instance|mariadb.x2.large.2c|4 cores, 8 GB|6,000|20 GB to 6,000 GB|
|mariadb.x4.large.2c|4 cores, 16 GB|8,000|
|mariadb.x2.xlarge.2c|8 cores, 16 GB|8,000|
|mariadb.x4.xlarge.2c|8 cores, 32 GB|10,000|
|mariadb.x2.2xlarge.2c|16 cores, 32 GB|10,000|
|mariadb.x4.2xlarge.2c|16 cores, 64 GB|15,000|
|mariadb.x8.2xlarge.2c|16 cores, 128 GB|20,000|
|mariadb.x4.4xlarge.2c|32 cores, 128 GB|20,000|
|mariadb.x8.4xlarge.2c|32 cores, 256 GB|64,000|
|Dedicated host|mariadb.x4.8xlarge.2c|56 cores, 224 GB|64,000|
|mariadb.x8.8xlarge.2c|56 cores, 480 GB|100,000|

## Phased-out ApsaraDB RDS for MySQL instance types

The following table lists phased-out ApsaraDB RDS for MySQL instance types. These instance types are no longer available to new instances.

|Instance type|CPU cores|Memory capacity|Maximum connections|Maximum IOPS|
|-------------|---------|---------------|-------------------|------------|
|rds.mys2.small|2|240 MB|60|150|
|rds.mys2.mid|4|600 MB|150|300|
|rds.mys2.standard|6|1,200 MB|300|600|
|rds.mys2.large|8|2,400 MB|600|1,200|
|rds.mys2.xlarge|9|6,000 MB|1,500|3,000|
|rds.mys2.2xlarge|10|12,000 MB|2,000|6,000|
|rds.mys2.4xlarge|11|24,000 MB|2,000|12,000|
|rds.mys2.8xlarge|13|48,000 MB|2,000|14,000|
|rds.mysql.st.d13|30|220 GB|64,000|20,000|
|mysql.x8.medium.3|2|16 GB|2,500|4,500|
|mysql.x4.large.3|4|16 GB|2,500|4,500|
|mysql.x8.large.3|4|32 GB|5,000|9,000|
|mysql.x4.xlarge.3|8|32 GB|5,000|9,000|
|mysql.x8.xlarge.3|8|64 GB|10,000|18,000|
|mysql.x4.2xlarge.3|16|64 GB|10,000|18,000|
|mysql.x8.2xlarge.3|16|128 GB|20,000|36,000|
|mysql.x4.4xlarge.3|32|128 GB|20,000|36,000|
|mysql.x8.4xlarge.3|32|256 GB|40,000|72,000|
|mysql.st.8xlarge.3|60|470 GB|100,000|120,000|
|mysql.n2.2xlarge.1|16|32 GB|10,000|See [IOPS](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|
|mysql.n4.2xlarge.1|16|64 GB|15,000|
|mysql.n8.2xlarge.1|16|128 GB|20,000|
|mysql.x2.3xlarge2c|24|48 GB|24,000|
|mysql.n4.4xlarge.1|32|128 GB|20,000|
|mysql.n8.4xlarge.1|32|256 GB|64,000|
|mysql.n4.8xlarge.1|56|224 GB|64,000|
|mysql.n8.8xlarge.1|56|480 GB|64,000|

## Phased-out ApsaraDB RDS for SQL Server instance types

The following table lists phased-out ApsaraDB RDS for SQL Server instance types. These instance types are no longer available to new instances.

|Instance type|CPU cores|Memory capacity|Maximum connections|Maximum IOPS|
|-------------|---------|---------------|-------------------|------------|
|rds.mssql.s1.small|1|2 GB|600|1,000|
|rds.mss1.small|6|1,000 MB|100|500|
|rds.mss1.mid|8|2,000 MB|200|1,000|
|rds.mss1.standard|9|4,000 MB|400|2,000|
|rds.mss1.large|10|6,000 MB|600|3,000|
|rds.mss1.xlarge|11|8,000 MB|800|4,000|
|rds.mss1.2xlarge|12|12,000 MB|1,200|6,000|
|rds.mss1.4xlarge|13|24,000 MB|2,000|12,000|
|rds.mss1.8xlarge|13|48,000 MB|2,000|14,000|
|rds.mssql.c2.xlp2|16|96 GB|24,000|16,000|
|pg.n1.micro.1|1|1 GB|100|See [IOPS](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|

## Phased-out instance types of ApsaraDB RDS for PostgreSQL

The following table describes the phased-out instance types of ApsaraDB RDS for PostgreSQL. These instance types are no longer available to new instances.

|Instance type|CPU cores|Memory capacity|Maximum connections|Maximum IOPS|
|-------------|---------|---------------|-------------------|------------|
|rds.pg.t1.small|1|1GB|100|600|
|pg.x8.4xlarge.2|32|256GB|20000|50000|
|pg.n1.micro.1|1|1GB|100|See [IOPS](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).|
|pg.gn5i-c2g1.large.1|2|8 GB|800|
|pg.gn5i-c4g1.xlarge.1|4|16 GB|1,600|
|pg.gn5i-c8g1.2xlarge.1|8|32 GB|3,200|
|pg.gn5i-c16g1.4xlarge.1|16|64 GB|6,400|
|pg.gn5i-c16g1.8xlarge.1|32|128 GB|12,800|
|pg.gn5i-c28g1.14xlarge.1|56|224 GB|22,000|

## Phased-out ApsaraDB RDS for PPAS instance types

The following table lists phased-out ApsaraDB RDS for PPAS instance types. These instance types are no longer available to new instances.

|Instance type|CPU cores|Memory capacity|Maximum connections|Maximum IOPS|
|-------------|---------|---------------|-------------------|------------|
|rds.ppas.s1.small|1|2 GB|200|1,000|
|rds.ppas.s2.large|2|4 GB|400|2,000|
|rds.ppas.s3.large|4|8 GB|800|5,000|
|rds.ppas.m1.medium|4|16 GB|1,500|8,000|
|rds.ppas.c1.xlarge|8|32 GB|2,000|12,000|
|rds.ppas.c2.xlarge|16|64 GB|2,000|14,000|
|rds.pg.c2.2xlarge|16|128 GB|3,000|16,000|

## FAQ

Why does an entry-level RDS instance support a larger maximum number of connections and deliver higher IOPS than an enterprise-level RDS instance when the instances have the same CPU cores and memory capacity?

The entry-level RDS instance belongs to the shared or general-purpose instance family, whereas the enterprise-level RDS instance belongs to the dedicated instance family. The shared and general-purpose instance families reuse CPU resources. This allows the entry-level RDS instance to support a larger maximum number of connections and deliver higher IOPS. However, the dedicated instance family uses exclusive CPU and memory resources. This allows the enterprise-level RDS instance to run more stably. For more information, see [Instance families](/intl.en-US/Product Introduction/Product specifications/Instance families.md).


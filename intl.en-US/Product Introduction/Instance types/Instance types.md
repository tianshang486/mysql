# Instance types {#reference_lbw_tyw_5db .reference}

## ApsaraDB RDS for MySQL {#section_f33_wwz_xdb .section}

|Edition|Version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-------|-------|---------------|-------------|--------------|-------------------|------------|----------------|
|Basic Edition|5.7 or 8.0|General-purpose|mysql.n1.micro.1|1 core, 1 GB|2,000|min\{30 × Storage capacity, 20,000\}|20 GB to 6,000 GB|
|mysql.n2.small.1|1 core, 2 GB|2,000|
|mysql.n2.medium.1|2 cores, 4 GB|4,000|
|mysql.n4.medium.1|2 cores, 8 GB|6,000|
|mysql.n4.large.1|4 cores, 16 GB|8,000|
|mysql.n4.xlarge.1|8 cores, 32 GB|10,000|
|mysql.n4.2xlarge.1|16 cores, 64 GB|15,000|
|mysql.n4.4xlarge.1|32 cores, 128 GB|20,000|
|mysql.n8.4xlarge.1|32 cores, 256 GB|64,000|
|mysql.n4.8xlarge.1|56 cores, 224 GB|64,000|
|mysql.n8.8xlarge.1|56 cores, 480 GB|64,000|
|High-availability Edition|5.5, 5.6, 5.7, or 8.0|General-purpose|rds.mysql.t1.small|1 core, 1 GB|300|600|5 GB to 2,000 GB|
|rds.mysql.s1.small|1 core, 2 GB|600|1,000|
|rds.mysql.s2.large|2 cores, 4 GB|1,200|2,000|
|rds.mysql.s2.xlarge|2 cores, 8 GB|2,000|4,000|
|rds.mysql.s3.large|4 cores, 8 GB|2,000|5,000|
|rds.mysql.m1.medium|4 cores, 16 GB|4,000|7,000|
|rds.mysql.c1.large|8 cores, 16 GB|4,000|8,000|
|rds.mysql.c1.xlarge|8 cores, 32 GB|8,000|12,000|
|rds.mysql.c2.xlarge|16 cores, 64 GB|16,000|14,000|5 GB to 3,000 GB|
|rds.mysql.c2.xlp2|16 cores, 96 GB|24,000|16,000|
|Dedicated instance \(with high memory\)|mysql.x8.medium.2|2 cores, 16 GB|2,500|4,500|250 GB|
|mysql.x8.large.2|4 cores, 32 GB|5,000|9,000|500 GB|
|mysql.x8.xlarge.2|8 cores, 64 GB|10,000|18,000|1,000 GB or 2,000 GB|
|mysql.x8.2xlarge.2|16 cores, 128 GB|20,000|36,000|2,000 GB or 3,000 GB|
|Dedicated instance \(with high CPU\)|mysql.x4.large.2|4 cores, 16 GB|2,500|4,500|250 GB or 500 GB|
|mysql.x4.xlarge.2|8 cores, 32 GB|5,000|9,000|500 GB, 1,000 GB, or 2,000 GB|
|mysql.x4.2xlarge.2|16 cores, 64 GB|10,000|18,000|1,000 GB, 2,000 GB, or 3,000 GB|
|mysql.x4.4xlarge.2|32 cores, 128 GB|20,000|36,000|2,000 GB or 3,000 GB|
|Dedicated host|rds.mysql.st.h43|60 cores, 470 GB|100,000|50,000|3,000 GB, 4,000 GB, 5,000 GB, or 6,000 GB|
|Read-only instance|5.6, 5.7, or 8.0|General-purpose|rds.mysql.t1.small|1 core, 1 GB|300|600|5 GB to 2,000 GB|
|rds.mysql.s1.small|1 core, 2 GB|600|1,000|
|rds.mysql.s2.large|2 cores, 4 GB|1,200|2,000|
|rds.mysql.s2.xlarge|2 cores, 8 GB|2,000|4,000|
|rds.mysql.s3.large|4 cores, 8 GB|2,000|5,000|
|rds.mysql.m1.medium|4 cores, 16 GB|4,000|7,000|
|rds.mysql.c1.large|8 cores, 16 GB|4,000|8,000|
|rds.mysql.c1.xlarge|8 cores, 32 GB|8,000|12,000|
|rds.mysql.c2.xlarge|16 cores, 64 GB|16,000|14,000|5 GB to 3,000 GB|
|rds.mysql.c2.xlp2|16 cores, 96 GB|24,000|16,000|
|Dedicated instance \(with high memory\)|mysqlro.x8.medium.1|2 cores, 16 GB|2,500|4,500|250 GB|
|mysqlro.x8.large.1|4 cores, 32 GB|5,000|9,000|500 GB|
|mysqlro.x8.xlarge.1|8 cores, 64 GB|10,000|18,000|1,000 GB or 2,000 GB|
|mysqlro.x8.2xlarge.1|16 cores, 128 GB|20,000|36,000|2,000 GB or 3,000 GB|
|Dedicated instance \(with high CPU\)|mysqlro.x4.large.1|4 cores, 16 GB|2,500|4,500|250 GB or 500 GB|
|mysqlro.x4.xlarge.1|8 cores, 32 GB|5,000|9,000|500 GB, 1,000 GB, or 2,000 GB|
|mysqlro.x4.2xlarge.1|16 cores, 64 GB|10,000|18,000|1,000 GB, 2,000 GB, or 3,000 GB|
|mysqlro.x4.4xlarge.1|32 cores, 128 GB|20,000|36,000|2,000 GB or 3,000 GB|

## ApsaraDB RDS for SQL Server primary instance {#section_bi5_oit_d93 .section}

|Edition|Version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-------|-------|---------------|-------------|--------------|-------------------|------------|----------------|
|Basic Edition|2012 Enterprise Edition|General-purpose|rds.mssql.s2.large|2 cores, 4 GB|Not limited|min\{30 × Storage capacity, 20,000\}|20 GB to 3,000 GB|
|rds.mssql.s2.xlarge|2 cores, 8 GB|
|rds.mssql.s3.large|4 cores, 8 GB|
|rds.mssql.m1.medium|4 cores, 16 GB|
|rds.mssql.c1.large|8 cores, 16 GB|
|rds.mssql.c1.xlarge|8 cores, 32 GB|
|rds.mssql.c2.xlarge|16 cores, 64 GB|
|2012 Web Edition and 2016 Web Edition|Dedicated instance|mssql.x2.medium.w1|2 cores, 4 GB|Not limited|min\{30 × Storage capacity, 20,000\}|20 GB to 3,000 GB|
|mssql.x4.medium.w1|2 cores, 8 GB|
|mssql.x2.large.w1|4 cores, 8 GB|
|mssql.x4.large.w1|4 cores, 16 GB|
|mssql.x2.xlarge.w1|8 cores, 16 GB|
|mssql.x4.xlarge.w1|8 cores, 32 GB|
|mssql.x2.2xlarge.w1|16 cores, 32 GB|
|mssql.x4.2xlarge.w1|16 cores, 64 GB|
|High-availability Edition|2008 R2|General-purpose|rds.mssql.s2.large|2 cores, 4 GB|1,200|2,000|10 GB to 2,000 GB|
|rds.mssql.s2.xlarge|2 cores, 8 GB|2,000|4,000|
|rds.mssql.s3.large|4 cores, 8 GB|2,000|5,000|
|rds.mssql.m1.medium|4 cores, 16 GB|4,000|7,000|
|rds.mssql.c1.large|8 cores, 16 GB|4,000|8,000|
|rds.mssql.c1.xlarge|8 cores, 32 GB|8,000|12,000|
|rds.mssql.c2.xlarge|16 cores, 64 GB|16,000|14,000|
|rds.mssql.c2.xlp2|16 cores, 96 GB|24,000|16,000|
|Dedicated instance|mssql.x8.medium.2|2 cores, 16 GB|2,500|4,500|250 GB|
|mssql.x8.large.2|4 cores, 32 GB|5,000|9,000|500 GB|
|mssql.x8.xlarge.2|8 cores, 64 GB|10,000|18,000|1,000 GB|
|mssql.x8.2xlarge.2|16 cores, 128 GB|20,000|36,000|2,000 GB|
|Dedicated host|rds.mssql.st.d13|30 cores, 220 GB|64,000|20,000|2,000 GB|
|rds.mssql.st.h43|60 cores, 470 GB|100,000|50,000|2,000 GB|
|2012 Enterprise Edition and 2016 Enterprise Edition|Dedicated instance|mssql.x4.medium.e2|2 cores, 8 GB|Not limited|Dependent on the performance of cloud disks|20 GB to 4,000 GB|
|mssql.x8.medium.e2|2 cores, 16 GB|
|mssql.x4.large.e2|4 cores, 16 GB|
|mssql.x8.large.e2|4 cores, 32 GB|
|mssql.x4.xlarge.e2|8 cores, 32 GB|
|mssql.x8.xlarge.e2|8 cores, 64 GB|
|mssql.x4.2xlarge.e2|16 cores, 64 GB|
|mssql.x8.2xlarge.e2|16 cores, 128 GB|
|mssql.x4.3xlarge.e2|24 cores, 96 GB|
|mssql.x4.4xlarge.e2|32 cores,128 GB|
|mssql.x8.4xlarge.e2|32 cores, 256 GB|
|mssql.x8.7xlarge.e2|56 cores, 480 GB|
|mssql.x4.8xlarge.e2|64 cores, 256 GB|
|mssql.x8.8xlarge.e2|64 cores, 512 GB|
|2012 Standard Edition and 2016 Standard Edition|General-purpose|mssql.s2.medium.s2|2 cores, 4 GB|
|mssql.s2.large.s2|4 cores, 8 GB|
|mssql.s2.xlarge.s2|8 cores, 16 GB|
|mssql.s2.2xlarge.s2|16 cores, 32 GB|
|Dedicated instance|mssql.x4.medium.s2|2 cores, 8 GB|
|mssql.x8.medium.s2|2 cores, 16 GB|
|mssql.x4.large.s2|4 cores, 16 GB|
|mssql.x8.large.s2|4 cores, 32 GB|
|mssql.x4.xlarge.s2|8 cores, 32 GB|
|mssql.x8.xlarge.s2|8 cores, 64 GB|
|mssql.x4.2xlarge.s2|16 cores, 64 GB|
|mssql.x8.2xlarge.s2|16 cores, 128 GB|
|mssql.x4.3xlarge.s2|24 cores, 96 GB|
|Cluster Edition|2017 Enterprise Edition|Dedicated instance|mssql.x4.medium.e2|2 cores, 8 GB|Not limited|Dependent on the performance of cloud disks|20 GB to 4,000 GB|
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

## ApsaraDB RDS for SQL Server read-only instance {#section_eg1_3ph_wfb .section}

|Edition|Version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-------|-------|---------------|-------------|--------------|-------------------|------------|----------------|
|Cluster Edition|2017 Enterprise Edition|General-purpose|rds.mssql.s2.large|2 cores, 4 GB|Not limited|Dependent on the performance of cloud disks|20 GB to 4,000 GB|
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

## ApsaraDB RDS for PostgreSQL primary instance or read-only instance \(based on local disks\) {#section_xe8_op0_gyq .section}

|Edition|Version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-------|-------|---------------|-------------|--------------|-------------------|------------|----------------|
|High-availability Edition| 9.4

 |General-purpose|rds.pg.t1.small|1 core, 1 GB|100|600|5 GB to 2,000 GB|
|rds.pg.s1.small|1 core, 2 GB|200|1,000|
|rds.pg.s2.large|2 cores, 4 GB|400|2,000|
|rds.pg.s3.large|4 cores, 8 GB|800|5,000|
|rds.pg.c1.xlarge|8 cores, 32 GB|2,000|12,000|
|rds.pg.c2.xlarge|16 cores, 64 GB|2,000|14,000|
|Dedicated instance \(with high memory\)|pg.x8.medium.2|2 cores, 16 GB|2,500|4,500|250 GB|
|pg.x8.large.2|4 cores, 32 GB|5,000|9,000|500 GB|
|pg.x8.xlarge.2|8 cores, 64 GB|10,000|18,000|1,000 GB|
|pg.x8.2xlarge.2|16 cores, 128 GB|12,000|36,000|2,000 GB|
|Dedicated instance \(with high CPU\)|pg.x4.large.2|4 cores, 16 GB|2,500|4,500|250 GB or 500 GB|
|pg.x4.xlarge.2|8 cores, 32 GB|5,000|9,000|500 GB or 1,000 GB|
|pg.x4.2xlarge.2|16 cores, 64 GB|10,000|18,000|1,000 GB or 2,000 GB|
|pg.x4.4xlarge.2|32 cores, 128 GB|12,000|36,000|2,000 GB or 3,000 GB|
|Dedicated host|rds.pg.st.d13|30 cores, 220 GB|4,000|20,000|3,000 GB|
|rds.pg.st.h43|60 cores, 470 GB|4,000|50,000|3,000 GB, 4,000 GB, 5,000 GB, or 6,000 GB|

## ApsaraDB RDS for PostgreSQL primary instance \(based on cloud disks\) {#section_cq5_z2p_d3b .section}

|Edition|Version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-------|-------|---------------|-------------|--------------|-------------------|------------|----------------|
|Basic Edition|10|General-purpose|pg.n1.micro.1|1 core, 1 GB|100|min\{1,200 + 30 × Storage capacity, 20,000\}|20 GB to 6,000 GB|
|pg.n2.small.1|1 core, 2 GB|200|
|pg.n2.medium.1|2 cores, 4 GB|400|
|pg.n4.medium.1|2 cores, 8 GB|800|
|pg.n2.large.1|4 cores, 8 GB|800|
|pg.n4.large.1|4 cores, 16 GB|1,600|
|pg.n2.xlarge.1|8 cores, 16 GB|1,600|
|pg.n4.xlarge.1|8 cores, 32 GB|3,200|
|pg.n2.2xlarge.1|16 cores, 32 GB|3,200|
|pg.n4.2xlarge.1|16 cores, 64 GB|6,400|
|pg.n8.2xlarge.1|16 cores, 128 GB|10,000|
|pg.n4.4xlarge.1|32 cores, 128 GB|12,800|
|pg.n8.4xlarge.1|32 cores, 256 GB|20,000|
|pg.n4.8xlarge.1|56 cores, 224 GB|22,000|
|pg.n8.8xlarge.1|56 cores, 480 GB|48,000|
|pg.n2.medium.2c|2 cores, 4 GB|100|
|Dedicated instance|pg.x2.large.2c|4 cores, 8 GB|200|
|pg.x4.large.2c|4 cores, 16 GB|400|
|pg.x2.xlarge.2c|8 cores, 16 GB|400|
|pg.x4.xlarge.2c|8 cores, 32 GB|800|
|pg.x2.2xlarge.2c|16 cores, 32 GB|800|
|pg.x4.2xlarge.2c|16 cores, 64 GB|1,600|
|pg.x8.2xlarge.2c|16 cores, 128 GB|3,200|
|pg.x4.4xlarge.2c|32 cores, 128 GB|3,200|
|pg.x8.4xlarge.2c|32 cores, 256 GB|6,400|
|pg.x4.8xlarge.2c|56 cores, 224 GB|5,600|
|pg.x8.8xlarge.2c|56 cores, 480 GB|12,000|

## ApsaraDB RDS for PPAS {#section_xzc_fhx_5db .section}

|Edition|Version|Instance family|Instance type|CPU and memory|Maximum connections|Maximum IOPS|Storage capacity|
|-------|-------|---------------|-------------|--------------|-------------------|------------|----------------|
|High-availability Edition| 10

 |General-purpose|rds.ppas.t1.small|1 core, 1 GB \(for compatibility test\)|100|1,200|150 GB|
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

## ApsaraDB RDS for MariaDB {#section_qdb_l2g_2fb .section}

|Edition|Instance family|Instance type|CPU and memory|Maximum connections|Storage|
|Maximum IOPS|Storage capacity|
|-------|---------------|-------------|--------------|-------------------|-------|
|------------|----------------|
|High-availability Edition|General-purpose|mariadb.n2.small.2c|1 core, 2 GB|2,000|min\{1,200 + 30 × Storage capacity, 20,000\}|20 GB to 1,000 GB|
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
|mariadb.x4.8xlarge.2c|56 cores, 224 GB|64,000|
|mariadb.x8.8xlarge.2c|56 cores, 480 GB|100,000|

## Phased-out instance types of ApsaraDB RDS for MySQL {#section_bpx_khx_5db .section}

The following table describes the phased-out instance types of ApsaraDB RDS for MySQL. They will not be available when you create instances. We recommend that you use the latest instance types.

|Instance type|CPU cores|Memory|Maximum connections|Maximum IOPS|
|-------------|---------|------|-------------------|------------|
|rds.mys2.small|2|240 MB|60|150|
|rds.mys2.mid|4|600 MB|150|300|
|rds.mys2.standard|6|1,200 MB|300|600|
|rds.mys2.large|8|2,400 MB|600|1,200|
|rds.mys2.xlarge|9|6,000 MB|1,500|3,000|
|rds.mys2.2xlarge|10|12,000 MB|2,000|6,000|
|rds.mys2.4xlarge|11|24,000 MB|2,000|12,000|
|rds.mys2.8xlarge|13|48,000 MB|2,000|14,000|
|rds.mysql.st.d13|30|220 GB|64,000|20,000|

## Phased-out instance types of ApsaraDB RDS for SQL Server {#section_c3f_shx_5db .section}

The following table describes the phased-out instance types of ApsaraDB RDS for SQL Server. They will not be available when you create instances. We recommend that you use the latest instance types.

|Instance type|CPU cores|Memory|Maximum connections|Maximum IOPS|
|-------------|---------|------|-------------------|------------|
|rds.mssql.s1.small|1|2 GB|600|1,000|
|rds.mss1.small|6|1,000 MB|100|500|
|rds.mss1.mid|8|2,000 MB|200|1,000|
|rds.mss1.standard|9|4,000 MB|400|2,000|
|rds.mss1.large|10|6,000 MB|600|3,000|
|rds.mss1.xlarge|11|8,000 MB|800|4,000|
|rds.mss1.2xlarge|12|12,000 MB|1,200|6,000|
|rds.mss1.4xlarge|13|24,000 MB|2,000|12,000|
|rds.mss1.8xlarge|13|48,000 MB|2,000|14,000|

## Phased-out instance types of ApsaraDB RDS for PostgreSQL {#section_0n8_r0b_8s7 .section}

The following table describes the phased-out instance types of ApsaraDB RDS for PostgreSQL. They will not be available when you create instances. We recommend that you use the latest instance types.

|Instance type|CPU cores|Memory|Maximum connections|Maximum IOPS|
|-------------|---------|------|-------------------|------------|
|rds.pg.c1.large|8|16 GB|1,500|8,000|

## Phased-out instance types of ApsaraDB RDS for PPAS {#section_lph_jhd_x2b .section}

The following table describes the phased-out instance types of ApsaraDB RDS for PPAS. They will not be available when you create instances. We recommend that you use the latest instance types.

|Instance type|CPU cores|Memory|Maximum connections|Maximum IOPS|
|-------------|---------|------|-------------------|------------|
|rds.ppas.s1.small|1|2 GB|200|1,000|
|rds.ppas.s2.large|2|4 GB|400|2,000|
|rds.ppas.s3.large|4|8 GB|800|5,000|
|rds.ppas.m1.medium|4|16 GB|1,500|8,000|
|rds.ppas.c1.xlarge|8|32 GB|2,000|12,000|
|rds.ppas.c2.xlarge|16|64 GB|2,000|14,000|


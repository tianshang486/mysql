# Storage types {#concept_kpg_5wx_5db .concept}

ApsaraDB RDS provides two types of storage: local SSD and cloud SSD.

## Storage types {#section_s1k_1xx_5db .section}

-   **Local SSD \(recommended\)**

    A local SSD is in the server node where database engine resides. With local SSDs, computing is close to data so that I/O latency is reduced.

-   **Cloud SSD** 

    A SSD is an elastic block storage device based on the distributed storage architecture. With cloud SSDs, computing is separated from storage.


As technology evolves, Alibaba Cloud will provide enhanced cloud SSDs with better read/write performance. No matter which type of storage you choose, Alibaba Cloud ensures that RDS provides reliability, availability, and read/write performance that meet SLA requirements.

## Comparison {#section_vyn_2y5_fgb .section}

The following table lists the differences in performance and characteristics between local SSDs and cloud SSDs.

|Item|Local SSD|Cloud SSD|
|----|---------|---------|
|I/O performance|★★★★★ Low I/O latency and good performance

 |★★★★ Performance is slightly lower due to additional network I/O.

 |
|Functions|★★★★★ Supports all features of RDS

 |★★★ Currently certain database engines do not support read/write splitting, SQL audit, and CloudDBA.

 |
|Configuration flexibility|★★★ The storage capacity of an dedicated instance depends on the instance specification and therefore cannot be adjusted without changing the instance specification.

 |★★★★★ There are more optional configurations, and the storage capacity can be adjusted separately.

 |
|Max. storage capacity|★★★ 3 TB

 |★★★★★ 6 TB

 |
|Scalability|★★★ Scaling requires data replication and may take a few hours.

 |★★★★★ Minute-level scaling

 |

## Product support { .section}

The supported storage types depend on the database engine, version, and series.

|Database engine|Version|Series|Storage type|
|---------------|-------|------|------------|
|MySQL|5.7|Basic|Cloud SSD|
|High Availability|Cloud SSD|
|Local SSD|
|5.6/5.5|High Availability|Local SSD|
|SQLServer|2008 R2|High Availability|Local SSD|
|2012|Basic or High Availability|Cloud SSD|
|2016|Basic or High Availability|Cloud SSD|
|PostgreSQL|9.4|High Availability|Local SSD|
|10|Basic|Cloud SSD|
|PPAS|9.3|High Availability|Local SSD|


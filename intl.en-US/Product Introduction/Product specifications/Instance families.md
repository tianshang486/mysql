# Instance families

This topic describes the instance families of ApsaraDB RDS. They are shared, general-purpose, and dedicated instance families. Different instance families support different specifications and are suitable for different scenarios.

## Instance families

|Instance family|Description|Scenario|
|---------------|-----------|--------|
|Shared instance family \(Not supported\)

|-   A shared instance exclusively occupies the memory resources allocated to it, but shares CPU and storage resources with the other shared instances that are deployed on the same server.
-   CPU resources are highly reused among shared instances that are deployed on the same server. This maximizes cost effectiveness.
-   Shared instances may compete for resources.

|-   Business that requires low costs.
-   Business that requires high availability but is not demanding for stability. |
|General-purpose instance family|-   A general-purpose instance exclusively occupies the memory resources allocated to it, but shares CPU and storage resources with the other general-purpose instances that are deployed on the same server.
-   CPU resources are moderately reused among general-purpose instances that are deployed on the same server. This increases cost effectiveness.
-   The storage capacity of a general-purpose instance is independent of the number of CPU cores and memory capacity. You can flexibly configure the storage capacity based on your business requirements.

|Business that is not demanding on performance and stability.|
|Dedicated instance family|A dedicated instance exclusively occupies the CPU and memory resources allocated to it. Its performance remains stable and is not affected by other instances that are deployed on the same server. The top configuration of this instance family is dedicated host. A dedicated host instance occupies all resources on the server where it is deployed.

|Business that uses databases as the core system, such as finance, e-commerce, government affairs, and large- and medium-sized Internet services.|

The following figure shows the differences between the three instance families.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8244029951/p1370.png)

## Cost-effectiveness comparison

The three instance families have some unique performance metrics that cannot be directly compared. The following table is a comparison of costs between the three instance families based on instance types with similar specifications. This comparison provides a basis for you to make purchase decisions.

|Instance family|CPU cores and memory capacity|Storage capacity|Maximum connections|Maximum IOPS|Monthly subscription fee|
|---------------|-----------------------------|----------------|-------------------|------------|------------------------|
|Shared or general-purpose instance family|4 CPU cores, 16 GB|500GB|4000|7000|USD 320|
|Dedicated instance family|4 CPU cores, 32 GB|500GB|5000|9000|USD 550|

Based on the preceding table, a dedicated instance costs 70% more but provides twice as much memory capacity, 25% more connections, and 28% higher input/output operations per second \(IOPS\) than a shared or general-purpose instance. A dedicated instance also provides more stable CPU and storage performance. The dedicated instance family delivers high cost effectiveness if it is used in suitable business scenarios.

## Instance types

For more information about instance types and their specifications, such as the number of CPU cores, memory capacity, storage capacity, maximum number of connections, and IOPS, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).

## Pricing

For more information about the price of each instance type, see [the ApsaraDB RDS pricing page](https://www.alibabacloud.com/zh/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.10.30c7bf1fLOkY71#pricing).

## Change of the instance family

You can change the instance family and specifications of your RDS instance based on business requirements.

**Note:** You cannot directly upgrade your RDS instance from the shared instance family to the general-purpose or dedicated instance family. This will be supported soon. To do so, you must first create an RDS instance that belongs to the general-purpose or dedicated instance family. Then, use [Data Transmission Service \(DTS\)](/intl.en-US/RDS SQL Server Database/Data migration/Data migration solutions.md) to migrate data from the shared RDS instance to the new RDS instance.

For more information about how to change the specifications of your RDS instance, see the following topics:

-   [Change the specifications of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the specifications of an ApsaraDB RDS for MySQL instance.md)
-   [Change the specifications of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)
-   [Change the specifications of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Change the specifications of an ApsaraDB RDS for PostgreSQL instance.md)
-   [Change the specifications of an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Instance/Change the configuration of an RDS PPAS instance.md)
-   [Change the specifications of an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Instance/Change the configuration of an RDS MariaDB instance.md)

## FAQ

Why does an entry-level RDS instance outperform an enterprise-level instance? The entry-level RDS instance belongs to the shared or general-purpose instance family, whereas the enterprise-level RDS instance belongs to the dedicated instance family.

Therefore, the entry-level RDS instance supports a larger maximum number of connections and delivers higher IOPS than the enterprise-level RDS instance even when they have the same CPU and memory specifications. However, the enterprise-level RDS instance is more stable because it exclusively occupies CPU and memory resources. For more information, see [Instance families](#section_hmj_v1d_52b).


# Billing methods and billable items {#concept_qxr_pd2_vdb .concept}

## Billing methods {#section_25l_g7t_kzx .section}

RDS supports two billing methods.

|Billing method|Description|
|--------------|-----------|
|Subscription| -   Indicates prepayment. You need to pay when creating an instance.
-   For long-term requirements, Subscription is more cost-effective than Pay-As-You-Go. Moreover, the longer the subscription, the higher the discount.
-   Subscription instances cannot be released manually.
-   Subscription instances cannot be converted to Pay-As-You-Go instances.

 |
|Pay-As-You-Go| -   Indicates post payment. You are billed by hour. The system generates a billing order every hour and deducts the corresponding amount from your account balance. The amount depends on the instance configuration at the time when the order is generated.
-   Pay-As-You-Go is cost-effective for short-term requirements because the instance can be released at any time.
-   Pay-As-You-Go instances can be [converted to Subscription instances](../../../../intl.en-US/User Guide/Billing management/Change the billing method.md#).

 |

## Billable items {#section_prx_qd2_vdb .section}

|Item|Billing standard|
|----|----------------|
|Master instance|The price depends on the [RDS instance specifications](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#). The billing method is Subscription or Pay-As-You-Go.|
|Storage|The billing method is Subscription or Pay-As-You-Go, depending on the billing method of the master instance.|
|[Read-only instance](../../../../intl.en-US/Quick Start for MySQL/Scale instances/Read-only instance/Introduction to MySQL read-only instances.md#)|The billing method is Pay-As-You-Go. The costs depend on the read-only instance specifications.|
|[Clone instance](../../../../intl.en-US/User Guide/Recovery/Restore MySQL data.md#)|A clone instance is the instance created when you restore data to a new instance. The costs are the same as those of a master instance.|
|[Backup space](../../../../intl.en-US/User Guide/Backup/Back up RDS data.md#)|No charge is incurred if the size of the backups \(data and log backups\) of an instance do not exeed the [free quota](../../../../intl.en-US/User Guide/Backup/View the free quota of the backup space.md#). If they exceed the free quota, the excess space used is billed by hour.|
|[Monitoring](../../../../intl.en-US/User Guide/Monitoring and Alarming/Set the monitoring frequency.md#)| -   Free: monitoring frequency of once every 60 or 300 seconds
-   BIlled by hour: monitoring frequency of once every 5 seconds

 |
|[../../../../dita-oss-bucket/SP\_60/DNMYSQ1860058/EN-US\_TP\_7947.md\#](../../../../intl.en-US/User Guide/Security/SQL audit.md#)| -   This function is disabled by default. If it is enabled, you are billed by hour.
-   Hourly fee = price x total SQL log size at the time when the hourly billing order is generated

 |

## Price {#section_si8_9va_l3v .section}

For detailed pricing of the preceding billable items, see the following:

-   [MySQL](https://www.alibabacloud.com/product/apsaradb-for-rds-mysql/pricing)
-   [MariaDB TX](https://www.alibabacloud.com/product/apsaradb-for-rds-mariadb/pricing)
-   [SQL Server](https://www.alibabacloud.com/product/apsaradb-for-rds-sql-server/pricing)
-   [PostgreSQL](https://www.alibabacloud.com/product/apsaradb-for-rds-postgresql/pricing)
-   [PPAS](https://www.alibabacloud.com/product/apsaradb-for-rds-ppas)

## View billing history {#section_6ny_gqo_64a .section}

To check how much the billable items \(such as instance specifications, monitoring, SQL audit\) have costed you, see [EN-US\_TP\_7811.md\#](intl.en-US/Purchase Guide/View purchase details.md#).


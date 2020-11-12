# Pricing, billable items, and billing methods

This topic describes the pricing, billable items, and billing methods of ApsaraDB RDS.

## Billable items

|Billable item|Description|Pricing|
|-------------|-----------|-------|
|Primary and secondary instance types|You must pay for the selected instance type. The instance type is charged based on the pay-as-you-go or subscription billing method. For more information about the billing methods, see [Billing methods](#section_hbd_3ij_zkc).|-   [RDS MySQL](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-mysql/pricing)
-   [RDS SQL Server](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-sql-server/pricing)
-   [RDS PostgreSQL](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-postgresql/pricing)
-   [RDS PPAS](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-ppas/pricing)
-   [RDS MariaDB TX](https://www.alibabacloud.com/zh/product/apsaradb-for-rds-mariadb/pricing) |
|Storage capacity|You must pay for the storage capacity provisioned to the primary, secondary, read-only, and disaster recovery RDS instances that you create. The storage capacity is charged based on the pay-as-you-go or subscription billing method.|
|[Read-only instance type](/intl.en-US/RDS MySQL Database/Read-only instances/Overview of ApsaraDB RDS for MySQL read-only instances.md) \(optional\)|You must pay for the selected instance type. The instance type is charged based on the pay-as-you-go or subscription billing method. For more information, see [Read-only instance types](/intl.en-US/Product Introduction/Product specifications/Read-only instance types.md).|
|[Cloned instance](/intl.en-US/RDS MySQL Database/Restoration/Restore the data of an ApsaraDB RDS for MySQL instance.md) \(optional\)|A cloned instance is charged based on the same pricing standards as a new primary RDS instance.|
|[Backup storage](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md) \(optional\)|ApsaraDB RDS offers a free quota for backup storage. If your usage exceeds the free quota, you must pay for the excess backup storage that you use. For more information, see [View the free quota for backup storage of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/View the free quota for backup storage of an ApsaraDB RDS for MySQL instance.md).|
|[Performance monitoring](/intl.en-US/RDS MySQL Database/Monitoring and alerts/View the resource and engine metrics of an ApsaraDB RDS for MySQL instance.md) \(optional\)|-   Free functions: The 60-second monitoring and 300-second monitoring functions are provided free of charge.
-   [Charged function](/intl.en-US/RDS MySQL Database/Monitoring and alerts/Set the monitoring frequency of an ApsaraDB RDS for MySQL instance.md): The 5-second monitoring function is charged based on the pay-as-you-go billing method. |
|[SQL Explorer \(SQL audit\)](/intl.en-US/RDS MySQL Database/Audit/SQL Explorer.md) \(optional\)|The SQL Explorer \(SQL audit\) feature is disabled by default. No additional fees are required. If you enable this feature, you are charged an hourly fee based on the pay-as-you-go billing method. Hourly fee = Total volume of SQL logs at the hour of fee deduction × Unit price

**Note:** This feature is provided free of charge for the RDS Enterprise Edition. |
|[Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md) \(optional\)|The dedicated proxy feature is disabled by default. No additional fees are required. If you enable this feature, you are charged an hourly fee based on the pay-as-you-go billing method. The fee is deducted once every hour. |

## Billing methods

ApsaraDB RDS supports the following two billing methods.

|Billing method|Description|
|--------------|-----------|
|Subscription|-   A subscription instance is an instance that you subscribe to for a period of time and pay for up front.
-   Subscription billing is more cost-effective than pay-as-you-go billing. Therefore, we recommend that you select subscription billing with a longer commitment. You can receive larger discounts for longer subscription periods.
-   A subscription instance cannot be released within the subscription period.
-   You can switch your RDS instance from subscription billing to pay-as-you-go billing. For more information, see [Switch the billing method from subscription to pay-as-you-go](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from subscription to pay-as-you-go.md). |
|Pay-as-you-go|-   A pay-as-you-go instance is charged per hour based on your actual resource usage. The hourly fee is calculated based on the instance type that you specified in the purchase order and is deducted accordingly from the balance of your Alibaba Cloud account.
-   We recommend that you select pay-as-you-go billing for short-term use. If you no longer need your pay-as-you-go instance, you can release it to reduce costs.
-   You can switch your RDS instance from pay-as-you-go billing to subscription billing. For more information, see [Switch the billing method from pay-as-you-go to subscription](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from pay-as-you-go to subscription.md). |

## Spending details

For more information about how to view the spending details of an RDS instance, see [View the spending details of an ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/View the spending details of an ApsaraDB for RDS instance.md). The details include the costs and usage that are categorized based on billable items, such as the instance type, performance monitoring, and SQL Explorer \(SQL audit\).

## FAQ

-   Why am I charged additional fees for a subscription RDS instance?

    The fee that you pay when you create a subscription RDS instance only covers the instance and its storage capacity. If you create read-only RDS instances, enable the SQL Explorer \(SQL audit\) or performance monitoring feature, or use more storage than the free quota for backup storage, you must pay the additional fees required. For more information, see [Billable items](#section_prx_qd2_vdb).

-   Will I be charged for a pay-as-you-go RDS instance that I am not using?

    Yes, a pay-as-you-go RDS instance consumes computing and storage resources even if it is not used. Therefore, you are still charged an hourly fee. If you will not use a pay-as-you-go RDS instance for a long period of time, we recommend that you save the required data and then release the instance.

-   Is the inbound and outbound Internet traffic consumed for pay-as-you-go and subscription RDS instances free of charge?

    Yes, all of the inbound and outbound Internet traffic that is consumed for pay-as-you-go and subscription RDS instances is free of charge.



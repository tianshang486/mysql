# Change the specifications of an ApsaraDB RDS for MySQL instance

This topic describes how to change the specifications of an ApsaraDB RDS for MySQL instance, including the RDS edition, instance type, and storage capacity.

Your Alibaba Cloud account does not have overdue renewal orders.

For more information about how to change specifications in other database engines, see the following topics:

-   [Change the specifications of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)
-   [Change the specifications of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Change the specifications of an ApsaraDB RDS for PostgreSQL instance.md)
-   [Change the specifications of an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Instance/Change the configuration of an RDS PPAS instance.md)
-   [Change the specifications of an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Instance/Change the configuration of an RDS MariaDB instance.md)

## Change items

|Change item|Description|Change method|Billing|
|-----------|-----------|-------------|-------|
|RDS edition|MySQL 5.7: You can change your RDS edition from Basic to High-availability or from High-availability to Enterprise. Your RDS edition cannot be rolled back after the change is complete.

|For more information, see [Procedure](#section_ky2_tnw_b2b).|For more information, see [Specification change fees](/intl.en-US/Purchase Guide/Specification change fees.md).|
|Instance type|You can change to any available instance type.|
|Storage capacity|You can increase the storage capacity of all RDS instances. **Note:**

-   The new storage capacity that you specify must fall within the range of storage capacity allowed for the instance type. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).
-   You cannot reduce its storage capacity.
-   If the RDS instance uses standard SSDs or ESSDs, you can increase its storage capacity online.
-   If the range of storage capacity allowed for the instance type does not meet your requirements, we recommend that you change the instance type before you adjust the storage capacity of the RDS instance. |
|Storage type|When you change the edition of an ApsaraDB RDS for MySQL 5.7 instance from Basic to High-availability, you can change the storage type of the RDS instance from standard SSD or ESSD to local SSD.|
|Zone|You can migrate an RDS instance across zones in the same region. The attributes, configurations, and endpoints of the RDS instance remain unchanged after the migration.

When you change the edition of an ApsaraDB RDS for MySQL 5.7 instance from High-availability to Enterprise, you must change the zone of the RDS instance. For more information, see [Procedure](#section_ky2_tnw_b2b).

**Note:** You must migrate data when you change zones. A larger data volume requires more time to complete the migration.

|[Migrate an ApsaraDB RDS for MySQL instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md)|Free of charge.|
|Primary/secondary switchover|You can perform a manual or automatic switchover of services between primary and secondary RDS instances. After the switchover, the primary RDS instance becomes the secondary RDS instance.|[Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md)|
|Network type|All RDS instances can be deployed in virtual private clouds \(VPCs\), and some RDS instances can also be deployed in the classic network. You can change the network type of an RDS instance that supports both network types.|[Change the network type of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)|
|VPC and VSwitch|You can change the VPC or VSwitch for some RDS instances.|[Switch to a new VPC and VSwitch for an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md)|
|Maintenance window|You can change the maintenance window of an RDS instance.|[Set the maintenance window of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md)|
|Data replication mode|You can change the data replication mode of an RDS instance to improve database availability.|[Change the data replication mode of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the data replication mode of an ApsaraDB RDS for MySQL instance.md)|
|Instance parameter|You can reconfigure some parameters based on your business requirements.|For more information, see [Reconfigure the parameters of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance parameters/Reconfigure the parameters of an ApsaraDB RDS for MySQL instance.md) or [Use a parameter template to manage parameters](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md).|
|Database engine version|The database engine can only be upgraded from MySQL 5.5 to MySQL 5.6.|[Upgrade the database engine version of an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the database engine version of an RDS MySQL instance.md)|
|Billing method|The billing method of an RDS instance can be switched between pay-as-you-go and subscription. **Note:** Read-only RDS instances support only pay-as-you-go billing.

|[Switch the billing method from pay-as-you-go to subscription](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from pay-as-you-go to subscription.md)[Switch the billing method from subscription to pay-as-you-go](t1874750.md#)

|For more information, see [Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md).|
|Region|You cannot change the region of an existing RDS instance. Instead, you can create an RDS instance in the destination region and use Data Transmission Service \(DTS\) to migrate data from the existing RDS instance to the new RDS instance. After the data is migrated, you must update the endpoint for your application. After you confirm that your business runs normally, you can [release the existing RDS instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md).|[Migrate data between ApsaraDB for RDS instances](/intl.en-US/RDS MySQL Database/Data Migration/Migrate data between ApsaraDB for RDS instances.md)|For more information, see [Pricing, billing items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md) and [Pricing]().|

**Note:**

-   Changing the preceding items does not change the endpoint of the RDS instance.
-   You can create read-only RDS instances to scale the read capability of your database system. For more information, see [Create a read-only ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md).

## Billing

For more information, see [Specification change fees](/intl.en-US/Purchase Guide/Specification change fees.md).

## Precautions

-   Data may be migrated after you change the specifications of an RDS instance. After the migration is complete, the RDS instance switches over services during the scheduled time period. The switchover does not interrupt the synchronization of incremental data. During a switchover, a 30-second brief disconnection may occur. In addition, operations related to databases, accounts, and networks cannot be performed. We recommend that you change the specifications during off-peak hours or make sure that your application is configured to automatically reconnect to your RDS instance.
-   After you change the specifications of an RDS instance, you do not need to manually restart the RDS instance.
-   In the RDS Basic Edition, the database system consists of only one primary RDS instance, and no secondary RDS instances are provided as hot backups. If the primary RDS instance breaks down, is undergoing specification changes, or is upgrading, it becomes unavailable until the operations are done. If you require high database availability, we recommend that you use the RDS High-availability, Cluster, or Enterprise Edition.

## Procedure

**Note:** The following procedure describes how to change the specifications of an RDS instance. These specifications include the RDS edition, instance type, storage capacity, and storage type. For more information, see [Change items](#section_zlk_qvz_z2b).

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  Click **Change Specifications**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9150359951/p11174.png)

5.  In the dialog box that appears, select a change method and click **Next**. This step is required only for subscription instances.

    **Note:** You can select Upgrade or Downgrade for both subscription and pay-as-you-go instances. The new specifications immediately take effect.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1050359951/p33461.png)

6.  Change the specifications of the RDS instance. For more information, see [Change items](#section_zlk_qvz_z2b).

7.  Specify Switching Time.

    -   **Switch Immediately After Data Migration**: The system switches over services immediately after data migration is complete.
    -   **Switch Within Maintenance Window**: The system switches over services during the maintenance window that you specify. For more information, see [Set the maintenance window of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md).
8.  On the **Change Specifications** page, read and select Terms of Service, and click **Pay Now**.


## FAQ

-   How do I change the storage type of my RDS instance?

    For more information, see [How to change a cloud disk to a local disk](/intl.en-US/FAQs/Purchases and Payments/How do I change an SSD to a local SSD?.md).

-   Do I need to migrate data to a new RDS instance if I only want to expand the storage capacity?

    Check whether the storage capacity of the host where your current RDS instance resides is sufficient. If yes, you can expand the storage capacity without migrating data. If no, you must migrate data to a new RDS instance located on a host with sufficient storage capacity.

-   Will the specifications of read-only instances be upgraded automatically after I upgrade the specifications of their primary RDS instance?

    No, you must manually upgrade the specifications of read-only instances.

-   Will my online services be interrupted while I change the specifications of my RDS instance?

    While you change the specifications of your RDS instance, only a 30-second brief disconnection may occur during the subsequent switchover.

-   Will the endpoints of my RDS instance change after I change its specifications?

    After you change the specifications of your RDS instance, the [internal and public endpoints](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance.md) and [read/write splitting endpoint](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md) of your RDS instance remain unchanged, but the bound IP addresses may change. We recommend that you use the internal endpoint, public endpoint, or read/write splitting endpoint of your RDS instance to establish a connection from your application.


## Related operations

|Operation|Description|
|---------|-----------|
|[ModifyDBInstanceSpec](/intl.en-US/API Reference/Instance management/Modify instance.md)|Changes the specifications of an RDS instance.|


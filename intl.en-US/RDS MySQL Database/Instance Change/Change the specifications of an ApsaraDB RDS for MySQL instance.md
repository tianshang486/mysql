# Change the specifications of an ApsaraDB RDS for MySQL instance

This topic describes how to change the specifications of an ApsaraDB RDS for MySQL instance. The specifications include the RDS edition, instance type, and storage capacity.

-   Your Alibaba Cloud account does not have overdue renewal orders.
-   Your RDS instance runs MySQL.

**Note:**

For more information about how to change the specifications of RDS instances that run other database engines, see the following topics:

-   [Change the specifications of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Instance/Change the specifications of an ApsaraDB RDS for SQL Server instance.md)
-   [Change the specifications of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Change the specifications of an ApsaraDB RDS for PostgreSQL instance.md)
-   [Change the specifications of an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Instance/Change the configuration of an RDS PPAS instance.md)
-   [Change the specifications of an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Instance/Change the configuration of an RDS MariaDB instance.md)

## Change items

|Change item|Description|Change method|Billing|
|-----------|-----------|-------------|-------|
|RDS edition|If your RDS instance runs MySQL 5.7, you can upgrade the RDS edition from Basic to High-availability or from High-availability to Enterprise. After the change is complete, the RDS edition cannot be rolled back.

|For more information, see [Procedure](#section_ky2_tnw_b2b).|For more information, see [Specification change fees](/intl.en-US/Purchase Guide/Specification change fees.md).|
|Instance type|You can change the instance type regardless of the instance configuration.|
|Storage capacity|You can increase the storage capacity regardless of the instance configuration. **Note:**

-   The new storage capacity must fall within the storage capacity range that is allowed for the instance type. For more information, see [Primary instance types](/intl.en-US/Product Introduction/Product specifications/Primary instance types.md).
-   You cannot reduce the storage capacity of your RDS instance.
-   If your RDS instance uses enhanced SSDs, you can increase its storage capacity online.
-   If the storage capacity range that is allowed for the instance type does not meet your business requirements, we recommend that you change the instance type of your RDS instance. |
|Storage type|When you upgrade the RDS edition from Basic to High-availability, you can change the storage type from standard SSD to local SSD. This applies if your RDS instance runs MySQL 5.7.|
|Zone|You can migrate your RDS instance across zones in the same region. After the migration is complete, the attributes, configuration, and endpoints of your RDS instance remain unchanged.

When you upgrade the RDS edition from High-availability to Enterprise, you must change the zone. This applies if your RDS instance runs MySQL 5.7. For more information, see [Procedure](#section_ky2_tnw_b2b).

**Note:** When you change the zone of your RDS instance, you must migrate data. A larger data volume indicates more time that is required to complete the migration.

|For more information, see [Migrate an ApsaraDB RDS for MySQL instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md).|Free of charge.|
|Primary/secondary switchover|You can perform a manual or automatic switchover between your primary and secondary RDS instances. After the switchover is complete, the role of the primary RDS instance changes to secondary.|For more information, see [Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance](/intl.en-US/RDS MySQL Database/Instance Change/Perform a manual or automatic switchover of services between a primary ApsaraDB RDS for MySQL instance and its secondary instance.md).|
|Network type|All RDS instances can be deployed in virtual private clouds \(VPCs\), and some RDS instances can also be deployed in the classic network. If your RDS instance supports both network types, you can change its network type.|For more information, see [Change the network type of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md).|
|VPC and VSwitch|Some RDS instances support changes to their VPCs and VSwitches.|For more information, see [Switch to a new VPC and VSwitch for an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Switch to a new VPC and VSwitch for an RDS MySQL instance.md).|
|Maintenance window|You can change the maintenance window of your RDS instance.|For more information, see [Set the maintenance window of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md).|
|Data replication mode|You can change the data replication mode of your RDS instance. This allows you to improve database availability.|For more information, see [Change the data replication mode of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Change the data replication mode of an ApsaraDB RDS for MySQL instance.md).|
|Instance parameter|You can reconfigure some parameters of your RDS instance based on your business requirements.|For more information, see [Reconfigure the parameters of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance parameters/Reconfigure the parameters of an ApsaraDB RDS for MySQL instance.md) or [Use a parameter template to manage parameters](/intl.en-US/RDS MySQL Database/Instance parameters/Use a parameter template to manage parameters.md).|
|Database engine version|You can only upgrade the database engine of your RDS instance from MySQL 5.5 to MySQL 5.6.|For more information, see [Upgrade the database engine version of an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the database engine version of an RDS MySQL instance.md).|
|Billing method|You can switch the billing method of your RDS instance between pay-as-you-go and subscription. **Note:** Read-only RDS instances support only the pay-as-you-go billing method.

|For more information, see [Switch the billing method from pay-as-you-go to subscription](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from pay-as-you-go to subscription.md) or [Switch the billing method from subscription to pay-as-you-go](/intl.en-US/RDS MySQL Database/Instance Change/Switch the billing method from subscription to pay-as-you-go.md).|For more information, see [Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md).|
|Region|You cannot change the region of your existing RDS instance. Instead, you can create an RDS instance in the destination region and use Alibaba Cloud Data Transmission Service \(DTS\) to migrate data from your existing RDS instance to the new RDS instance. After the migration is complete, you must update the endpoints on your application. After you confirm that your workloads run normally, you can release your existing RDS instance. For more information, see [Release or unsubscribe from an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md).|For more information, see [Migrate data between ApsaraDB RDS instances](/intl.en-US/RDS MySQL Database/Data Migration/Migrate data between ApsaraDB RDS for MySQL instances.md).|For more information, see [Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md) and [Pricing]().|

**Note:**

-   After you change the preceding items, the endpoints of your RDS instance remain unchanged.
-   To scale up the read capability of your database system, you can create read-only RDS instances that offload read requests from your primary RDS instance. For more information, see [Create a read-only ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Read-only instances/Create a read-only ApsaraDB RDS for MySQL instance.md).

## Billing

For more information, see [Specification change fees](/intl.en-US/Purchase Guide/Specification change fees.md).

## Precautions

-   If you change the specifications of your RDS instance, the data of your RDS instance may be migrated to a new RDS instance. After the migration is complete, your workloads will be switched over to the new RDS instance during the specified switching time. The switchover does not interrupt the synchronization of incremental data. However, the switchover will cause a transient connection error of about 30 seconds. In addition, the operations related to databases, accounts, and networks cannot be performed. We recommend that you change the specifications during off-peak hours. Otherwise, make sure that your application is configured to automatically reconnect to your RDS instance.
-   After you change the specifications of your RDS instance, you do not need to manually restart the instance.
-   In the RDS Basic Edition, your database system consists of only one primary RDS instance, and no secondary RDS instances are provided as hot backups. If the primary RDS instance breaks down, is executing specification changes, or is upgrading the database engine version, it remains unavailable for a long period of time. If you require high database availability, we recommend that you select the RDS High-availability, Cluster, or Enterprise Edition.

## Procedure

**Note:** The following procedure describes how to change the specifications of your RDS instance. These specifications include the RDS edition, instance type, storage capacity, and storage type. For more information, see [Change items](#section_zlk_qvz_z2b).

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  Click **Change Specifications**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9150359951/p11174.png)

5.  In the dialog box that appears, select a change method and click **Next**. This step is required only when your RDS instance uses the subscription billing method.

    **Note:** You can select the Upgrade or Downgrade option for both subscription and pay-as-you-go instances. The new specifications immediately take effect.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1050359951/p33461.png)

6.  Change the specifications of your RDS instance. For more information, see [Change items](#section_zlk_qvz_z2b).

7.  Specify the **Switching Time** parameter.

    -   **Switch Immediately After Data Migration**: ApsaraDB RDS switches over your workloads immediately after the data migration is complete.
    -   **Switch Within Maintenance Window**: ApsaraDB RDS switches over your workloads during the specified maintenance window. For more information, see [Set the maintenance window of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md).
8.  Read and select Terms of Service, click **Pay Now**, and then complete the payment.


## FAQ

-   How do I change the storage type of my RDS instance?

    For more information, see [How to change a cloud disk to a local disk](/intl.en-US/FAQs/Purchases and Payments/How do I change an SSD to a local SSD?.md).

-   If I only expand the storage capacity of my RDS instance, do I need to migrate data to a new RDS instance?

    Check whether the storage capacity of the host where your RDS instance resides is sufficient. If yes, you can expand the storage capacity of your RDS instance without migrating the data. If no, you must migrate the data to a new RDS instance that resides on another suitable host. This host must provide sufficient storage capacity. The migration does not interrupt your workloads. However, after the migration is complete, your workloads will be switched over to the new RDS instance. This causes a transient connection error of about 30 seconds.

-   When I upgrade my primary RDS instance, will ApsaraDB RDS automatically upgrade the read-only RDS instances?

    No, after you upgrade your primary RDS instance, you must manually upgrade the read-only RDS instances.

-   When I change the specifications of my RDS instance, will my online workloads be interrupted?

    No, when you change the specifications of your RDS instance, your online workloads will not be interrupted. However, a transient connection error of about 30 seconds may occur during the subsequent switchover.

-   After I change the specifications of my RDS instance, will its endpoints change?

    After you change the specifications of your RDS instance, its internal, public, and read/write splitting endpoints remain unchanged. However, the IP addresses that are associated with the endpoints may change. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md) and [Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Enable the read/write splitting function in the shared proxy of an ApsaraDB RDS for MySQL instance.md). We recommend that you use the internal endpoint, public endpoint, or read/write splitting endpoint of your RDS instance to establish a connection from your application.


## Operations

|Operation|Description|
|---------|-----------|
|[ModifyDBInstanceSpec](/intl.en-US/API Reference/Instance management/Change instance configuration.md)|Changes the specifications of an ApsaraDB RDS instance.|


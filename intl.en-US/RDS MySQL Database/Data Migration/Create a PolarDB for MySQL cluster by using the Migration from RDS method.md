# Create a PolarDB for MySQL cluster by using the Migration from RDS method

PolarDB allows you to create a PolarDB for MySQL cluster by using the Migration from RDS method. The created PolarDB cluster retains the accounts, databases, IP address whitelist, and required parameters of the source ApsaraDB RDS for MySQL instance.

-   The edition of the source RDS instance is ApsaraDB RDS for MySQL 5.6 or 5.7 High-availability Edition, and the storage type is the local SSD.
-   -   For ApsaraDB RDS for MySQL 5.6, the minor version of the kernel for the RDS instance is 20190130 or later.
-   For ApsaraDB RDS for MySQL 5.7, the minor version of the kernel for the RDS instance is 20200331 or later.
    **Note:** You can execute the `show variables like '%rds_release_date%'` statement to view the minor version of the kernel for the RDS instance. For more information about how to upgrade the minor version of the kernel, see [Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Version upgrade/Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance.md).

-   [Transparent data encryption \(TDE\)](https://www.alibabacloud.com/help/zh/doc-detail/33510.htm) and [secure sockets layer \(SSL\)](https://www.alibabacloud.com/help/zh/doc-detail/32474.htm) are disabled on the source RDS instance.
-   The source RDS instance uses InnoDB as the table storage engine.
-   If Database Proxy \(Safe Mode\) is enabled for the RDS instance, a privileged account is created. For more information, see [Create a privileged account](/intl.en-US/RDS MySQL Database/Quick start/Create accounts and databases for an ApsaraDB RDS for MySQL instance.md). Otherwise, the network connection mode of the RDS instance is changed to the high-performance mode. For more information, see [\[Important\] RDS network link upgrade](t64586.md#).

    ![Check the database proxy mode](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0720359951/p54653.png)


PolarDB is a next-generation relational cloud database that is developed by Alibaba Cloud. The database service provides the following benefits:

-   Large storage capacity: up to 100 TB.
-   High performance: up to six times higher than the performance of MySQL.
-   Serverless storage: You do not need to purchase a storage capacity in advance. The system can automatically scale the storage capacity. You are charged for the used storage capacity.
-   Temporary specification scale-up: You can scale up cluster specifications to handle workload spikes.

**Note:** For more information, see [Benefits](/intl.en-US/Product Introduction/Benefits.md).

You can create a PolarDB for MySQL cluster by using the Migration from RDS method. The created PolarDB cluster retains the accounts, databases, IP address whitelist, and required parameters of the source RDS instance. The Migration from RDS method provides the following benefits:

-   The data migration feature is free.
-   No data loss occurs during the migration.
-   Incremental migration is supported. This supports a service downtime of less than 10 minutes.
-   Migration rollbacks are supported. If a migration fails, the migration can be rolled back within 10 minutes.
-   The switch with endpoints interchange feature is supported. You do not need to modify the configurations of your applications to connect to the PolarDB cluster.

## Limits

-   Cross-region data migration is not supported.
-   You cannot set the parameters of the source RDS instance during data migration.

## Billing

You are not charged for migrating data from the source RDS instance to the PolarDB cluster. You are charged only for purchasing the PolarDB cluster. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md).

## Data migration procedure

|Step|Description|
|----|-----------|
|1. [Migrate data from the source RDS instance](#section_s4t_zsn_13b)|In this step, a PolarDB cluster is created. The cluster stores the same data as the source RDS instance. Then, incremental data is synchronized from the source RDS instance to the PolarDB cluster in real time.|
|2. [Enable reverse migration](#section_jdh_0d3_zjz)|-   When you enable reverse migration, you can select Switch with Endpoints \(Connection Changes Not Required\). Then, the system automatically interchanges the endpoints between the RDS instance and the PolarDB cluster. The PolarDB cluster must have an endpoint, for example, the endpoint of a classic network or the Internet. In this case, you do not need to modify the configurations of your applications to connect to the PolarDB cluster.
-   After the reverse migration is enabled, the read/write status of the source RDS instance changes to Read Only, and the read/write status of the PolarDB cluster changes to Read and Write. Incremental data on the PolarDB cluster is synchronized to the source RDS instance.

**Note:** If data errors occur after the reverse migration is completed, you can roll back the migration. This allows you to restore the database and data to the status before the migration is performed. For more information, see [Roll back the migration](#section_hw4_hy4_13b). |
|3. [Complete the migration](#section_3ds_ojf_lmm)|-   We recommend that you test the PolarDB cluster to confirm that the cluster runs as expected before you click Complete Migration. You must click Complete Migration within seven days after the cluster is created.
-   After you click Complete Migration, the system stops synchronizing data between the source RDS instance and the PolarDB cluster. The read/write status of the source RDS instance changes to Read and Write. |

## Step 1: Migrate data from the source RDS instance

In this step, a PolarDB cluster is created. The cluster stores the same data as the source RDS instance. Then, incremental data is synchronized from the source RDS instance to the PolarDB cluster in real time.

1.  Log on [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  Click **Create Cluster**.

    **Note:** You can also log on to the [RDS console](https://rds.console.aliyun.com/). Find and click the ID of the source RDS instance. In the upper-right corner, click **Migrate to RDS for PolarDB Instance**. Then, perform the following steps to create a PolarDB for MySQL cluster.

4.  Select **Subscription** or **Pay-As-You-Go** as **Product Type**.

    -   **Subscription**: If you use the subscription billing method, you must pay for compute nodes when you create the cluster. You are charged for the consumed storage space by hour. The charges are deducted from your account balance on an hourly basis.
    -   **Pay-As-You-Go**: If you use the pay-as-you-go billing method, you pay for the resources after you use them. You are charged for the compute nodes and the consumed storage space by hour. The charges are deducted from your account balance on an hourly basis.
5.  Specify the parameters that are listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|The region where the source RDS instance is deployed. **Note:** The PolarDB cluster to be created must also be deployed in this region. |
    |**Create Type**|The method to create a PolarDB cluster. Select **Migration from RDS**. In this method, a PolarDB cluster is cloned from an RDS instance, and data is synchronized between the source RDS instance and the PolarDB cluster. By default, the binary logging feature is enabled for the new PolarDB cluster.|
    |**RDS Engine Type**|The engine type of the source RDS instance. The default value of this parameter is **MySQL** and cannot be changed.|
    |**RDS Engine Version**|The engine version of the source RDS instance. You can select **5.6** or **5.7**.|
    |**Source RDS Instance**|The available source RDS instances that exclude read-only instances. Select an RDS instance from the drop-down list.|
    |**Primary Availability Zone**|The primary zone of the cluster. Each zone is an independent geographical location that resides in a region. The zones that are deployed in the same region are similar.

You can deploy your PolarDB cluster and the Elastic Compute Service \(ECS\) instance in the same zone or in different zones.

You need to select only the primary zone. The system automatically selects a secondary zone. |
    |**Network Type**|The network type of the PolarDB cluster. The value of this parameter cannot be changed.|
    |**VPC****VSwitch**

|The VPC and the VSwitch to which the PolarDB cluster is connected. Make sure that the PolarDB cluster and the ECS instance to be connected are deployed in the same VPC. Otherwise, the cluster and the ECS instance cannot communicate over the internal network. This compromises performance.|
    |**Compatibility**|The database engine version of the PolarDB cluster. The default version is the same as the engine version of the source RDS instance and cannot be changed.|
    |**Edition**|The edition of the cluster. The value of this parameter can be only **Standard \(2-16 nodes\) \(Recommended\)**. You do not need to specify this parameter.|
    |**Node Specification**|The node specification of the cluster. Select a node specification based on your business needs. We recommend that you select a specification that is the same or higher than the specification of the source RDS instance. All the nodes in the PolarDB cluster are dedicated nodes. The dedicated nodes offer stable and reliable performance. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md).|
    |**Nodes**|The number of nodes to be created in the cluster. You do not need to specify this parameter. The system automatically creates a read-only node that has the same specification as the primary node.|
    |**Storage Cost**|The storage cost. You do not need to specify this parameter. You are charged for the used storage space on an hourly basis. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md). **Note:** You do not need to select a storage capacity when you create a cluster. The system automatically scales the storage capacity based on the amount of data to be stored. |
    |**Time Zone**|The time zone of the cluster. The default value is **UTC+08:00**.|
    |**Table Name Case Sensitivity**|Specifies whether table names are case-sensitive. The default value is **Not Case-sensitive**. If table names are case-sensitive in your on-premises database, we recommend that you select Case-sensitive. This ensures that you can migrate data in an easy way.**Note:** The value of this parameter cannot be changed after the cluster is created. Proceed with caution. |
    |**Release Cluster**|The backup retention policy that is used after the cluster is deleted or released. The default value is **Retain Last Automatic Backup \(Automatic Backup before Release\)**.    -   **Retain Last Automatic Backup \(Automatic Backup before Release\)**: retains the last backup after you delete the cluster.
    -   **Retain All Backups**: retains all backups after you delete the cluster.
    -   **Delete All Backups \(Cannot be restored\)**: retains no backups after you delete the cluster.
**Note:** If you need to retain backups after you delete or release the instance, you may need to pay a few fees. You can delete the backups to reduce costs. For more information, see [Data backup pricing](/intl.en-US/Pricing/Specifications and pricing.mdsection_ryg_gsw_hmu). |
    |**Cluster Name**|    -   The name of the new cluster. The cluster name must be 2 to 128 characters in length, and can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\).
    -   If you leave this parameter blank, the system automatically generates a cluster name. You can change the cluster name after the cluster is created. |
    |**Resource Group**|The resource group of the cluster. Select a resource group from available resource groups. For more information about how to create a resource group, see [Create a resource group]().**Note:** A resource group is a container that contains a group of resources in an Alibaba Cloud account. You can perform centralized management on these resources. A resource belongs to only one resource group. For more information, see [Use RAM to create and authorize resource groups](/intl.en-US/Tutorials/Use RAM to create and authorize resource groups.md). |

6.  If you create a **subscription** cluster, specify the **Purchase Plan** and **Number** parameters, and then click **Buy Now** in the right corner.

7.  On the **Confirm Order** page, confirm your order information. Read the terms of the service agreement, select the check box, and click **Buy Now**.

8.  On the **Purchase** page, confirm the unpaid order and the payment method and click **Purchase**.

9.  Log on to the [PolarDB console](https://polardb.console.aliyun.com) and check the status of the new PolarDB cluster.

    **Note:**

    -   After the cluster is created, the system starts to migrate data from the RDS instance to the cluster. You must click [Complete Migration](#section_3ds_ojf_lmm) in the PolarDB console within seven days after the cluster is created. Otherwise, the migration task is automatically terminated after seven days.
    -   You can also cancel the migration task. For more information about the impacts of canceling a migration task, see [FAQ](#section_lxr_3fp_13b).

## Step 2: Enable reverse migration

You can enable reverse migration to synchronize data from the PolarDB cluster to the RDS instance if the following conditions are met:

-   The operations that are described in [Step 1: Migrate data from the source RDS instance](#section_s4t_zsn_13b) are performed.
-   The value of **Replication Delay** is less than 60 seconds.

    ![Basic information](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0720359951/p51400.png)


1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com).

2.  Find the cluster and click the cluster ID.

3.  On the **Overview** page, click **Switch**. In the message that appears, click **OK**.

    ![Enable reverse migration](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p51031.png)

    **Note:** In most cases, it takes less than 5 minutes for the system to complete the reverse migration process.

    After the reverse migration is enabled, the read/write status of the source RDS instance and the destination PolarDB cluster are interchanged. The read/write status of the source RDS instance changes to Read Only, and the read/write status of the PolarDB cluster changes to Read and Write. The replication direction is changed so that incremental data on the PolarDB cluster is synchronized to the RDS instance.

4.  In the **Start Switching** dialog box, select **Switch with Endpoints \(Connection Changes Not Required\)** or **Switch without Endpoints \(Connection Changes Required\)**.

    ![Start the reverse migration](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p120880.png)

    If you select **Switch with Endpoints \(Connection Changes Not Required\)**, perform the following steps:

    1.  After you select **Switch with Endpoints \(Connection Changes Not Required\)**, the system automatically interchanges the endpoints between the RDS instance and the PolarDB cluster. You do not need to modify the configurations of your applications to connect to the PolarDB cluster. The following figure shows the rules for endpoint interchanges between the RDS instance and the PolarDB cluster.

        ![Rules for endpoint interchanges](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p120873.png)

        **Note:**

        -   After the switch with endpoints interchange feature is enabled, only the endpoints of the RDS instance and the PolarDB cluster are interchanged. Other configurations are not interchanged, such as the configurations of the VSwitches and virtual IP addresses.
        -   Endpoints can be interchanged only if both the source RDS instance and the destination PolarDB cluster have endpoints. By default, only the primary endpoints in the internal network can be interchanged if you do not create other endpoints.
        -   If you want to interchange other endpoints, create these endpoints first. For more information about how to create endpoints for the PolarDB cluster, see [Create a custom cluster endpoint](/intl.en-US/User Guide/Connect to PolarDB/Cluster endpoint/Create a custom cluster endpoint.md). For more information about how to create endpoints for the RDS instance, see [Configure endpoints for an RDS instance]().
        -   After the switch with endpoints interchange feature is enabled, the port numbers are not interchanged between the RDS instance and the PolarDB cluster. Therefore, make sure that the port number of the RDS instance is the same as that of the PolarDB cluster. If the port numbers are different, change one of the port numbers. For more information about how to change the port number of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md). For more information about how to change the port number of the PolarDB cluster, see [Modify the endpoint and port](/intl.en-US/User Guide/Connect to PolarDB/Modify or delete an endpoint.md).
        -   After the endpoints are interchanged, issues may occur due to the expiration of the Domain Name System \(DNS\) cache data. Before the DNS cache data is refreshed, the databases in the PolarDB cluster fail to be connected or support only read operations. We recommend that you refresh the DNS cache data of your server to fix this issue.
        -   If you want to use Data Management \(DMS\) to log on to the PolarDB database after the endpoints are interchanged, you must use the latest version of DMS and the cluster ID to log on to the database. You cannot log on to the database by using the endpoint.
    2.  Click **OK**.

        **Note:** If data errors occur after the reverse migration is completed, you can roll back the migration. This allows you to restore the database and data to the status before the migration is performed. For more information, see [Roll back the migration](#section_hw4_hy4_13b).

    If you select **Switch without Endpoints \(Connection Changes Required\)**, perform the following steps:

    1.  Select **Switch without Endpoints \(Connection Changes Required\)**. After the reverse migration is completed, you must change the database endpoint in your application at the earliest opportunity.

    2.  Click **OK**.

    3.  Refresh the page. After the value of the **PolarDB Read/Write Status** parameter becomes **Read and Write**, change the database endpoint in your application at the earliest opportunity.

        ![Refresh](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p51038.png)

        **Note:** If data errors occur after the reverse migration is completed, you can roll back the migration. This allows you to restore the database and data to the status before the migration is performed. For more information, see [Roll back the migration](#section_hw4_hy4_13b).


## Step 3: Complete the migration

After you perform the operations that are described in [Migrate data from the source RDS instance](#section_s4t_zsn_13b), you must click **Complete Migration** to complete the migration within seven days after the cluster is created.

**Warning:** After the migration is completed, the system stops synchronizing data between the RDS instance and the PolarDB cluster, and the [migration rollback](#section_hw4_hy4_13b) feature becomes unavailable. We recommend that you test the PolarDB cluster to confirm that the cluster runs as expected before you complete the migration.

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com).

2.  Find the cluster and click the cluster ID.

3.  On the **Overview** page, click **Complete Migration**. In the message that appears, click **OK**.

    ![Complete the migration](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p48987.png)

    ![Confirm the completion of the migration](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p51039.png)

    **Note:**

    -   After you click **OK**, the system stops data synchronization within about 2 minutes. During this process, the **Complete Migration** button is still available. Do not click the button again.
    -   You can specify whether to disable the binary logging feature for the PolarDB cluster. If this feature is disabled, the write performance can be slightly improved. However, you must restart the PolarDB cluster.
    -   If the source RDS instance is no longer required, you can release the instance. For more information, see [Release or unsubscribe from an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md).

## Roll back the migration

If data errors occur before the migration is completed, you can roll back the migration. This allows you to restore the database and data to the status before the migration is performed. After the rollback operation is complete, the read/write status of the source RDS instance changes to Read and Write, and the read/write status of the PolarDB cluster changes to Read Only. The system synchronizes data from the RDS instance to the PolarDB cluster.

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com).

2.  Find the cluster and click the cluster ID.

3.  On the **Overview** page, click **Rollback**.

    ![Roll back the migration](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p48988.png)

4.  In the **Switch Back** dialog box, select **Switch Back with Endpoints \(Connection Changes Not Required\)** or **Switch Back without Endpoints \(Connection Changes Required\)**.

    ![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1720359951/p131920.png)

    If you select **Switch Back with Endpoints \(Connection Changes Not Required\)**, perform the following steps:

    1.  After you select **Switch Back with Endpoints \(Connection Changes Not Required\)**, the system automatically interchanges the endpoints between the RDS instance and the PolarDB cluster. You do not need to modify the configurations of your applications to connect to the RDS instance.

        **Note:**

        -   After the switch with endpoints interchange feature is enabled, only the endpoints of the RDS instance and the PolarDB cluster are interchanged. Other configurations are not interchanged, such as the configurations of the VSwitches and virtual IP addresses.
        -   After the switch with endpoints interchange feature is enabled, the port numbers are not interchanged between the RDS instance and the PolarDB cluster. Therefore, make sure that the port number of the RDS instance is the same as that of the PolarDB cluster. If the port numbers are different, change one of the port numbers. For more information about how to change the port number of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md). For more information about how to change the port number of the PolarDB cluster, see [Modify the endpoint and port](/intl.en-US/User Guide/Connect to PolarDB/Modify or delete an endpoint.md).
        -   After the endpoints are interchanged, issues may occur due to the expiration of the DNS cache data. Before the DNS cache data is refreshed, the databases in the PolarDB cluster fail to be connected or support only read operations. We recommend that you refresh the DNS cache data of your server to fix this issue.
    2.  Click **OK**.

        **Note:** After you click **OK**, the read/write status of the source RDS instance changes to Read and Write, and the read/write status of the PolarDB cluster changes to Read Only. The system synchronizes data from the RDS instance to the PolarDB cluster.

    If you select **Switch Back without Endpoints \(Connection Changes Required\)**, perform the following steps:

    1.  Select **Switch Back without Endpoints \(Connection Changes Required\)**. After the reverse migration is completed, you must change the database endpoint in your application at the earliest opportunity.

    2.  Click **OK**.

        **Note:** After you click **OK**, the read/write status of the source RDS instance changes to Read and Write, and the read/write status of the PolarDB cluster changes to Read Only. The system synchronizes data from the RDS instance to the PolarDB cluster.

    3.  Refresh the page. After the value of the **Source RDS Read/Write Status** parameter becomes **Read and Write**, change the database endpoint in your application to the endpoint of the RDS instance at the earliest opportunity.


## FAQ

-   Is the source RDS instance affected when data is migrated from the RDS instance?

    No, the source RDS instance is not affected when data is migrated from the RDS instance.

-   What are the impacts of smooth migration on my workloads that run on the connected databases?

    Smooth migration ensures zero data loss during the migration. The service downtime is less than 10 minutes. You can roll back the migration based on your business needs.

-   What happens if I cancel the migration?

    After the migration is canceled, you can modify the parameters of the source RDS instance. The read/write status of the PolarDB cluster changes to Read and Write, and the data in the cluster is not deleted. If you manually cancel the migration, you can specify whether to disable the binary logging feature for the PolarDB cluster. Binary logging is not disabled if the migration is automatically canceled.


## Related API operations

|API|Description|
|---|-----------|
|[CreateDBCluster](/intl.en-US/API Reference/Cluster management/CreateDBCluster.md)|Creates a PolarDB cluster. **Note:** If you create a PolarDB cluster by using the Migration from RDS method, set the CreationOption parameter to MigrationFromRDS. |
|[DescribeDBClusterMigration](/intl.en-US/API Reference/Data migration from RDS/DescribeDBClusterMigration.md)|Queries the migration status of a PolarDB cluster.|
|[ModifyDBClusterMigration](/intl.en-US/API Reference/Data migration from RDS/ModifyDBClusterMigration.md)|Enables reverse migration to synchronize data from a PolarDB cluster to an RDS instance, or rolls back the migration.|
|[CloseDBClusterMigration](/intl.en-US/API Reference/Data migration from RDS/CloseDBClusterMigration.md)|Cancels or completes the migration for a PolarDB cluster.|


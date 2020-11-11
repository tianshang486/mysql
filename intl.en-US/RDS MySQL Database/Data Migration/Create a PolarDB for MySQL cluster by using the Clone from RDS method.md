# Create a PolarDB for MySQL cluster by using the Clone from RDS method

PolarDB allows you to create a PolarDB for MySQL cluster by using the Clone from RDS method.

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

For more information, see [Benefits](/intl.en-US/Product Introduction/Benefits.md).

You can create a PolarDB cluster by using the Clone from RDS method. The created PolarDB cluster retains the accounts, databases, IP address whitelist, and required parameters of the source RDS instance. The incremental data of the source RDS instance cannot be synchronized to the created PolarDB cluster.

**Note:** If you need to synchronize the incremental data of the source RDS instance to the PolarDB cluster in real time when you create the PolarDB cluster, follow instructions in [Create a PolarDB for MySQL cluster by using the Migration from RDS method](/intl.en-US/Data Migration/Synchronization/Migrate data from ApsaraDB for RDS to ApsaraDB for PolarDB/Create a PolarDB for MySQL cluster by using the Migration from RDS method.md). This achieves no service downtime during data migration.

## Highlights

-   The cloning feature is free.
-   No data is lost during the cloning.

## Procedure

1.  Log on [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  Click **Create Cluster**.

4.  Select **Subscription** or **Pay-As-You-Go** as **Product Type**.

    -   **Subscription**: If you use the subscription billing method, you must pay for compute nodes when you create the cluster. You are charged for the consumed storage space by hour. The charges are deducted from your account balance on an hourly basis.
    -   **Pay-As-You-Go**: If you use the pay-as-you-go billing method, you pay for the resources after you use them. You are charged for the compute nodes and the consumed storage space by hour. The charges are deducted from your account balance on an hourly basis.
5.  Specify the parameters that are listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|The region where the source RDS instance is deployed. **Note:** The PolarDB cluster to be created must also be deployed in this region. |
    |**Create Type**|The method to create a PolarDB cluster. Select **Clone from RDS**.|
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


## FAQ

Is the source RDS instance affected when data is cloned from the RDS instance?

No, the source RDS instance is not affected when data is clone from the RDS instance.

## Related API operations

|API|Description|
|---|-----------|
|[CreateDBCluster](/intl.en-US/API Reference/Cluster management/CreateDBCluster.md)|Creates a PolarDB cluster. **Note:** If you create a PolarDB cluster by using the Clone from RDS method, set the CreationOption parameter to CloneFromRDS. |

You must change the endpoint over which your application accesses the PolarDB cluster to the endpoint of the PolarDB cluster at the earliest opportunity. For more information, see [View or apply for an endpoint](/intl.en-US/User Guide/Connect to PolarDB/View or apply for an endpoint.md).


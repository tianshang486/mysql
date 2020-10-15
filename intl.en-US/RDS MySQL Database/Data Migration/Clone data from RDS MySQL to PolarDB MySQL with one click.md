# Clone data from RDS MySQL to PolarDB MySQL with one click

ApsaraDB for PolarDB allows you to clone data from an RDS MySQL instance to a new PolarDB MySQL cluster with one click.

This feature creates a destination ApsaraDB for PolarDB cluster with the same data as that of the source RDS instance. The incremental data of the source RDS instance will not be synchronized to the destination ApsaraDB for PolarDB cluster.

**Note:** If you need to synchronize the incremental data of the source RDS instance to the destination ApsaraDB for PolarDB cluster in real time while the cluster is being created, that is, to smoothly migrate data without service interruption, see [t475602.md\#](/intl.en-US/Data Migration/Synchronization/Migrate data from ApsaraDB for RDS to ApsaraDB for PolarDB/Create a PolarDB for MySQL cluster by using the Migration from RDS method.md).

## ApsaraDB for PolarDB introduction

ApsaraDB for PolarDB is the next-generation relational cloud database developed by Alibaba Cloud, which has the following main advantages.

-   Large storage capacity: up to 100 TB of storage.
-   High performance: up to 6x performance improvement over MySQL.
-   Serverless storage: no need to purchase storage capacity in advance, which is automatically scaled and is billed by usage.
-   Temporary upgrade: supports temporary upgrade of specifications to easily cope with short-term business peaks.

For more information, see [Benefits](/intl.en-US/Product Introduction/Benefits.md).

## Highlights

-   Free-of-charge
-   Zero data loss during cloning

## Precautions

-   Data cloning can only be performed in the same region.
-   The destination ApsaraDB for PolarDB cluster must contain information of the source RDS instance, including the account, database, IP address whitelist, and required parameters.

## Prerequisites

-   The source RDS instance is of the RDS MySQL 5.6 high-availability version.
-   [Transparent Data Encryption \(TDE\)]() and [Secure Sockets Layer \(SSL\)]()are not enabled in the source RDS instance.
-   The table storage engine of the source RDS instance is InnoDB.

## Procedure

1.  Log on to the [ApsaraDB for PolarDB console](https://polardb.console.aliyun.com).
2.  Click **Create Cluster**.
3.  Select Subscription or Pay-As-You-Go \(Hourly Rate\).
4.  Set parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|The region where the source RDS MySQL instance resides. **Note:** The destination ApsaraDB for PolarDB cluster is also located in this region. |
    |**Create Type**|The method of creating the cluster.     -   **Default Create Type**: creates a new ApsaraDB for PolarDB cluster.
    -   **Clone from RDS**: clones the data of the selected RDS instance to an ApsaraDB PolarDB cluster.
    -   **Migration from RDS**: clones the data of the selected RDS instance to an ApsaraDB for PolarDB cluster and keeps the data synchronized between the RDS instance and the ApsaraDB for PolarDB cluster. The binlogging feature is enabled for the new cluster by default.
 Select **Clone from RDS**. |
    |**RDS Engine Type**|The engine type of the source RDS instance, which cannot be changed.|
    |**RDS Engine Version**|The engine version of the source RDS instance, which cannot be changed.|
    |**Source RDS instance**|The source RDS instances for selection, which do not include read-only instances.|
    |**Primary availability zone**|The zone of the instance. A zone is an independent physical area located within a region. There are no substantive differences between the zones.

 You can deploy the ApsaraDB for PolarDB cluster and the ECS instance in the same zone or in different zones. |
    |**Network Type**|The network type of the ApsaraDB for PolarDB cluster, which cannot be changed.|
    |**VPC** **Vswitch**

|The VPC and VSwitch to which the ApsaraDB for PolarDB cluster belongs. Make sure that you place your ApsaraDB for PolarDB cluster and the ECS instance to be connected in the same VPC. Otherwise, they cannot communicate with each other through the internal network to achieve optimal performance.|
    |**Database Engine**|The database engine of the ApsaraDB for PolarDB cluster, which cannot be changed.|
    |**Node Specification**|The node specifications of the ApsaraDB for PolarDB cluster. Select the specifications as required. We recommend that you select specifications that are at least the same as those of the source RDS instance. All ApsaraDB for PolarDB nodes are dedicated ones with stable and reliable performance. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md).|
    |**Number Nodes**|The number of nodes. You do not need to specify this parameter. The system will create a read-only node with the same specifications as those of the primary node by default.|
    |**Storage Cost**|The storage capacity. You do not need to specify this parameter. The actual usage is billed hourly in pay-as-you-go mode. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md).|
    |**Cluster Name**|The cluster name for business distinguishing. The system will automatically create a name for your ApsaraDB for PolarDB cluster if you leave it blank. You can also modify the name after the cluster is created.|

5.  Specify **Duration** \(only applicable to subscription clusters\) and click **Buy Now** on the right side of the page.
6.  Confirm the order information, read the **Service Agreement**, select the checkbox to agree to it, and click **Activate Now**.

## Next step

Change the database connection point in applications to that of the ApsaraDB for PolarDB cluster as soon as possible. For more information, see [t3018.md\#](/intl.en-US/User Guide/Connect to PolarDB/View or apply for an endpoint.md).

## FAQ

Q: Will the source RDS instance be affected when **data is cloned** from the RDS instance?

A: No, the source RDS instance can run properly.


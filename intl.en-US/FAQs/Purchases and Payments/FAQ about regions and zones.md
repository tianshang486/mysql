# FAQ about regions and zones

This topic provides answers to some commonly asked questions about the regions and zones of ApsaraDB RDS.

## Introduction to regions and zones

A region is a physical data center. After an RDS instance is created, you cannot change its region.

Zones in a region are physical areas with independent power supplies and network facilities. The network latency is low between RDS instances within the same zone.

The following figure shows the relationships between regions and zones.

## Can instances in different regions communicate over an internal network?

No, instances in different regions can communicate only over the Internet by using public endpoints. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md). If you want two instances in different regions to communicate over an internal network, use one of the following two methods:

-   Method 1: [Release one of the two instances](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) and then create an instance in the same region as the other instance.
-   Method 2: If you want your ECS and RDS instances in different regions to communicate over an internal network, configure their network types to [VPC]() and create a [Cloud Enterprise Network](https://www.alibabacloud.com/help/zh/doc-detail/64648.htm) between the VPCs that host your ECS and RDS instances.

## Can instances in different zones of the same region communicate over an internal network?

Yes, instances in different zones of the same region can communicate over an internal network by using internal endpoints. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md).

## Can I change the region of my RDS instance?

No, you cannot change the region of your RDS instance after you confirm the purchase order. However, you can use Alibaba Cloud Data Transmission Service \(DTS\) to migrate the data of your original RDS instance to a new RDS instance in the destination region. Then, you can release your original RDS instance. For more information, see [Overview of data migration scenarios](/intl.en-US/Data Migration/Overview of data migration scenarios.md) and [Release or unsubscribe from an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Release or unsubscribe from an ApsaraDB RDS for MySQL instance.md).

## Can I change the zone of my RDS instance?

Yes, you can change the zone of your RDS instance. However, zones in the same region provide the same services. In this case, you do not need to change the zone of your RDS instance. If you want to change the zone of your RDS instance for specific reasons, see [Migrate an ApsaraDB RDS for MySQL instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md).

## Which deployment method is recommended: single-zone deployment or multi-zone deployment?

Zones in the same region are independent physical areas that are accessible to one another. If your application requires high disaster recovery capabilities, we recommend that you choose multi-zone deployment to create your RDS instances in different zones of the same region.

**Note:** For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md).


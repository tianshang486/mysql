# Create an RDS for PostgreSQL instance {#concept_kzn_qcg_wdb .concept}

This topic describes how to create an RDS for PostgreSQL instance by using the RDS console.

For information about how to create an RDS for PostgreSQL instance by calling an API action, see [CreateDBInstance](../../../../intl.en-US/API Reference/Instance management/CreateDBInstance.md#).

For information about the pricing of RDS for PostgreSQL instances, see [Billing methods and billable items](../../../../intl.en-US/Purchase Guide/Billing methods and billable items.md#).

## Prerequisites {#section_vqd_tcg_wdb .section}

-   You have registered an Alibaba Cloud account.
-   If you are creating a pay-as-you-go instance, make sure that your account balance is sufficient.

## Precautions {#section_o2c_vkk_a51 .section}

-   Subscription instances cannot be converted to pay-as-you-go instances.
-   Pay-as-you-go instances can be converted to subscription instances. For more information, see [Change the billing method](../../../../intl.en-US/User Guide/Billing management/Change the billing method.md#).
-   An Alibaba Cloud account can create up to 30 pay-as-you-go RDS instances. You can [open a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex) to apply for increasing the limit.
-   If you want to create an RDS instance in the PostgreSQL 10 High-availability Edition with local SSDs, PostgreSQL 10 Basic Edition, or PostgreSQL 9.4, you must log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
-   If you want to create an RDS instance in the PostgreSQL 10 or 11 High-availability Edition with SSDs, you must log on to the [new PostgreSQL console](https://gpdbnext.console.aliyun.com/gpdb/cn-hangzhou/list).

## Create an RDS instance in PostgreSQL 10 or 11 High-availability Edition with SSDs {#section_kvc_ayi_bq8 .section}

1.  Log on to the [new PostgreSQL console](https://common-buy.aliyun.com/?productCode=postgresql&chargeType=prepay&#/buy).
2.  Click the **Subscription** or **Pay-As-You-Go** tab.

    **Note:** For more information about the billing method, see [Billing methods and billable items](../../../../intl.en-US/Purchase Guide/Billing methods and billable items.md#).

3.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |Region|The region where the RDS instance is located. You cannot change the region after the instance is purchased.     -   Select the region where your target users are located to increase access speeds.
    -   Make sure that the RDS instance is located in the same region as the ECS instance to be connected. Otherwise, the RDS and ECS instances cannot communicate through a private network and consequently cannot achieve their optimal performance.
 |
    |Edition|**High-availability**. In the HA architecture, the RDS instance consists of two nodes: one master node and one slave node. For more information, see [Product series overview](../../../../intl.en-US/Product Introduction/Product series/Product series overview.md#).

 |
    |Primary Zone|The primary zone of the RDS instance.     -   A zone is an independent physical zone in a region. Zones in the same region are basically the same.
    -   You can create the RDS instance in the same or different zone from the ECS instance to be connected.
    -   You only need to select a primary zone. The system automatically assigns a secondary zone.
 |
    |Database Engine|The type of the DB engine. Only one option is available: **PostgreSQL**.|
    |Version|The version of PostgreSQL. The new PostgreSQL console supports PostgreSQL 11 and PostgreSQL 10.|
    |Instance Type|The type of the RDS instance. Each instance type provides a specific number of CPU cores, memory size, maximum number of connections, and maximum IOPS. For more information, see [Instance types](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#). RDS instances fall into the following types:

     -   General-purpose instances \(including entry-level instances and test instances\) : Each instance owns the memory and I/O resources allocated to it and shares CPU and storage resources with the other general-purpose instances on the same server.
    -   Dedicated instances: Each instance owns the CPU, memory, storage, and I/O resources allocated to it.
    -   Dedicated-host instances: Each instance owns all the CPU, memory, storage, and I/O resources on the server where it is deployed.
 For example, **4 Cores, 16 GB** is a general-purpose instance, **8 Cores, 32 GB \(Dedicated Instance\)** is a dedicated instance, and **30 Cores, 220 GB \(Dedicated Host\)** is a dedicated-host instance.

 |
    |Network Type|**VPC**. A Virtual Private Cloud \(VPC\) is an isolated network that is superior to a classic network in terms of security and performance. **Note:** Make sure that the network type of the RDS instance is the same as that of the ECS instance to be connected. If their network types are different, they cannot communicate through a private network.

 |
    |VPC VSwitch

 |     -   If you have created a VPC that meets your network planning requirements, you can select the VPC and a VSwitch on the VPC.
    -   If you have not created a VPC that meets your network planning requirements, you can select the default VPC and VSwitch.
 |
    |Storage Type|Standard SSD or Enhanced SSD. For more information, see [Storage types](../../../../intl.en-US/Product Introduction/Storage types.md#).|
    |Capacity|Used to store data, system files, binary log files, and transaction files.|
    |Data Encryption|Available only to the China \(Hong Kong\) region. Two options are provided: **No Encryption** and **KMS Encryption**. For more information, see [Manage CMKs](https://www.alibabacloud.com/help/doc-detail/108805.htm).|

4.  Set **Quantity** and **Duration**, then click **Buy Now**.

    **Note:** You must set **Duration** only when you are creating a subscription instance.

5.  On the Confirm Order page, select the terms of service, and click **Pay** to complete the payment.

## Create an RDS instance in PostgreSQL 10 High-availability Edition \(with local SSDs\), PostgreSQL 10 Basic Edition, or PostgreSQL 9.4 \(through the old RDS console\) {#section_6fa_4rj_42i .section}

1.  Log on to the [old RDS console](https://rds-buy.aliyun.com/?#/create/rds).
2.  Click the **Subscription** or **Pay-As-You-Go** tab. For more information about pricing, see [Billing methods and billable items](../../../../intl.en-US/Purchase Guide/Billing methods and billable items.md#).
3.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |Region|The physical location where the RDS instance is located. You cannot change the region after the instance is purchased.     -   Select the region where your target users are located to increase access speeds.
    -   Make sure that the RDS instance is located in the same region as the ECS instance to be connected. Otherwise, the RDS and ECS instances cannot communicate through a private network and consequently cannot achieve their optimal performance.
 |
    |Resource Group|The resource group to which the RDS instance belongs.|
    |Database Engine| The type of the DB engine. Select **PostgreSQL**.

 **Note:** The available DB engines vary depending on the region you select.

 |
    |Version|The version of PostgreSQL. The old RDS console supports PostgreSQL 9.4 and PostgreSQL 10. **Note:** The available versions vary depending on the region you select.

 |
    |Edition|     -   **Basic**: The RDS instance consists of only one node. Compute is decoupled from storage to reduce costs.
    -   **High-availability**: The RDS instance consists of a master node and a slave node.
 For more information, see [Product series overview](../../../../intl.en-US/Product Introduction/Product series/Product series overview.md#). The available editions vary depending on the version you select.

 |
    |Storage Type|     -   **Local SSD**: A local SSD is located on the same node as the DB engine. Data is stored on the local SSD to reduce I/O latency.
    -   **SSD**: An SSD is a scalable block storage device designed based on the distributed architecture. Data is stored on the SSD to decouple compute and storage.
 For more information, see [Storage types](../../../../intl.en-US/Product Introduction/Storage types.md#).

 |
    |Zone| A zone is an independent physical zone in a region. Zones in the same region are basically the same. You can create the master and slave nodes of the RDS instance in the same or different zones.

 Multi-zone deployment provides a higher level of disaster tolerance than single-zone deployment.

 |
    |Network Type|     -   **Classic Network**: a classic network.
    -   **VPC** \(recommended\): A Virtual Private Cloud \(VPC\) is an isolated network that is superior to a classic network in terms of security and performance.

**Note:** Make sure that the network type of the RDS instance is the same as that of the ECS instance to be connected. If their network types are different, they cannot communicate through a private network.

 |
    |CPU and Memory|The type of the RDS instance. Each instance type provides a specific number of CPU cores, memory size, maximum number of connections, and maximum IOPS. For more information, see [Instance types](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#). RDS instances fall into the following types:

     -   General-purpose instances \(including entry-level instances and test instances\) : Each instance owns the memory and I/O resources allocated to it and shares CPU and storage resources with the other general-purpose instances on the same server.
    -   Dedicated instances: Each instance owns the CPU, memory, storage, and I/O resources allocated to it.
    -   Dedicated-host instances: Each instance owns all the CPU, memory, storage, and I/O resources on the server where it is deployed.
 For example, **4 Cores, 16 GB** is a general-purpose instance, **8 Cores, 32 GB \(Dedicated Instance\)** is a dedicated instance, and **30 Cores, 220 GB \(Dedicated Host\)** is a dedicated-host instance.

 |
    |Capacity|Used to store data, system files, binary log files, and transaction files.|

4.  Set **Quantity** and **Duration** \(the **Duration** parameter is available only when you are creating a subscription instance\), then click **Buy Now**.

    **Note:** 

    -   If you are creating a subscription instance, you can select **Auto-renewal**. Then the system automatically deducts fees based on the specified duration. For example, if you select a duration of three months, the system automatically deducts fees of three months in each automatic renewal.
    -   If you are creating a subscription instance, you can click **Add to Cart** to add the RDS instance to the cart, and click **Cart** later to pay for the instance.
5.  On the Order Confirmation page, select the terms of service, and click **Pay Now** to complete the payment.

## What to do next {#section_7eq_u77_8zv .section}

In the upper-left corner, select the region where the new RDS instance is located. Then you can view the new RDS instance.

![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156894414249667_en-US.png)

After you create the RDS instance, you must [configure a whitelist](intl.en-US/Quick Start for PostgreSQL/Initial configuration/Configure a whitelist for an RDS for PostgreSQL instance.md#) and [create databases and accounts](intl.en-US/Quick Start for PostgreSQL/Initial configuration/Create databases and accounts for an PostgreSQL instance.md#) for it. If you connect the RDS instance through the Internet, you must also [apply for a public connection address](intl.en-US/Quick Start for PostgreSQL/Initial configuration/Apply for a public endpoint for an RDS for PostgreSQL instance.md#). For more information about how to connect to an RDS instance, see [Connect to an instance](intl.en-US/Quick Start for PostgreSQL/Connect to an RDS for PostgreSQL instance.md#).

## APIs {#section_kd6_ec1_a1h .section}

|API|Description|
|---|-----------|
|[CreateDBInstance](../../../../intl.en-US/API Reference/Instance management/CreateDBInstance.md#)|Used to create an RDS instance.|


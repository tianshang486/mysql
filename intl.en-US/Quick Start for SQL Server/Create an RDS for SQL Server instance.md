# Create an RDS for SQL Server instance {#concept_pv1_n5z_vdb .concept}

You can use the RDS console or APIs to create an RDS instance. For more information about instance pricing, see [Pricing of ApsaraDB for RDS](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15zCpnIt#pricing). This topic describes how to use the RDS console to create an RDS for SQL Server instance. For more information about how to use APIs to create an RDS for SQL Server instance, see [CreateDBInstance](../intl.en-US/API Reference/Instance management/CreateDBInstance.md#).

## Prerequisites {#section_hyl_tcf_vdb .section}

You have registered an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.html).

## Precautions {#section_8hp_py7_xy2 .section}

-   Subscription instances cannot be converted to Pay-As-You-Go instances.
-   Pay-As-You-Go instances can be converted to Subscription instances. For operation instructions, see [Change the billing method](../intl.en-US/User Guide/Billing management/Change the billing method.md#).
-   An Alibaba Cloud account can create up to 30 Pay-As-You-Go RDS instances. You can [open a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex) to apply for increasing the limit.

## Procedure {#section_o45_5cf_vdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  On the Instances page, click **Create Instance**.
3.  Select a billing method:
    -   **Pay-As-You-Go**: indicates post payment \(billed by hour\). For short-term requirements, create Pay-As-You-Go instances because they can be released at any time to save costs.
    -   **Subscription**: indicates prepayment. You need to pay when creating an instance. For long-term requirements, create Subscription instances because they are more cost-effective. Furthermore, the longer the subscription, the higher the discount.
4.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|Indicates the location of the RDS instance you want to purchase. You cannot change the region once you confirm your order.     -   Select the region closest to your users to increase the access speed.
    -   Select the region where your ECS instance is located so that the ECS instance can access the RDS instance through the intranet. If the ECS instance and RDS instance are located in different regions, they can communicate only through the Internet and hence performance is degraded.
 |
    |**Database Engine**| The supported database engines are MySQL, Microsoft SQL Server, PostgreSQL, PPAS \(compatible with Oracle\), and MariaDB TX.

 In this example, select **Microsoft SQL Server**.

 **Note:** The available database engines vary depending on the region you select.

 |
    |**Version**| For RDS for SQL Server, the supported versions are SQL Server 2017, 2016, 2012, and 2008 R2. For more information, see [Functions supported by different editions of SQL Server](intl.en-US/Quick Start for SQL Server/Functions supported by different editions of SQL Server.md#).

 **Note:** The available versions vary depending on the region you select.

 |
    |**Edition**|     -   **Basic**: This edition provides a single node and separates computing from storage. It is extremely cost-effective.
    -   **High-availability**: This edition adopts the high-availability architecture with one master node and one slave node. It is applicable to over 80% of scenarios.
    -   **AlwaysOn**: This edition provides one master node, one slave node, and up to seven read-only nodes that horizontally scale read capabilities.
 **Note:** The available product series vary depending on the region you select. For more information on the product series, see [Product series overview](../intl.en-US/Product Introduction/Product series/Product series overview.md#).

 |
    |**Zone**| A zone is a physical area within a region. Different zones in the same region are basically the same.

 You can deploy the master and slave nodes of your RDS instance in the same zone or in different zones.

 |
    |**Network Type**|     -   **Classic Network**: indicates the traditional network.
    -   **VPC** \(recommended\): short for Virtual Private Cloud. A VPC is an isolated network environment and therefore provides higher security and performance than the classic network.

**Note:** Make sure the network type of the RDS instance is the same as that of your ECS instance so that the ECS instance can access the RDS instance through the intranet.

 |
    |**Type**| Indicates the specifications of the RDS instance. Each instance type supports a specific number of CPU cores, memory size, maximum number of connections, and maximum IOPS. For more information, see [Instance type list](../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 RDS for SQL Server supports the following instance type families:

     -   **General-purpose instance**: owns dedicated memory and I/O resources, but shares CPU and storage resources with the other general-purpose instances on the same server.
    -   **Dedicated instance**: owns dedicated CPU, memory, storage, and I/O resources.
    -   **Dedicated host**: owns all the CPU, memory, storage, and I/O resources on the server where it is located.
 For example, **8 Cores 32 GB \(Basic\)** indicates a general-purpose instance, and **8 Cores 32 GB \(Dedicated\)** indicates a dedicated instance.

 |
    |**Capacity**| Used for storing data, system files, binlog files, and transaction files.

 |

5.  Set the duration \(only for Subscription instances\) and quantity, and click **Buy Now**.

    **Note:** For a Subscription instance, you can:

    -   Select **Auto Renew** in the **Duration** section. Then the system can automatically deduct fees from your account to extend the validity period of your instance. For example, if you purchase a three-month Subscription instance with **Auto Renew** selected, the system automatically deducts frees of three months when the instance is about to expire.
    -   Click **Add to Cart** and then click the cart to place the order.
6.  On the **Order Confirmation** page, review the order information, select the terms and agreements as prompted, click **Pay Now**, and complete the payment.

## What to do next {#section_d9p_3w4_wgt .section}

1.  In the upper left corner of the [RDS console](https://rdsnext.console.aliyun.com), select the region where the instance is located, and view the instance details.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567623936543_en-US.png)

2.  [Configure a whitelist](intl.en-US/Quick Start for SQL Server/Initial configuration/Configure a whitelist.md).
3.  [Create accounts](intl.en-US/Quick Start for SQL Server/Initial configuration/Creating accounts and databases/Create databases and accounts for an RDS for SQL Server 2008 R2 instance.md).
4.  [Apply for an Internet address](intl.en-US/Quick Start for SQL Server/Initial configuration/Apply for an Internet address.md#) \(if you want to access the RDS instance through the Internet\).
5.  [Connect to the RDS instance](intl.en-US/Quick Start for SQL Server/Connect to an RDS for SQL Server instance.md).

## APIs {#section_ni9_m6n_1w2 .section}

|API|Description|
|---|-----------|
|[CreateDBInstance](../intl.en-US/API Reference/Instance management/CreateDBInstance.md#)|Used to create an RDS instance.|


# Create an RDS for MariaDB TX instance {#concept_wzp_ncf_vdb .concept}

You can use the RDS console or APIs to create an RDS for MariaDB TX instance. For more information about instance pricing, see [Billing methods and billing items](../intl.en-US/Purchase Guide/Billing methods and billing items.md#). This topic describes how to create an RDS for MariaDB TX instance in the RDS console. For information about how to create an RDS for MariaDB TX by using APIs, see [CreateDBInstance](../intl.en-US/API Reference/Instance management/CreateDBInstance.md#).

## Prerequisites {#section_hyl_tcf_vdb .section}

You have registered an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.html).

## Precautions {#section_kmf_kkp_mgb .section}

-   Subscription instances cannot be converted to Pay-As-You-Go instances.
-   Pay-As-You-Go instances can be converted to Subscription instances. For more information, see [Change the billing method](../intl.en-US/User Guide/Billing management/Change the billing method.md#).
-   An Alibaba Cloud account can create up to 30 Pay-As-You-Go RDS instances. You can [open a ticket](https://workorder-intl.console.aliyun.com/console.htm#/ticket/createIndex) to apply for increasing the limit.

## Procedure {#section_o45_5cf_vdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  On the Instances page, click **Create Instance**.
3.  Select a billing method.
    -   **Pay-As-You-Go**: indicates post payment \(billed by hour\). For short-term requirements, create Pay-As-You-Go instances because they can be released at any time to save costs.
    -   **Subscription**: indicates prepayment. You need to pay when creating an instance. For long-term requirements, create Subscription instances because they are more cost-effective. Furthermore, the longer the subscription, the higher the discount.
4.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |Region|Indicates the location of the RDS instance you want to purchase. You cannot change the region once you confirm your order.     -   Select the region closest to your users to increase the access speed.
    -   Select the region where your ECS instance is located so that the ECS instance can access the RDS instance through the intranet. If the ECS instance and RDS instance are located in different regions, they can communicate only through the Internet and hence performance is degraded.
 |
    |Zone|A zone is a physical area within a region. Different zones in the same region are basically the same. You can deploy the master and slave nodes of your RDS instance in the same zone or in different zones.

 |
    |Database Engine| The supported database engines are MySQL, Microsoft SQL Server, PostgreSQL, PPAS \(compatible with Oracle\), and MariaDB TX.

 In this example, select **MariaDB TX**.

 **Note:** The available database engines vary depending on the region you select.

 |
    |Version|For RDS for MariaDB TX, the supported version is MariaDB TX 10.3.|
    |Edition|Select **High-availability**. This edition adopts the high-availability architecture with one master node and one slave node. **Note:** The available product series vary depending on the region you select. For more information on the product series, see [Product series overview](../intl.en-US/Product Introduction/Product series/Product series overview.md#).

 |
    |Network Type|You do not need to select a network type. MariaDB TX supports only the VPC network type. A Virtual Private Cloud \(VPC\) is an isolated network environment and therefore provides higher security and performance than a classic network. For more information, see [Create a default VPC and VSwitch](https://www.alibabacloud.com/help/doc-detail/65402.htm?spm=a2c63.l28256.b99.14.fde5639dWHeUIx).

**Note:** Make sure the network type of the RDS instance is the same as that of your ECS instance so that the ECS instance can access the RDS instance through the intranet.

 |
    |Type|Indicates the specifications of the RDS instance. Each instance type supports a specific number of CPU cores, memory size, maximum number of connections, and maximum IOPS. For more information, see [Instance type list](../intl.en-US/Product Introduction/Instance types/Instance type list.md#). RDS for MariaDB TX supports the following instance type families:

     -   **General-purpose instance**: owns dedicated memory and I/O resources, but shares CPU and storage resources with the other general-purpose instances on the same server.
    -   **Dedicated instance**: owns dedicated CPU, memory, storage, and I/O resources.
    -   **Dedicated host**: owns all the CPU, memory, storage, and I/O resources on the server where it is located.
 **8 Cores 32 GB \(Basic\)** indicates a general-purpose instance, and **8 Cores 32 GB \(Dedicated\)** indicates a dedicated instance.

 |
    |Capacity|Used for storing data, system files, binlog files, and transaction files.|

5.  Set the duration \(only for Subscription instances\) and quantity, and click **Buy Now**.

    **Note:** For a Subscription instance, you can:

    -   Select **Auto Renew** in the **Duration** section. Then the system can automatically deduct fees to extend the validity period of your instance. For example, if you purchase a three-month Subscription instance with **Auto Renew** selected, the system automatically deducts frees of three months when the instance is about to expire.
    -   Click **Add to Cart** and then click the cart to place the order.
6.  On Order Confirmation page, select **Terms of Service, Service Level Agreement, and Terms of Use**, click **Pay Now**, and complete the payment.

## What to do next {#section_rtf_q4z_2fb .section}

1.  In the upper-left corner of the [RDS console](https://rdsnext.console.aliyun.com), select the region where the instance is located, and view the instance details.

    ![DO NOT TRANSLATE](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567894036543_en-US.png)

2.  [Configure a whitelist](intl.en-US/Quick Start for MariaDB TX/Initial configuration/Configure a whitelist.md#).
3.  [Create accounts](intl.en-US/Quick Start for MariaDB TX/Initial configuration/Create accounts and databases.md#).
4.  [Apply for an Internet address](intl.en-US/Quick Start for MariaDB TX/Initial configuration/Apply for an Internet address.md#) \(if you want to access the RDS instance through the Internet\).
5.  [Connect to the RDS instance](intl.en-US/Quick Start for MariaDB TX/Connect to an RDS for MariaDB TX instance.md#).


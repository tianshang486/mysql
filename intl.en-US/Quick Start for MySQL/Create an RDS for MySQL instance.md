# Create an RDS for MySQL instance {#concept_wzp_ncf_vdb .concept}

You can use the RDS console or APIs to create an RDS for MySQL instance. For more information about instance pricing, see [Billing methods and billing items](../../../../intl.en-US/Purchase Guide/Billing methods and billing items.md#). This topic describes how to use the RDS console to create an instance. To use APIs to create an RDS for MySQL instance, see [CreateDBInstance](../../../../intl.en-US/API Reference/Instance management/CreateDBInstance.md#).

## Prerequisites {#section_hyl_tcf_vdb .section}

You have registered an Alibaba Cloud account.

## Precautions {#section_sft_yn0_nsm .section}

-   Subscription instances cannot be converted to Pay-As-You-Go instances.
-   Pay-As-You-Go instances can be converted to Subscription instances. For operation instructions, see [Change the billing method](../../../../intl.en-US/User Guide/Billing management/Change the billing method.md#).
-   An Alibaba Cloud account can create up to 30 Pay-As-You-Go RDS instances. You can open a ticket to apply for increasing the limit.

## Procedure {#section_o45_5cf_vdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  On the Instances page, click **Create Instance**.
3.  Select a billing method:
    -   **Pay-As-You-Go**: indicates post payment \(billed by hour\). For short-term requirements, create Pay-As-You-Go instances because they can be released at any time to save costs.
    -   **Subscription**: indicates prepayment. You need to pay when creating an instance. For long-term requirements, create Subscription instances because they are more cost-effective. Furthermore, the longer the subscription, the higher the discount.
4.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|Indicates the location of the RDS instance you want to purchase. The region cannot be changed after the purchase.     -   Select the region closest to your users for high access speed.
    -   Make sure to select the region where your ECS instance is deployed so that the ECS instance can access the RDS instance through the intranet; otherwise, they intercommunicate through the Internet and the access speed is affected.
 |
    |**Database Engine**| The supported database engines are MySQL, Microsoft SQL Server, PostgreSQL, PPAS \(compatible with Oracle\), and MariaDB TX.

 In this example, select **MySQL**.

 **Note:** The available database engines vary depending on the region you select.

 |
    |**Version**| For RDS for MySQL, the supported versions are MySQL 5.5, 5.6, 5.7, and 8.0.

 **Note:** The available versions vary depending on the region you select.

 |
    |**Edition**|     -   **Basic Edition**: It provides a single node and separates computing from storage, and is extremely cost-effective.
    -   **High-availability Edition**: It adopts the high-availability architecture with one master node and one slave node. It is applicable to over 80% of scenarios.
 **Note:** The available product series vary depending on the region you select. For more information on the product series, see [Product series overview](../../../../intl.en-US/Product Introduction/Product series/Product series overview.md#).

 |
    |**Zone**| A zone is a physical area within a region. Different zones in the same region are basically the same.

 You can deploy the master and slave nodes of an RDS instance in the same zone or in different zones.

 |
    |**Network type**|     -   **Classic Network**: indicates the traditional network type.
    -   **VPC** \(recommended\): short for Virtual Private Cloud. A VPC is an isolated network environment and therefore provides higher security and performance than the classic network.

**Note:** Make sure the network type is the same as that of your ECS instance so that the ECS instance can access the RDS instance through the intranet.

 |
    |**Type**| Indicates instance specifications. For specific resources \(CPU cores, memory, maximum number of connections, and IOPS\) provided by each instance type, see [Instance type list](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 RDS supports the following instance type families:

     -   **General-purpose instance**: owns dedicated memory and I/O resources, but shares CPU and storage resources with other general-purpose instances on the same server.
    -   **Dedicated instance**: owns dedicated CPU, memory, storage, and I/O resources.
    -   **Dedicated host**: owns all the CPU, memory, storage, and I/O resources on the server on which it is located.
 For example, **8 Cores 32 GB \(Basic\)** indicates a general-purpose instance, and **8 Cores 32 GB \(Dedicated\)** indicates a dedicated instance.

 |
    |**Capacity**| Used for storing data, system files, binlog files, and transaction files.

 |

5.  Set the duration \(only for Subscription instances\) and quantity, and click **Buy Now**.

    **Note:** For a Subscription instance, you can:

    -   Select **Auto Renew** in the **Duration** section. Then the system can automatically deduct fees to extend the validity period of your instance. For example, if you purchase a three-month Subscription instance with **Auto Renew** selected, the system automatically deducts frees of three months when the instance is about to expire.
    -   Click **Add to Cart** and then click the cart to place the order.
6.  On the **Order Confirmation** page, review the order information, select **Terms of Service, Service Level Agreement, and Terms of Use**, click **Pay Now**, and complete the payment.

## What to do next {#section_gfp_axw_21c .section}

1.  In the upper left corner of the [RDS console](https://rdsnext.console.aliyun.com), select the region where the instance is located, and view the instance details.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156346434136543_en-US.png)

2.  [Configure a whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Configure a whitelist.md#).
3.  [Create a databse account](intl.en-US/Quick Start for MySQL/Initial configuration/Create accounts and databases.md#).
4.  [Apply for an Internet address](intl.en-US/Quick Start for MySQL/Initial configuration/Apply for an Internet address.md#) \(if you want to access RDS through the Internet\).
5.  [Connect to the RDS instance](intl.en-US/Quick Start for MySQL/Connect to an RDS for MySQL instance.md#).

## FAQ {#section_0a8_omz_gyu .section}

How do I authorize a RAM user to manage RDS instances?

See [Manage RDS permissions by using RAM](https://www.alibabacloud.com/help/doc-detail/58932.htm).

## APIs {#section_enw_cvk_fde .section}

|API|Description|
|---|-----------|
|[CreateDBInstance](../../../../intl.en-US/API Reference/Instance management/CreateDBInstance.md#)|Used to create an RDS instance.|


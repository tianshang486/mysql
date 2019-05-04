# Create an RDS for MySQL instance {#concept_wzp_ncf_vdb .concept}

You can use the RDS console or APIs to create an RDS instance. For more information about instance pricing, see [../../../../dita-oss-bucket/SP\_60/DNMYSQ1864174/EN-US\_TP\_7805.md\#](../../../../intl.en-US/Purchase Guide/Billing methods and billing items.md#). This document describes how to use the RDS console to create an instance. For more information about how to use APIs to create an instance, see [CreateDBInstance](../../../../intl.en-US/API Reference/Instance management/Create an RDS instance.md#).

## Prerequisites {#section_hyl_tcf_vdb .section}

You have registered an Alibaba Cloud account.

## Precautions {#section_sft_yn0_nsm .section}

-   Subscription instances cannot be converted to Pay-As-You-Go instances.
-   Pay-As-You-Go instances can be converted to Subscription instances. For operation instructions, see [../../../../dita-oss-bucket/SP\_60/DNMYSQ1860058/EN-US\_TP\_7882.md\#](../../../../intl.en-US/User Guide/Billing management/Change the billing method.md#).
-   An Alibaba Cloud account can create up to 30 Pay-As-You-Go instances. You can submit a ticket to apply for increasing the limit.

## Procedure {#section_o45_5cf_vdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  On the Instances page, click **Create Instance**.
3.  Select a billing method:
    -   **Pay-As-You-Go**: indicates post payment \(billed by hour\). For short-term requirements, create Pay-As-You-Go instances, because they can be released at any time to save costs.
    -   **Subscription**: indicates prepayment. You need to pay when creating an instance. For long-term requirements, create Subscription instances because they are more cost-effective. Furthermore, the longer the subscription, the higher the discount.
4.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|Indicates the location of the RDS instance you want to purchase. The region cannot be changed after the purchase.     -   Select the region closest to your users for high access speed.
    -   Make sure to select the region where your ECS instance is deployed so that the ECS instance can access the RDS instance through the intranet; otherwise, they intercommunicate through the Internet and the access speed is affected.
 |
    |**DB Engine**| The supported database engines are MySQL, SQL Server, PostgreSQL, PPAS, and MariaDB TX.

 In this example, select MySQL.

 **Note:** Different engines support different database engines.

 |
    |**Version**| For RDS for MySQL, the supported versions are MySQL 5.5, 5.6, and 5.7.

 **Note:** Different regions support differen database versions.

 |
    |**Edition**|RDS for MySQL instances support the Basic Edition and High-availability Edition.     -   Basic Edition: It provides a single node and separates computing from storage, and is extremely cost-effective.
    -   High-availability Edition: It adopts the high-availability architecture with one master node and one slave node. It is applicable to over 80% of scenarios.
 **Note:** Different database versions support different series \(editions\). For more information on the product series, see [../../../../dita-oss-bucket/SP\_60/DNMYSQ1821992/EN-US\_TP\_7787.md\#](../../../../intl.en-US/Product Introduction/Product series/Product series overview.md#).

 |
    |**Zone**| A zone is a physical area within a region. Different zones in the same region are basically the same.

 For a High-availability Edition instance, you can choose multiple zones \(such as Zone F + Zone G\), which means the master and slave nodes of the instance will be in differen zones. This inceases availability and does not require extra fees. For more information, see [Disaster tolerance](https://www.alibabacloud.com/help/doc-detail/53624.htm).

**Note:** Not all regions support multiple zones.

 |
    |**Network Type**|     -   **Classic Network**: indicates the traditional network type.
    -   **VPC** \(recommended\): short for Virtual Private Cloud\). A VPC provides higher security and performance than the classic network.

**Note:** Make sure the network type is the same as that of your ECS instance so that the ECS instance can access the RDS instance through the intranet.

 |
    |**Type**| Indicates instance specifications. For specific resources \(CPU cores, memory, maximum number of connections, and IOPS\) provided by each instance type, see [../../../../dita-oss-bucket/SP\_60/DNMYSQ1821992/EN-US\_TP\_7793.md\#](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 RDS supports the following instance type families:

     -   **Common instance**: has its dedicated memory and I/O resources, but shares CPU and storage resources with other common instances on the same server.
    -   **Dedicated instance**: has it dedicated CPU, memory, storage, and I/O resources.
 For example, **8 Cores, 32 GB** indicates a common instance; **8 Cores, 32 GB \(Dedicated\)** is a dedicated instance;

 |
    |**Capacity**| The capacity is used for storing data, system files, binlog, and transaction files.

 |

5.  Set the duration \(only for Subscription instances\) and quantity, and click **Buy Now**.

    **Note:** For Subscription instances, you can also click **Add to Cart** and then click the cart to place the order.

6.  On the **Order Confirmation** page, review order information, select **Product Terms of Service and Service Level Notice and Terms of Use**, click **Pay Now**, and complete the payment.

## Next Steps {#section_gfp_axw_21c .section}

1.  Find the instance as folows:

    At the upper left corner of the [RDS console](https://rdsnext.console.aliyun.com), select the region where the instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155697657736543_en-US.png)

2.  [EN-US\_TP\_7816.md\#](intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md#).
3.  [Create a databse account](intl.en-US/Quick Start for MySQL/Initial configuration/Create accounts and databases.md#).
4.  [EN-US\_TP\_7817.md\#](intl.en-US/Quick Start for MySQL/Initial configuration/Apply for an Internet address.md#) \(if you want to access RDS through the Internet\).
5.  [Connect to the RDS instance](intl.en-US/Quick Start for MySQL/Connect to an instance.md#).

## FAQs {#section_0a8_omz_gyu .section}

How do I authorize a RAM user to manage RDS instances?

Answer: See [Manage RDS permissions by using RAM](https://www.alibabacloud.com/help/doc-detail/58932.htm).

## Related API {#section_enw_cvk_fde .section}

|API|Description|
|---|-----------|
|[../../../../dita-oss-bucket/SP\_60/DNMYSQ1851749/EN-US\_TP\_8086.md\#](../../../../intl.en-US/API Reference/Instance management/Create an RDS instance.md#)|Create an RDS instance..|


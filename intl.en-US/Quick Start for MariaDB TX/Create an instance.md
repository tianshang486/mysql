# Create an instance {#concept_wzp_ncf_vdb .concept}

You can use the RDS console or an API to create an RDS instance. For more information about instance pricing, see [Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15zCpnIt#pricing). This document describes how to use the RDS console to create an instance. If you need to use an API to create an instance, see [CreateDBInstance](../../../../../intl.en-US/API Reference/Instance management/Create an RDS instance.md#).

## Prerequisites {#section_hyl_tcf_vdb .section}

You have registered an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.html).

## Procedure {#section_o45_5cf_vdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/?spm=5176.doc43185.2.7.mR2Syx).
2.  On the Instances page, click **Create Instance**.
3.  Select **Subscription** or **Pay-As-You-Go**.
    -   **Subscription** indicates prepayment, which means you need to pay the monthly or yearly price when creating an instance. This is cost-effective if you want to use the instance for one month or more.
    -   **Pay-As-You-Go** indicates costs are automatically deducted from your Alibaba Cloud account by hour. You can release the instance at any time. This is cost-effective if you only want to use the instance temporarily.
4.  Select the instance configuration. The parameters are described as follows:
    -   Basic configuration
        -   Region and zone: Select the region and zone in which the instance is located. Some regions support both single-zone and multi-zone instances, while some regions support only single-zone instances.

            **Note:** Products in different regions cannot intercommunicate through the intranet, and you cannot change the instance region after creating an instance. Therefore, exercise caution when you select the region.

        -   Database engine: RDS supports MySQL, SQL Server, PostgreSQL, PPAS, and MariaDB TX. Different database types are supported in different regions.
        -   Version: indicates the database version. The MariaDB TX version is 10.3.
        -   Series: RDS for MariaDB TX instances support the High-availability Edition. For more information, see [../../../../../dita-oss-bucket/SP\_60/DNMYSQ1821992/EN-US\_TP\_7787.md](../../../../../intl.en-US/Product Introduction/Product editions/General introduction to product series.md).
    -   Network type: RDS supports only virtual private cloud \(VPC\), which is more secure than traditional classic networks. For more information, see [Network types](../../../../../intl.en-US/User Guide/Connection management/Set network type.md#).
    -   Specifications: indicate the CPU and memory occupied by the instance, the number of connections, and the maximum IOPS. For more information about instance specifications, see [Instance type list](../../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).
    -   Storage: indicates space used by data, system files, binlog files, and transaction files.
    -   Subscription time: indicates the duration of a Subscription instance.
    -   Quantity: indicates the number of instances with the same configurations to be purchased.
5.  Click **Buy Now** to go to the **Confirm Order** page.
6.  Select **Product Terms of Service and Service Level Notice and Terms of Use**, and then click **Pay Now**.


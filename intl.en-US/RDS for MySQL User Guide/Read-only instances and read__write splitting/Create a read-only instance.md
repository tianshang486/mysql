# Create a read-only instance {#concept_ghp_wq5_vdb .concept}

You can create read-only instances to process massive read requests sent to the database and increase the application throughput. A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances through the native replication capability of MySQL.

## Attention {#section_dbp_zq5_vdb .section}

-   Currently the following instances support read-only instances:
    -   MySQL 5.7 High-Availability Edition \(based on local SSDs\)
    -   MySQL 5.6
    -   SQL Server 2017
-   Quantity of read-only instances

    |Database type|Memory|Max number of read-only instances|
    |-------------|------|---------------------------------|
    |MySQL|≥ 64 GB|10|
    |< 64 GB|5|
    |SQL Server|Any|7|

-   Read-only instance is subject to an additional charge and its billing method is Pay-As-You-Go. For more information, see [Pricing](https://www.alibabacloud.com/en/product/apsaradb-for-rds?spm=a3c0i.o26117en.a3.1.FZgSTK#pricing) for read-only instances.
-   The read-only instance automatically copies the whitelist its master instance, but the whitelist of the read-only instance and that of the master instance are independent. To modify the whitelist of the read-only instance, see [Set a whitelist](intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md#).

## Procedure { .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the target instance to visit the Basic Information page.
4.  In the **Instance Distribution** area, click **Add Read-only Instance**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7827/15575426606172_en-US.png)

5.  On the purchasing page, choose the configuration of the read-only instance, and then click **Buy Now**.

    **Note:** 

    -   We recommend that the read-only instance and the master instance be in the same VPC.
    -   To guarantee sufficient I/O for data synchronization, we recommend that the configuration of the read-only instance \(the memory\) is not less than that of the master instance.
    -   We recommend that you purchase multiple read-only instances to improve availability.
6.  Select **Product Terms of Service and Service Level Notice and Terms of Use**, and then click **Pay Now**.
7.  After creating the read-only instance, you can view it on the Instances page, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7827/15575426602617_en-US.png)



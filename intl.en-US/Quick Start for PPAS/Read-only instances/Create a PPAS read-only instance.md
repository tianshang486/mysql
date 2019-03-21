# Create a PPAS read-only instance {#concept_gsm_zz1_ygb .concept}

You can create read-only instances to handle large numbers of read requests and increase the application throughput. A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances.

For more information, see [Introduction to PPAS read-only instances](intl.en-US/Quick Start for PPAS/Read-only instances/Introduction to PPAS read-only instances.md#).

## Pricing {#section_vqk_qbx_dhb .section}

The billing method of read-only instances is Pay-As-You-Go \(billed by hour.\). The costs are the same as a master instance. For more information, see [Pricing](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15K8Buqg#pricing).

## Prerequisites {#section_kdj_3gb_ygb .section}

-   The instance is an RDS for PPAS 10.0 instance.
-   The configuration of the master instance must be at least 8-core 32 GB \(dedicated or dedicated-host instance\).

## Attention {#section_dbp_zq5_vdb .section}

-   You can create read-only instances under a master instance and cannot switch an existing instance to read-only instances.
-   Creating a read-only instance does not affect the master instance because the read-only instance copies data from the slave node.
-   Read-only instances do not inherit parameter settings of the master instance, but use default parameter settings. You can modify the parameter settings on the console.
-   Specifications and storage capacity of each read-only instance cannot be lower than those of the master instance.
-   Each master instance can have up to five read-only instances.

## Create a read-only instance {#section_ix3_db1_1hb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315089940887_en-US.png)

3.  Find the instance and click the instance ID.
4.  Click **Add Read-only instance**.

    ![添加只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315089941248_en-US.png)

5.  On the purchase page, select instance configurations and click **Buy Now**.

    ![购买界面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315090041249_en-US.png)

    **Note:** Suggestions:

    -   Deploy read-only instances and the master instance in the same VPC.
    -   The configuration \(memory and storage\) of each read-only instance be equal to or higher than that of the master instance.
    -   You can deploy multiple read-only instances to improve availability and horizontally scale performance.
6.  Review order information, select **Product Terms of Service and Service Level Notice and Terms of Use**, click **Pay Now**, and complete the payment.

The instance creation takes a few minutes.

## View read-only instances {#section_dgy_ylr_52b .section}

**View the instance in the instance list**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the read-only instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315089940887_en-US.png)

3.  Find the read-only instance and click the instance ID.

    ![选择只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315090041250_en-US.png)


**View the read-only instance on the master instance information page**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the master instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315089940887_en-US.png)

3.  Find the master instance and click its ID.
4.  On the **Basic Information** page, place the mouse over the number of read-only instances and click the read-only instance ID.

    ![主实例内跳转只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315090041253_en-US.png)


## View the delay of a read-only instance {#section_sww_dv5_vdb .section}

When a read-only instance synchronizes data from the master instance, the read-only instance may lag behind the master instance by a small amount of time. You can view the delay on the basic information page of the read-only instance.

![只读实例延迟](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/134808/155315090041254_en-US.png)

## Related API {#section_hcn_555_jgb .section}

|API|Description|
|---|-----------|
|[Create a read-only instance](../../../../../intl.en-US/API Reference/Instance management/Create a read-only instance.md)|Create an RDS read-only instance|


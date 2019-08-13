# Create a PPAS read-only instance {#concept_gsm_zz1_ygb .concept}

You can create read-only instances to handle large numbers of read requests and increase the application throughput. A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances.

For more information, see [Introduction to PPAS read-only instances](intl.en-US/Quick Start for PPAS/Read-only instances/Introduction to PPAS read-only instances.md#).

## Prerequisites {#section_1y2_hre_6jl .section}

-   The master instance is an RDS for PPAS 10.0 instance.
-   The configuration of the master instance must be at least 8-core 32 GB \(dedicated or dedicated-host instance\).

## Precautions {#section_dbp_zq5_vdb .section}

-   You can create read-only instances under a master instance but cannot switch an existing instance to a read-only instance.
-   Creating a read-only instance does not affect the master instance because the read-only instance copies data from the slave instance.
-   Read-only instances do not inherit parameter settings of the master instance, but use default parameter settings. You can modify the parameter settings on the console.
-   Specifications and storage capacity of each read-only instance cannot be lower than those of the master instance.
-   Each master instance can have up to five read-only instances.
-   A read-only instance is charged according to the Pay-As-You-Go billing method. That is, fees are deducted for a read-only instance once every hour.

## Create a read-only instance {#section_ix3_db1_1hb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156566582036543_en-US.png)

3.  Find the target instance and click its ID.
4.  Click **Add Read-only Instance**.

    ![添加只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/156566582039780_en-US.png)

5.  On the purchase page, select the instance configuration and click **Buy Now**.

    ![购买界面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/156566582139782_en-US.png)

    **Note:** 

    -   We recommend that you deploy read-only instances and the master instance in the same VPC.
    -   The configuration \(memory and storage\) of each read-only instance must be equal to or higher than that of the master instance.
    -   You can deploy up to five read-only instances to improve availability and horizontally scale performance.
6.  On the Order Confirmation page, review the order information, select **Terms of Service, Service Level Agreement, and Terms of Use**, click **Pay Now**, and complete the payment.

The instance creation takes a few minutes.

## View a read-only instance {#section_dgy_ylr_52b .section}

**View a read-only instance in the instance list** 

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the read-only instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156566582036543_en-US.png)

3.  In the instance list, find the read-only instance and click its ID.

    ![选择只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/156566582139783_en-US.png)


**View a read-only instance on the Basic Information page of the master instance**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the master instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156566582036543_en-US.png)

3.  Find the master instance and click its ID.
4.  On the Basic Information page of the master instance, move the pointer over the number below **Read-only Instance** and click the ID of the read-only instance.

    ![主实例内跳转只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/156566582139784_en-US.png)


## View the delay of a read-only instance {#section_sww_dv5_vdb .section}

When a read-only instance synchronizes data from the master instance, the read-only instance may lag behind the master instance by a small amount of time. You can view the delay on the Basic Information page of the read-only instance.

![只读实例延迟](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/156566582239785_en-US.png)

## APIs {#section_hcn_555_jgb .section}

|API|Description|
|---|-----------|
|[CreateReadOnlyDBInstance](../intl.en-US/API Reference/Instance management/CreateReadOnlyDBInstance.md)|Used to create an RDS read-only instance.|


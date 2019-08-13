# Create an RDS for MySQL read-only instance {#concept_ghp_wq5_vdb .concept}

You can create read-only instances to process massive read requests sent to the database and increase the application throughput. A read-only instance is a read-only copy of the master instance. Changes to the master instance are also automatically synchronized to all relevant read-only instances through the native replication capability of MySQL.

## Prerequisites {#section_u9c_290_176 .section}

The version of your RDS master instance is as follows:

-   MySQL 8.0 High-availability Edition \(with local SSD\)
-   MySQL 5.7 High-availability Edition \(with local SSD\)
-   MySQL 5.6

## Precautions {#section_dbp_zq5_vdb .section}

-   You can create read-only instances in your master RDS instance. However, you cannot switch an existing instance to a read-only instance.
-   Creating a read-only instance does not affect your master RDS instance because the read-only instance copies data from the slave instance.
-   A read-only instance does not inherit the parameter settings of your master RDS instance. Instead, default parameter settings are generated. You can modify the parameter settings of a read-only instance on the RDS console.
-   The quantity of read-only instances is as follows.

    |Database type|Memory|Max number of read-only instances|
    |-------------|------|---------------------------------|
    |MySQL|≥ 64 GB|10|
    |< 64 GB|5|

-   A read-only instance is charged according to the Pay-As-You-Go billing method. Specifically, the fees for a read-only instance are deducted once per hour depending on the instance specifications. For more information, see the "Read-Only Instances" part at [Pricing](https://www.alibabacloud.com/en/product/apsaradb-for-rds?spm=a3c0i.o26117en.a3.1.FZgSTK#pricing).

## Create a read-only instance {#section_c1s_pt7_osg .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567605236543_en-US.png)

3.  Find the target instance and click its ID.
4.  Click **Add Read-only Instance**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7827/15656760526172_en-US.png)

5.  On the purchase page, choose the configuration of the read-only instance, and then click **Buy Now**.

    **Note:** 

    -   We recommend that the read-only instance and the master instance be in the same VPC.
    -   To guarantee sufficient I/O for data synchronization, we recommend that the configuration of the read-only instance \(the memory\) is greater than or equal to that of the master instance.
    -   We recommend that you purchase multiple read-only instances based on your business needs to improve availability.
6.  On the **Order Confirmation** page, review the order information, select the terms and agreements as prompted, click **Pay Now**, and complete the payment.

    The instance creation takes a few minutes.


## View a read-only instance {#section_z6s_6ed_yyf .section}

**View a read-only instance in the instance list** 

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the read-only instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567605236543_en-US.png)

3.  In the instance list, find the read-only instance and click its ID.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7827/15656760522617_en-US.png)


**View a read-only instance on the Basic Information page for the master instance**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the master instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567605236543_en-US.png)

3.  In the instance list, find the master instance and click its ID.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7827/156567605332584_en-US.png)

4.  On the Basic Information page of the master instance, move the pointer over the number below **Read-only Instance** and click the ID of the read-only instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7827/15656760539379_en-US.png)


## View the delay time of a read-only instance {#section_84x_dyf_ok0 .section}

When a read-only instance synchronizes data from the master instance, the read-only instance may lag behind the master instance by a small amount of time. You can view the delay on the Basic Information page of the read-only instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7828/15656760532636_en-US.png)

## APIs {#section_ak8_gmq_vui .section}

|API|Description|
|---|-----------|
|[CreateReadOnlyDBInstance](../../../../intl.en-US/API Reference/Instance management/CreateReadOnlyDBInstance.md#)|Used to create an RDS read-only instance.|


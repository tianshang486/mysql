# Change configurations {#concept_efl_pln_wdb .concept}

You can upgrade or downgrade RDS configurations at any time. The new configurations take effect immediately or during the specified maintenance time window.

## Configuration items {#section_276_io6_qzd .section}

This topic describes how to change the instance series, specifications, storage capacity, storage type, and zone. If you want to horizontally scale read capabilities, use read-only instances according to [Introduction to MySQL read-only instances](../../../../intl.en-US/Quick Start for MySQL/Scale instances/Read-only instance/Introduction to MySQL read-only instances.md#), [Introduction to SQL Server read-only instances](../../../../intl.en-US/Quick Start for SQL Server/Read-only instances/Introduction to SQL Server read-only instances.md#), [Introduction to PostgreSQL read-only instances](../../../../intl.en-US/Quick Start for PostgreSQL/Read-only instances/Introduction to PostgreSQL read-only instances.md#), and [Introduction to PPAS read-only instances](../../../../intl.en-US/Quick Start for PPAS/Read-only instances/Introduction to PPAS read-only instances.md#).

|Item|Description|
|----|-----------|
|Series \(Edition\)| For MySQL 5.7, the Basic Edition can be changed to High-availability Edition.

 |
|Zone|To change the zone, use the "[Migrate instances across zones](intl.en-US/User Guide/Instance management/Migrate instances across zones.md#)" function rather than the configuration change function.|
|[Specifications \(Type\)](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#)| You can change the specifications for any RDS instance.

 |
|Storage capacity| You can increase the storage capacity for any RDS instance. For the capacity range, see the RDS console or [Instance type list](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 You can decrease the storage capacity only by changing the configurations during [instance renewal](intl.en-US/User Guide/Billing management/Manually renew a Subscription instance.md#), and only when the storage type is local SSD.

 **Note:** 

-   You cannot decrease the storage capacity if the storage type is cloud SSD.
-   If the storage capacity range of the current instance specifications cannot meet your requirements, change the instance specifications.

 |
|Storage type|If you change MySQL 5.7 Basic Edition to High-availability Edition, the storage type changes from cloud SSD to local SSD.|

**Note:** Changing the preceding configurations does not change the instance connection addresses.

## Billing {#section_nfs_fcg_zxf .section}

See [Billing details for configuration change](../../../../intl.en-US/Purchase Guide/Billing details about configuration change.md#).

## Prerequisites {#section_okk_p9w_ouf .section}

Your Alibaba Cloud account does not have an unpaid renewal order.

## Precautions {#section_ahv_8vk_x5l .section}

-   When the configuration change is taking effect, RDS may be disconnected for about 30 seconds, and most operations related to databases, accounts, and networks cannot be performed. Therefore, perform the configuration change during off-peak hours or make sure that your application has the automatic reconnection mechanism.
-   If the instance belongs to Basic Edition \(which has no slave node as hot backup\), it becomes unavailable for a long time during the configuration change.
-   Before and after the configuration change, do not restart the instance; otherwise, the instance may be abnormal and locked.

## Procedure {#section_btg_cln_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  n the upper-left corner, select the region where the target instance is located.
3.  Click the instance ID to visit the Basic Information page.
4.  Click **Change configuration**.
5.  Change the configuration according to [Configuration items](#section_276_io6_qzd).
6.  Specify the time at which you want to change the configuration.

    -   **Switch immediately after data migration**: Change the configuration immediately after the data migration.
    -   **Switch during maintenance**: Change the configuration during the [maintenance period](intl.en-US/User Guide/Instance management/Configure the maintenance period.md#).
    **Note:** To change the maintenance period, do the following:

    1.  Click **Modify**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7891/15658369053043_en-US.png)

    2.  In the Configuration Information section, change the maintenance period and click **Save**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7891/15658369067257_en-US.png)

    3.  Go back to the configuration change page, refresh the page, and change the configurations again.
7.  Select **Product Terms of Service and Service Level Notice and Terms of Use** and click **Upgrade Now**.

## FAQ {#section_lp4_zwy_1dj .section}

1.  How can I change the storage type \(local SSD, cloud SSD, or cloud SSD\) of an instance?

    If you want to change the storage type of an instance that is not a MySQL, SQL Server, or PostgreSQL instance, you can save the instance data to your computer and then migrate the data to the cloud.

2.  Can I change the zone and edition of an instance?

    You can change the zone and edition of an instance as needed. For more information, see [Migrate instances across zones](intl.en-US/User Guide/Instance management/Migrate instances across zones.md#). For information about how to change the edition of an instance, see [Upgrade the database](intl.en-US/User Guide/Instance management/Upgrade the database version.md#) and [Upgrade SQL Server 2008 R2](https://www.alibabacloud.com/help/zh/doc-detail/111658.htm).

3.  Do I need to migrate data if I only want to expand the storage capacity of an instance?

    You need to check whether the server where your instance is located provides sufficient storage capacity. If yes, you do not need to migrate data and can directly expand the storage capacity. If no, you need to migrate data to a server that provides sufficient storage capacity before you expand the storage capacity.



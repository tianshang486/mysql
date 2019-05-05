# Change configurations {#concept_efl_pln_wdb .concept}

You can upgrade or downgrade RDS configurations at any time. The new configurations take effect immediately or during the specified maintenance time window.

## Configuration items {#section_276_io6_qzd .section}

**Note:** This article describes how to chnage the instance series, specifications, storage capacity, storage type, and zone. If you want to horizontally scale read capabilities, use read-only instances.

|Item|Description|
|----|-----------|
|Series \(Edition\)| For MySQL 5.7, the Basic Edition can be changed to High-availability Edition.

 |
|[Specifications \(Type\)](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#)| You can change the specifications for any RDS instance.

 |
|Storage capacity| You can increase the storage capacity for any RDS instance. For the capacity range, see the RDS console or [Instance type list](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 You can decrease the storage capacity only by changing the configurations during [instance renewal](intl.en-US/User Guide/Billing management/Manually renew a Subscription instance.md#), and only when the storage type is local SSD.

 **Note:** 

-   You cannot descrease the storage capacity if the storage type is cloud SSD.
-   If the storage capacity range of the current specifications cannot meet your requirements, change the specifications.

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
2.  At the upper-left corner, select the region where the target instance is located.
3.  Click the instance ID to visit the Basic Information page.
4.  Click **Change configuration**.
5.  Change the configurations by referring to [Configuration items](#section_276_io6_qzd).
6.  Configuration changes involve data migrations. You can choose to switch the configuration immediately after the data migration or during the [maintenance period](intl.en-US/User Guide/Instance management/Configure the maintenance period.md#).

    **Note:** To change the maintenance period, do the following:

    1.  Click **Modify**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7891/15570736243043_en-US.png)

    2.  In the Configuration Information area, change the maintenance period and click **Save**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7891/15570736247257_en-US.png)

    3.  Go back to the configuration change page, refresh the page, and change the configurations again.
7.  Select **Product Terms of Service and Service Level Notice and Terms of Use** and click **Upgrade Now**.


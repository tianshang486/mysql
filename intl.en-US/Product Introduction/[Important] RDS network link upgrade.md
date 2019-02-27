# \[Important\] RDS network link upgrade {#concept_vyz_wf2_wfb .concept}

To ensure better stability and performance, we recommend that you upgrade the network connection mode of your RDS instances from the high-security mode \(database proxy mode\) to the high-performance mode \(standard mode\).

## Potential risks of not performing the upgrade {#section_v4k_gsj_ngb .section}

The high-security mode may encounter temporary instability in certain scenarios. To ensure stability of your services, we recommend that you perform the upgrade as soon as possible.

## Benefits {#section_gwv_mkr_mgb .section}

After the upgrade, the network link is shorter so that:

-   The network becomes more stable.
-   The average response time is reduced by 20% and performance is significantly improved.

## Instances that need to be upgraded {#section_hzy_lkr_mgb .section}

RDS for MySQL, PostgreSQL, PPAS instances in high-security mode \(database proxy mode\).

To check whether an instance is in high-security mode \(database proxy mode\), perform the following:

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64586/155128312637659_en-US.png)

3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation pane, click **Connection Options**. Check the **Database Proxy Status \(High-Security Mode\)** field.
    -   If the status is **Disabled**, the instance does not need to be upgraded.
    -   If the status is **Enabled**, the instance needs to be upgraded.

        **Note:** 

        -   If an MySQL instance has enabled read/write splitting, the instance does not need to be upgraded. Alibaba Cloud will provide another upgrade plan for such instances.
        -   If an instance has read-only instances, you only need to upgrade the master instance and then the read-only instances will be automatically upgraded

## Impact of the upgrade {#section_gdm_pkr_mgb .section}

During the upgrade, the RDS instance being upgraded will be disconnected for about 30 seconds. Make sure that your services can automatically reconnect to the RDS instance.

## Upgrade method 1 {#section_cdd_rkr_mgb .section}

1.  On the **Connection Options** page, click **Switch Access Mode**.

    **Note:** This button is displayed only if the access mode of the instance is high-security mode \(database proxy mode\).

2.  In the displayed dialog box, click **Confirm**.
3.  Check that services are running properly.

    **Note:** This step is important.


## Upgrade method 2 {#section_gdh_ztr_mgb .section}

1.  On the **Connection Options** page, click the slider next to **Database Proxy Status \(High-Security Mode\)**.
2.  In the displayed dialog box, click **Confirm**.
3.  Check that services are running properly.

    **Note:** This step is important.


## FAQ {#section_kgg_ppj_ngb .section}

1.  How do I know whether an instance needs to be upgraded?

    See [Instances that need to be upgraded](#section_hzy_lkr_mgb).

2.  I cannot upgrade my instance. Why?

    If a MySQL instance has enabled read/write splitting, the instance currently cannot be upgraded. Alibaba Cloud will provide another upgrade plan for such instances.

3.  What do I need to do for my services after an upgrade?
    -   During an upgrade, the instance being upgraded may be disconnected. Make sure that your services have an automatic reconnection mechanism; otherwise, you may need to manually restart your services.
    -   After an upgrade, the connection address, IP address, and other settings of the RDS instance remain unchanged, so you do not need to make any changes to your applications.
4.  Can I switch back to the high-security mode?

    You do not need to switch back to the high-security mode. The high security mode was designed to support the coexistence of different network types \(Internet and intranet\), but now the high-performance mode \(standard mode\) also serves that purpose.

5.  If a master instance has read-only instances, do I need to upgrade each read-only instance?

    No. You only need to upgrade the master instance. The attached read-only instances are then automatically upgraded.



# Disabling the database proxy mode {#concept_jlf_hpq_wdb .concept}

Disabling the database proxy mode helps to increase RDS instance performance.

**Note:** The database proxy mode may cause service instability in certain circumstances. For smooth service operation, we recommend that you upgrade the network connection mode of your RDS instance as soon as possible. For more information, see [\[Important\] RDS network link upgrade](../../../../dita-oss-bucket/SP_60/DNMYSQ1821992/EN-US_TP_64586.md#).

## Precautions {#section_vb8_do1_i5w .section}

-   You can only disable the database proxy mode \(that is, switch from the database proxy mode to the standard mode\). However, you cannot enable the database proxy mode \(that is, switch from the standard mode to the database proxy mode\).
-   During the access mode switching, your RDS instance may be disconnected once for about 30 seconds. We recommend that you perform the switching during off-peak hours or make sure that your application can automatically reconnect to the RDS instance.
-   RDS instances in SQL Server 2008 R2 use the database proxy mode by default when running in VPCs. They cannot be switched to the standard mode.
-   RDS instances in SQL Server 2008 R2 use the standard mode by default when running in classic networks. They cannot be switched to the database proxy mode or VPCs.

## Prerequisites {#section_hc7_xyi_pdm .section}

The database proxy mode is enabled for your RDS instance.

**Note:** The database proxy is enabled only when your RDS instance has a **Database Proxy** tab page.

## Procedure {#section_rwz_xtz_zgb .section}

**Method 1**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region.
3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  Click **Switch Access Mode**.

    **Note:** This button is available only if you have enabled the database proxy mode.


**Method 2**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region.
3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation pane, click **Database Proxy**.
5.  On the **Database Proxy** tab page, click the slider to turn on or off the database proxy mode.

    **Note:** This tab page is available only if you have enabled the database proxy mode.



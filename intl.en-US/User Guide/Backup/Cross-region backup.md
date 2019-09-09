# Cross-region backup {#concept_405443 .concept}

ApsaraDB RDS for MySQL provides the cross-region backup function that automatically synchronizes local backup files to OSS in another region. Cross-region backup can be used for monitoring and disaster recovery.

**Note:** 

-   This topic describes the cross-region backup function that is used to back up files to another region. For details about the default backup function, see [Back up RDS data](intl.en-US/User Guide/Backup/Back up RDS data.md#).
-   If you have completed cross-region backup, you can use [Cross-region restoration](intl.en-US/User Guide/Recovery/Cross-region restoration.md#) to restore data to a new instance in the destination region.

## Differences between cross-region backup and default backup {#section_yr0_1yb_8r9 .section}

-   Default backup is enabled by default while cross-region backup must be manually enabled.
-   Cross-region backup stores data in another region while default backup stores data in the source region.
-   You can use cross-region backup to restore data to a new instance in the source region or a different destination region. You can use default backup to [restore data to a new instance in the source region or to the original instance](intl.en-US/User Guide/Recovery/Cross-region restoration.md#).
-   After the instance is released, the cross-region backup data is retained until the retention period expires. The backup data is retained for seven days by default.

## Prerequisites {#section_lb1_pre_6b7 .section}

The instance must be of the following versions:

-   MySQL 5.7 High-availability Edition \(based on local SSDs\)
-   MySQL 5.6

## Pricing {#section_tt2_3o4_8rf .section}

The pricing for cross-region backup is as follows:

-   Geo-OSS storage fee: 0.0002 USD/GB/Hour
-   Traffic fee: Cross-region backup is free during the open beta test.

**Note:** Currently, you only need to pay for the traffic fee, but since October 23, 2019 you must also pay for the geo-OSS storage fee.

## Precautions {#section_hzj_bnl_xhb .section}

-   Cross-region backup can be used to restore data to a instance in the source or destination region.
-   Cross-region backup can be used only to restore data to a new instance.
-   Cross-region backup does not affect default backup, both of which exist \(the local backup is copied to the OSS of another region\).
-   When cross-region backup is enabled, and there is no valid backup set in the last 24 hours, the data of the secondary RDS instance will be backed up automatically.
-   Cross-region backup is not supported in some regions. The following table lists the regions that support cross-region backup.

    |Source region|Destination region that supports backup|
    |-------------|---------------------------------------|
    |China \(Hangzhou\)|China \(Shanghai\), China \(Qingdao\), China \(Shenzhen\)|
    |China \(Shanghai\)|China \(Hangzhou\), China \(Qingdao\), China \(Shenzhen\)|
    |China \(Qingdao\)|China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\)|
    |China \(Beijing\)|China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Shenzhen\)|
    |China \(Shenzhen\)|China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\)|
    |Hong Kong|China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Shenzhen\)|


## Method 1 to enable cross-region backup {#section_b1d_nv0_q4c .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/328067/156799247948250_en-US.png)

3.  Find the instance. In the Actions column corresponding to the instance, choose **More** \> **Cross-region Backup Settings** from the shortcut menu.
4.  Configure the following parameters:

    |Parameter|Description|
    |---------|-----------|
    |**Cross-region Backup Status**|Specifies whether to enable cross-region backup. Select **Enable**.|
    |**Backup Region**|The region where the backup data is stored. The local backup files are automatically copied to the OSS in this region.|
    |**Cross-region Retention Period**|The retention period of the backup data in days. You can specify an integer from 7 to 1825. Cross-region backup files can be retained for a maximum of five years. **Note:** If the RDS instance expires or is released, the retention time of the cross-region backup file is not affected. You can click [Cross-region Backup](#) in the left-side navigation pane to view the backup files that do not expire.

 |
    |**Cross-region Log Backup Status**|Specifies whether to enable cross-region log backup. After it is enabled, the backup file of the local log is automatically copied to the OSS in this region.|

    ![Cross-region Backup Settings](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/328067/156799247948555_en-US.png)

5.  Click **OK**.

## Method 2 to enable cross-region backup {#section_lb2_dnl_xhb .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.
3.  Find the instance and click its ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  Click the Cross-region Backup tab and click **Edit**.

    **Note:** If the Cross-region Backup tab is not displayed, make sure the instance meets the [Prerequisites](#section_lb1_pre_6b7).

6.  Configure the following parameters:

    |Parameter|Description|
    |---------|-----------|
    |**Cross-region Backup Status**|Specifies whether to enable cross-region backup. Select **Enable**.|
    |**Backup Region**|The region where the backup data is stored. The local backup files are automatically copied to the OSS in this region.|
    |**Cross-region Retention Period**|The retention period of the backup data in days. You can specify an integer from 7 to 1825. Cross-region backup files can be retained for a maximum of five years. **Note:** If the RDS instance expires or is released, the retention time of the cross-region backup files are not affected. You can click [Cross-region Backup](#) in the left-side navigation pane to view the backup files that do not expire.

 |
    |**Cross-region Log Backup Status**|Specifies whether to enable cross-region log backup. After it is enabled, the backup file of the local log is automatically copied to the OSS in this region.|

    ![Cross-region Backup Settings](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/328067/156799247948555_en-US.png)

7.  Click **OK**.

## Modify cross-region backup settings {#section_ryt_44l_xhb .section}

The cross-region backup menu is added to the RDS console. You can modify the cross-region backup settings even if the instance is released.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com).
2.  In the left-side navigation pane, click **Cross-region Backup**.
3.  Find the instance and click **Edit** in the Cross-region Backup Settings column to modify the backup settings.

    **Note:** If the instance is released, you can only modify the retention period.


**Note:** You can also click **Go to DBS Console** to [create a backup plan](https://www.alibabacloud.com/help/zh/doc-detail/65909.htm).


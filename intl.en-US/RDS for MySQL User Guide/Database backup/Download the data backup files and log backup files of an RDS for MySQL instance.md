# Download the data backup files and log backup files of an RDS for MySQL instance {#concept_yjb_pn4_ydb .concept}

This topic describes how to download the data backup files and log backup files of an RDS for MySQL instance. The downloaded log backup files are not encrypted. You can save the backup files for archiving or use them to restore the instance to an on-premises database.

**Note:** 

An RDS for MySQL instance with SSDs does not support the download of data backup files. You can [restore the data of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Database restoration/Restore the data of an RDS for MySQL instance.md#) or [migrate data from RDS for MySQL to an on-premises MySQL database](intl.en-US/RDS for MySQL User Guide/Data migration and synchronization/Migrate data from RDS for MySQL to an on-premises MySQL database.md#).

## Limits {#section_prg_zhx_wfb .section}

A RAM user who has only the read-only permissions cannot download backup files. You can add the required permissions to a RAM user in the RAM console. For more information, see [Grant backup file download permissions to a RAM user with only read-only permissions](intl.en-US/RDS for MySQL User Guide/Appendixes/Grant backup file download permissions to a RAM user with only read-only permissions.md#).

|DB engine|Data backup download|Log backup download|
|---------|--------------------|-------------------|
|MySQL| -   MySQL 5.5/5.6/5.7/8.0 \(with local SSDs\): support the download of full physical data backup files and logical data backup files.
-   MySQL 5.7/8.0 Basic/High-availability Edition \(with ESSDs/SSDs\): do not support the download of data backup files.

 |All versions support the download of log backup files. **Note:** For more information about binary logs, see [How do I use the mysqlbinlog command to view the binary logs of an RDS for MySQL instance?](../intl.en-US/FAQs/Data backup__recovery/How do I use the mysqlbinlog command to view the binary logs of an RDS for MySQL instance?.md#)

 |

## Procedure {#section_lxw_cn4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156895966236543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  Click the **Data Backup** or Log Backup tab.
    -   If you want to download data backup files, click **Data Backup**.
    -   If you want to download log backup files, click Log Backup
6.  Select a time range and click **Search**.
7.  Find the data or log backup file you want to download, and in the **Actions** column click **Download**.

    **Note:** 

    -   If the **Download** button is unavailable, see [Limits](#section_prg_zhx_wfb).
    -   If you want to use the downloaded data backup file for data restoration, we recommend that you select the data backup file that was generated at the time point closest to the time point from which you want to restore data.
    -   If you want to use the downloaded log backup file to restore your RDS instance to an on-premises database, note the following:
        -   The **Instance ID** of the log backup file must be the same as the **Instance No.** of the selected data backup file.
        -   The start time of the log backup file must be later than the generation time of the selected data backup file and earlier than the time point from which you want to restore data.
8.  In the Download Instance Backup Set or Download Binary Log dialog box, select a download method.

    ![下载实例备份集](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7966/15689596626231_en-US.png)

    |Download method|Description|
    |---------------|-----------|
    |Download|To download the backup file through the public connection address.|
    |Copy Internal Download URL|To copy the internal download URL only. When your ECS instance is located in the same region as the RDS instance, you can log on to your ECS instance and then use the internal download URL to download the backup file. This is faster and more secure.|
    |Copy External Download URL|To copy the external download URL only. This method is suitable when you download the backup file by using other tools.|

    **Note:** In a Linux operating system, you can run the following command to download a data backup file:

    ``` {#codeblock_fax_2u9_7kf}
    wget -c '<Download URL of the data backup file>' -O <User-defined file name>.tar.gz
    ```

    -   The -c parameter is used to enable resumable download.
    -   The -O parameter is used to save the downloaded result as a file with the specified name \(the file extension is .tar.gz or .xb.gz as included in the URL\).
    -   If you enter more than one download URL, then you must include each download URL in a pair of single quotation marks \(''\). Otherwise, the download fails.

## FAQ {#section_cxl_5cn_qgb .section}

1.  Why are there two binary log files that have the same name for an RDS for MySQL instance?

    RDS for MySQL works in the master/slave HA architecture. Therefore, both the master and slave instances generate binary logs. You can distinguish between two binary log files that have the same name based on their **Instance ID**s. To view the IDs of the master and slave instances, you can go to the Service Availability page.

    ![实例编号](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/67074/156895966338570_en-US.png)

2.  What can I use the downloaded data and log backup files for?

    You can use the downloaded data and log backup files to restore data at anytime. For more information, see [Restore data from physical backup files of ApsaraDB for MySQL to an on-premises user-created database](../intl.en-US//Restore data from physical backup files of ApsaraDB for MySQL to an on-premises user-created database.md#).



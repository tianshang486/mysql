# Restore MySQL databases or tables {#concept_ocr_swk_ngb .concept}

In RDS for MySQL 5.6 High-Availability Edition, you can restore databases or tables rather than the entire instance.

**Prerequisites**

-   The instance type is RDS for MySQL 5.6 High-Availability Edition.
-   The region is Singapore. If your instance is in other regions, please [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to apply for activating the function.
-   The instance is running properly and not locked.
-   To restore data from a backup set, the instance must have at least one backup set.
-   To restore data to a point in time, make sure that the log backup function is enabled.

## Precautions {#section_kl1_wrv_ghb .section}

After this function is activated, the backup file format is changed from TAR to XBSTREAM, so the backup files occupy a little more space. Pay attention to the [backup file size](https://www.alibabacloud.com/help/doc-detail/55607.htm#concept-ipg-lm4-ydb) because the excess space that exceeds the free quota will incur costs. You can adjust the backup frequency if needed.

## Procedure {#section_m3j_zlb_3gb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the instance is located.
3.  Click the instance ID.
4.  In the left-side navigation pane, choose **Backup and Recovery**.
5.  In the upper right corner, click **Restore Databases/Tables**.

    **Note:** If this button is not displayed, see Prerequisites in this topic.

    ![库/表级别恢复](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/155405499537783_en-US.png)

6.  Set the following parameters.

    ![库/表级别恢复参数设置1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/155405499537784_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Restore To**|     -   **Restore to Current Instance**: If you select this option, ensure that the instance is not undergoing a migration process.
    -   **Restore to New Instance**
 |
    |**Restore Method**|     -   **By Backup Set**.
    -   **By Time**. This parameter is displayed only if the log backup function is enabled.
 |
    |**Backup Set**|Select a backup set.**Note:** This parameter is displayed only if **Restore Method** is **By Backup Set**.

|
    |**Restore Time**|Select a point in time. You can restore data to any time within the log retention period. To view or modify the log retention period, see [Back up RDS data](https://www.alibabacloud.com/help/doc-detail/26206.htm#concept-l1m-xgn-ydb).**Note:** This parameter is displayed only if **Restore Method** is **By Time**.

|
    |**Databases and Tables to Restore**|Select the databases or tables to restore.|
    |**Selected Databases and Tables**|Selected databases and tables are displayed here.    -   If needed, you can set the database and table names that are used after the restoration.
    -   This area also displays the total size of the selected databases and tables and the available storage of the current instance.
|

7.  Click **OK**. The restoration starts.

    **Note:** If you chose to restore a new instance, the instance purchase page is displayed. After you complete the payment, the restoration starts.



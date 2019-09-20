# Restore the data of an RDS for SQL Server instance {#concept_o52_hlx_52b .concept}

This topic describes how to restore the data of an RDS for SQL Server instance by using a data backup.

You can use one of the following methods to restore the data of an RDS for SQL Server instance:

-   [Restore data to an existing RDS instance](#section_huifu)
-   [Restore data to a new RDS instance](#section_l2n_r4x_52b)
-   [Restore data to the source RDS instance through a temporary instance](#section_ejq_2yz_52b)

## Restore data to an existing RDS instance {#section_huifu .section}

You can restore the data of one or more databases from an RDS instance by backup set or time to this RDS instance or to another existing RDS instance.

This function is available to SQL Server 2012 and SQL Server 2016.

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156895777736543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  In the upper-right corner, click **Restore**.
6.  In the displayed dialog box, select **Restore to Existing Instance** and click **OK**.

    ![恢复到已有实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/156895777710029_en-US.png)

7.  Set the following parameters and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17685/156895777710031_en-US.png)

    **Note:** 

    -   If two databases have the same name, you must select **New Name** and modify the database names.
    -   A new database name can contain lowercase letters, digits, underscores \(\_\), and hyphens \(-\).
    |Parameter|Description|
    |---------|-----------|
    |Restore Method|     -   **By Time**: You can select any time point within the specified log retention period. For more information about how to view or change the log retention period, see [Back up the data of an RDS for SQL Server instance](intl.en-US/RDS for SQL Server User Guide/Data backup/Back up the data of an RDS for SQL Server instance.md#).
    -   **By Backup Set**: You can specify a full or incremental backup set from which you want to restore data.
 |
    |Restore Time|Select the time point from which you want to restore data. This parameter is displayed when the **Restore Method** parameter is set to **By Time**.|
    |Backup Set|Select the backup set from which you want to restore data. This parameter is displayed when the **Restore Method** parameter is set to **By Backup Set**.|
    |Instance|Select the destination RDS instance to which you want to restore data. By default, the system displays the RDS instances \(including the source RDS instance\) that are created by the same Alibaba Cloud account, located in the same region, and use the same DB engine version as the source RDS instance.

 **Note:** If a large number of RDS instances are displayed, you can enter keywords in the search field to find the RDS instance you want.

 |
    |Databases to Restore|     1.  Select the databases you want to restore. By default, all databases of the source RDS instance are displayed and selected.
        -   If you want to restore the data of the whole instance, make sure that all databases are selected.
        -   If you want to restore one or more databases, make sure that these databases are selected.
    2.  Set the names of the restored databases. By default, the system uses the original database names.

**Note:** The names of the restored databases cannot be the same as those of the existing databases in the destination RDS instance.

 |


## Restore data to a new RDS instance {#section_l2n_r4x_52b .section}

You can restore the data of an RDS instance by backup set or time to a new RDS instance. If you choose to restore data by backup set, you can restore some or all databases in the selected backup set.

You must pay for the new RDS instance.

This function is available to SQL Server 2012, SQL Server 2016, and SQL Server 2017.

1.  Log on to the [RDS instance](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156895777736543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  In the upper-right corner, click **Restore**.
6.  In the displayed dialog box, select **Restore to New Instance** and click **OK**.
7.  Select a billing method and set the parameters of the new RDS instance.

    |Parameter|Description|
    |---------|-----------|
    |**Restore Mode**|     -   **By Time**: You can select any time point within the specified log retention period.
    -   **By Backup Set**: You can specify a full or incremental backup set from which you want to restore data.
 |
    |**Restore Point**|Select the time point from which you want to restore data. This parameter is displayed when the **Restore Method** parameter is set to **By Time**.|
    |**Backup Set**|Select the backup set from which you want to restore data. This parameter is displayed when the **Restore Method** parameter is set to **By Backup Set**.|
    |**Database**|     -   **All**: to restore all databases in the selected backup set.
    -   **Part**: to restore some databases in the selected backup set. If you select this option, you must select the databases you want to restore from the left list, and add them to the right list.
 |
    |**Edition/Zone/CPU and Memory/Capacity/Network Type/Duration**|For more information, see [Create an RDS for SQL Server instance](../intl.en-US/Quick Start for SQL Server/Create an RDS for SQL Server instance.md#).|
    |**Quantity**|Specify the number of RDS instances you want to purchase. You can create up to five RDS instances at a time for data restoration.|

8.  Click **Buy Now**.
9.  On the Order Confirmation page, select **Terms of Service, Service Level Agreement, and Terms of Use**, and click **Pay Now** to complete the payment.

## Restore data to the source RDS instance through a temporary instance {#section_ejq_2yz_52b .section}

This function is available to the following DB engine versions and editions:

-   SQL Server 2012 Enterprise Basic Edition
-   SQL Server 2012/2016 Web Basic Edition
-   SQL Server 2008 R2


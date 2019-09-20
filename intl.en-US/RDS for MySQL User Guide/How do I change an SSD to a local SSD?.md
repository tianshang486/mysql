# How do I change an SSD to a local SSD? {#concept_zz4_1ks_zgb .concept}

This topic describes how to change an SSD to a local SSD for an RDS instance. You can use the same method to change a local SSD to an SSD.

To change the storage class \(local SSD, SSD, or ESSD\) of an RDS instance, you must use DTS to migrate data from the source RDS instance to another new RDS instance.

## Prerequisites {#section_t4s_qqr_zgb .section}

-   The DB engine is one of the following:
    -   RDS for MySQL
    -   RDS for SQL Server
    -   RDS for PostgreSQL
-   You have created an RDS instance with the storage class you want. For more information, see [Create an RDS for MySQL instance](../../../../intl.en-US/Quick Start for MySQL/Create an RDS for MySQL instance.md#).
-   The storage capacity of the destination RDS instance cannot be lower than that of the source RDS instance.
-   The destination RDS instance is located in the same region as the source RDS instance.
-   The DB engine, version, and edition of the destination RDS instance are the same as those of the source RDS instance.
-   If you select the incremental data migration type, the binlog\_row\_image parameter is set to full for the source RDS instance.

## Precautions {#section_fn3_nsv_ydb .section}

-   The instance information changes after the migration, therefore you must modify the instance information on your application properly to guarantee service continuity.
-   Do not perform DDL operations during the migration.
-   Event migration is not supported in schema migration.
-   If the object name mapping function is used for an object, the migration of objects relying on the object may fail.

## Procedure {#section_lwy_4sv_ydb .section}

1.  Log on to the [DTS console](http://dts.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**. Then in the upper-right corner, click **Create Migration Task**.

    ![创建迁移任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040136_en-US.png)

3.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Task Name**|By default, DTS automatically generates a name for each task. You can change the name to indicate the specific services for easy identification of the task.|
    |**Source Database**|**Instance Type**|Select **RDS Instance**.|
    |**Instance Region**|Select the region where the source RDS instance is located.|
    |**RDS Instance ID**|Select the ID of the source RDS instance.|
    |**Database Account**|Enter the username of the database account you use to connect the source RDS instance. For example, the account can be a premier account, or a standard account that has the read and write permissions for all databases.|
    |**Database Password**|Enter the password of the database account you use to connect the source RDS instance.|
    |**Encryption**|In typical cases, select **Non-encrypted**. If the source RDS instance supports [Configure SSL encryption](../../../../intl.en-US/User Guide/Security/Configure SSL encryption.md#) and has SSL encryption enabled, select **SSL-encrypted**.|
    |**Destination Database**|**Device Spec**|Select **RDS Instance**.|
    |**Instance Region**|Select the region where the source RDS instance is located.|
    |**RDS Instance ID**|Select the ID of the destination RDS instance.|
    |**Database Account**|Enter the username of the database account you use to connect the destination RDS instance. For example, the account can be a premier account, or a standard account that has the read and write permissions for all databases.|
    |**Database Password**|Enter the password of the database account you use to connect the source RDS instance.|
    |**Encryption**|In typical cases, select **Non-encrypted**. If the source RDS instance supports [Configure SSL encryption](../../../../intl.en-US/User Guide/Security/Configure SSL encryption.md#) and has SSL encryption enabled, select **SSL-encrypted**.|

    **Note:** The values of the **Instance Type** and **RDS Instance ID** parameters determine which of the other parameters are displayed.

    ![迁移任务设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040108_en-US.png)

4.  Click **Test Connectivity** in the **Source Database** and **Destination Database** sections separately.

    **Note:** If a message is displayed to the right of **Test Connectivity**, the RDS instance can be connected. Otherwise, rectify faults based on the error message.

5.  In the lower-right corner, click **Set Whitelist and Next**.
6.  Select a migration type. In the **Available** section, select the objects you want to migrate, and click **\>** to add them to the **Selected** section. Then, click **Precheck**.

    ![迁移类型及列表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040110_en-US.png)

    **Note:** If you want to change the name of an object to be migrated, then find the object in the Selected section and click **Edit** to the right of the object.

    ![修改数据库名称](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040111_en-US.png)

7.  Optional. If the migration task fails the precheck, perform this step. If the migration task passes the precheck, go to Step 10.

    The system displays the precheck results, as shown in the following figure.

    ![预检查失败](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040132_en-US.png)

8.  Find each check item whose Check Result**Check Result** is **Failed** and click ![失败详情](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040130_en-US.png) to view the failure details. Then locate the fault based on the failure details.
9.  After all failures are located, navigate to the page that displays the migration task list, and start the migration task you have created.

    ![重启任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680040134_en-US.png)

10. When the migration task passes the precheck, click **Next**.

    ![预检查通过](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680140131_en-US.png)

11. Confirm the settings, select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, and click **Buy and Start**.

## What to do next {#section_vn3_5ss_zgb .section}

Wait until the migration is complete. After the migration is complete, you must modify the instance information on your application and use the endpoint of the new RDS instance to establish a connection.

![迁移完成](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/135620/156895680140140_en-US.png)


# Configure TDE for an ApsaraDB RDS for SQL Server instance

This topic describes how to configure Transparent Data Encryption \(TDE\) for your ApsaraDB RDS for SQL Server instance. TDE allows your RDS instance to encrypt the data that will be written into the disk and decrypt the data that will be read from the disk to the memory. TDE does not increase the sizes of data files. You can use TDE without the need to modify your application.

-   Your RDS instance is a primary instance that runs an Enterprise Edition of SQL Server. TDE is not supported for read-only instances.
-   You have logged on to the ApsaraDB for RDS console by using your Alibaba Cloud account.
-   Alibaba Cloud Key Management Service \(KMS\) is activated. If KMS is not activated, you can activate it as prompted when you enable TDE.

For data security purposes, we recommend that you enable TDE by using the ApsaraDB for RDS console or an API operation.

## Precautions

-   Instance-level TDE can be enabled but cannot be disabled. Database-level TDE can be enabled or disabled.
-   The key used for TDE is created and managed by KMS. ApsaraDB for RDS does not provide the key or certificate that is required for encryption. After TDE is enabled, you must decrypt data on your RDS instance if you want to restore the data to your computer. For more information, see the "[What to do next](#section_e12_sw4_ydb)" section in this topic.
-   After TDE is enabled, the CPU utilization of your RDS instance significantly increases.

## Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  On the **TDE** tab, turn on the switch next to **TDE Status**.

    **Note:** You can enable TDE only when the RDS instance meets all of the requirements that are specified in the "Prerequisites" section in this topic.

    ![Enable TDE](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2259259951/p103138.png)

6.  In the Database TDE Settings dialog box, select the databases that you want to encrypt from the Unselected Databases section, click the ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7816559951/p42083.png) icon to move the selected databases to the **Selected Databases** section, and click **OK**.

    ![Configure TDE](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2259259951/p42082.png)


## What to do next

If you no longer want to use TDE to protect a database, you can remove the database from the Selected Databases section in the **Database TDE Settings** dialog box.


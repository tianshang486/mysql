# Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance

This topic describes how to modify the permissions of a standard account that is created on an ApsaraDB RDS for MySQL instance. The permissions of a privileged account can only be reset to the default settings.

**Note:** You can use the Account Authorization and Management feature of Alibaba Cloud Data Management \(DMS\) to define permission combinations. You can also use this feature to manage the permissions on specific tables. For more information, see [Manage user permissions on MySQL databases]().

## Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Accounts**.

5.  Find the standard account whose permissions you want to modify, and click the **Edit Permissions** icon in the Actions column.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7250359951/p4167.png)

6.  In the **Modify Account Permissions** pane, modify the permissions of the standard account.

    -   If you want to add or remove an authorized database, select the database and click the **\>** or **<** icon.
    -   If you want to modify the permissions on an authorized database, select the database and then select the **Read/Write \(DDL + DML\)**, **Read-only**, **DDL Only**, or **DML Only** permissions in the **Authorized Databases** section.

        **Note:** You can use SQL statements to modify permissions at higher levels of granularity. For more information, see [Account permissions](/intl.en-US/RDS MySQL Database/Account/Account permission/Account permissions.md).

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7250359951/p4168.png)

7.  Click **OK**.



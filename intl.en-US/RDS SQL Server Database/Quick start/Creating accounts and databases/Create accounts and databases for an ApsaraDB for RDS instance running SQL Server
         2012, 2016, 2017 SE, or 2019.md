# Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2012, 2016, 2017 SE, or 2019

This topic describes how to create accounts and databases for an ApsaraDB for RDS instance that runs SQL Server 2012, 2014, 2016, 2017 SE, or 2019. You can create the databases and accounts by using the ApsaraDB for RDS console.

The RDS instance runs one of the following SQL Server versions:

-   SQL Server 2012
-   SQL Server 2016
-   SQL Server 2017 SE
-   SQL Server 2019

**Note:** For more information about how to create accounts and databases for RDS instances that run other SQL Server versions, see the following topics:

-   [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2017 EE](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2017 EE.md)
-   [Create accounts and databases for an ApsaraDB for RDS instance running SQL Server 2008 R2](/intl.en-US/RDS SQL Server Database/Quick start/Creating accounts and databases/Create accounts and databases for an ApsaraDB for RDS instance running SQL Server
         2008 R2.md)

## Creates an account

You can create both privileged and standard accounts by using the ApsaraDB for RDS console. However, note that you can create a privileged account only by using the ApsaraDB for RDS console.

Precautions

-   Databases on the same RDS instance share all of the resources that belong to the RDS instance. You can manage standard accounts and databases by using SQL statements.
-   You must follow the minimal privilege principle to create accounts and grant read-only or read/write permissions to the accounts based on the required roles. If necessary, you can create more than one account and grant each account only the permissions to access the data within its authorized workloads. If an account does not need to write data to a database, you must grant only the read-only permissions on the database to the account.
-   For security purposes, we recommend that you configure strong passwords for the created accounts and change the passwords on a regular basis.

Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Accounts**.

5.  Click **Create Account**.

    ![Create Account](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3250359951/p42073.png)

6.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account:**|Enter the username of the account. The username must be 2 to 16 characters in length. It can contain lowercase letters, digits, and underscores \(\_\). It must start with a lowercase letter and end with a lowercase letter or digit.|
    |**Account Type:**|    -   **Privileged Account**: You can select the **Privileged Account** option only when the account is the first account that you create for the RDS instance. This is because the first account that you create must be a privileged account. Each RDS instance can have only one privileged account. The privileged account of an RDS instance cannot be deleted.
    -   **Standard Account**: You can select the **Standard Account** option only after you have created a privileged account for the RDS instance. Each RDS instance can have more than one standard account. You must manually grant the permissions on specific databases to each standard account. |
    |**Authorized Databases:**|Select the authorized databases of the account. You must select authorized databases only when you select the **Standard Account** type. If no databases are created, you can leave this parameter empty. You can perform the following steps to grant the permissions on more than one database to the account:

    1.  In the **Unauthorized Databases** section, select the required databases.
    2.  Click the **\>** icon to move the selected databases to the **Authorized Databases:** section.
    3.  In the Authorized Databases section, specify the permissions that the account will be granted on each authorized database. The supported permissions are **Read/Write \(DML\)**, **Read-only**, and **Owner**.

**Note:**

        -   The account is authorized to create tables, delete tables, and modify schemas in a database only when it has the **Owner** permissions on the database.
        -   If you select the **Privileged Account** type, the account has the permissions on all of the databases created on the RDS instance and does not require authorization.
![Authorized Databases](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0449259951/p69595.png) |
    |**Password:**|Enter the password of the account. The password must meet the following requirements:

    -   The password must be 8 to 32 characters in length.
    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include ! @ \# $ % ^ & \* \( \) \_ + - = |
    |**Confirm Password:**|Enter the password of the account again.|
    |**Description:**|Enter a description that helps identify the account. The description can be up to 256 characters in length.|

7.  Click **OK**.


## Create a database

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Databases**.

5.  Click **Create Database**.

6.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Name:**|Enter the name of the database. The name must be 2 to 64 characters in length. It can contain lowercase letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a lowercase letter and end with a lowercase letter or digit.|
    |**Supported Character Sets:**|Select the character set that is supported by the database.|
    |**Authorized Account:**|Select the account to which you want to grant the permissions on the database. Then, you must set the Account Type parameter to **Read/Write**, **Read-only**, or **Owner**. If no accounts are created, you can leave this parameter empty.

**Note:** The account is authorized to create tables, delete tables, and modify schemas in a database only when it has the **Owner** permissions on the database. |
    |**Description:**|Enter a description that helps identify the database. The description can be up to 256 characters in length.|

7.  Click **Create**.


## Related operations

|Operation|Description|
|---------|-----------|
|[Create database account](/intl.en-US/API Reference/Account management/Create database account.md)|Creates an account for an ApsaraDB for RDS instance.|
|[Create database](/intl.en-US/API Reference/Database management/Create database.md)|Creates a database for an ApsaraDB for RDS instance.|


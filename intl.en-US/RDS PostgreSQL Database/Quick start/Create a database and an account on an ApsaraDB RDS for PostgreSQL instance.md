# Create a database and an account on an ApsaraDB RDS for PostgreSQL instance

Before you start to use ApsaraDB RDS, you must create databases and accounts on an ApsaraDB RDS instance. This topic describes how to create a database and an account on an ApsaraDB RDS for PostgreSQL instance.

## Account types

ApsaraDB RDS for PostgreSQL instances support two types of accounts: privileged accounts and standard accounts. The following table describes these account types.

|Account type|Description|
|------------|-----------|
|**Privileged account**|-   You can create and manage privileged accounts by using the ApsaraDB RDS console or the API.
-   If your RDS instance uses local SSDs, you can create only one privileged account. If your RDS instance uses standard or enhanced SSDs, you can create more than one privileged account. A privileged account allows you to manage all of the standard accounts and databases that are created on your RDS instance.
-   A privileged account has more permissions that allow you to manage your RDS instance at more fine-grained levels. For example, you can grant the query permissions on different tables to different users.
-   A privileged account has the permissions to disconnect any accounts that are created on your RDS instance. |
|**Standard account**|-   You can create and manage standard accounts by using the ApsaraDB RDS console, API, or SQL statements.
-   You can create more than one standard account on your RDS instance.
-   You must grant the permissions on specific databases to a standard account.
-   A standard account does not have the permissions to create, manage, or disconnect other accounts on your RDS instance. |

## Precautions

-   If your RDS instance uses local SSDs, you can create one privileged account in the ApsaraDB RDS console. After the privileged account is created, it cannot be deleted. You can also create and manage more than one standard account by using SQL statements.
-   If your RDS instance uses standard or enhanced SSDs, you can create more than one privileged account and standard account in the ApsaraDB RDS console. You can also create and manage more than one standard account by using SQL statements.
-   To migrate data from an on-premises database to your RDS instance, you must create a database and an account on the RDS instance. Make sure that the created database has the same properties as the on-premises database. Also make sure that the created account has the same permissions on the created database as the account that is authorized to manage the on-premises database.
-   Follow the least privilege principle to create accounts and grant them appropriate read-only and read/write permissions on databases. If necessary, you can create more than one account and grant them only the permissions on specific databases. If an account does not need to write data to a database, grant only the read-only permissions on that database to the account.
-   For security purposes, we recommend that you specify strong passwords for the accounts on your RDS instance and change the passwords on a regular basis.

## Create an account on an RDS instance that uses standard or enhanced SSDs

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
    |**Database Account:**|    -   The username of the account must be 2 to 16 characters in length.
    -   The username of the account can contain lowercase letters, digits, and underscores \(\_\).
    -   The username of the account must start with a lowercase letter and end with a lowercase letter or digit.
    -   The username of the account cannot be the same as the username of an existing account. |
    |**Account Type:**|Specify the type of the account. Two types of accounts are supported: privileged accounts and standard accounts.     -   A privileged account has all operation permissions on all databases.
    -   A standard account has all operation permissions only on its authorized databases.
**Note:** The operation permissions include SELECT, INSERT, UPDATE, DELETE, TRUNCATE, REFERENCES, and TRIGGER. |
    |**Password:**|    -   The password of the account must be 8 to 32 characters in length.
    -   The password of the account must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include ! @ \# $ % ^ & \* \( \) \_ + - = |
    |**Confirm Password:**|Enter the password of the account again.|
    |**Description:**|Enter the description of the account.|

7.  Click **OK**.


## Create a database on an RDS instance that uses standard or enhanced SSDs

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Databases**.

5.  Click **Create Database**.

6.  Configure the following parameters.

    ![Create a database for an RDS instance with standard or enhanced SSDs](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9250359951/p99288.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database Name:**|    -   The name of the database can contain up to 64 characters.
    -   The name of the database can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\).
    -   The name of the database must start with a lowercase letter and end with a lowercase letter or digit. |
    |**Supported Character Sets:**|The character set that is supported by the database.|
    |**Collate**|The rule that is used to sort strings.|
    |**Ctype**|The type of character that is supported by the database.|
    |**Authorized Account:**|The owner of the database. The owner has all permissions on the database.|
    |**Description:**|The description of the database.|

7.  Click **Create**.


## Create an account on an RDS instance that uses local SSDs

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Accounts**.

5.  Click **Create Privileged Account**.

6.  Configure the following parameters.

    ![Create an account on an RDS instance that uses local SSDs](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3250359951/p99778.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database Account:**|    -   The username of the account must be 2 to 16 characters in length.
    -   The username of the account can contain lowercase letters, digits, and underscores \(\_\).
    -   The username of the account must start with a lowercase letter and end with a lowercase letter or digit.
    -   The username of the account cannot be the same as the username of an existing account. |
    |**Password:**|    -   The password of the account must be 8 to 32 characters in length.
    -   The password of the account must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include ! @ \# $ % ^ & \* \( \) \_ + - = |
    |**Confirm Password:**|Enter the password of the account again.|

7.  Click **Create**.

    **Note:** After you complete the preceding steps, a privileged account is created. For more information about how to create a standard account, see the following steps.

8.  In the upper-right corner of the page, click **Log On to DB** to go to the RDS Database Logon page.

9.  Configure the following parameters.

    ![Log on to DMS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3250359951/p2961.png)

    |Parameter|Description|
    |---------|-----------|
    |**Network address:Port**|Enter the endpoint and port number that are used to connect to the RDS instance. For more information, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Database connections/View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for PostgreSQL instance.md).|
    |**Databases Username**|Enter the username of the account that is authorized to log on to the RDS instance.|
    |**Password**|The password of the preceding account.|

10. Click **Log On**.

    **Note:** If the system prompts you to add the Classless Inter-Domain Routing \(CIDR\) block of the Alibaba Cloud Data Management \(DMS\) server to an IP address whitelist of the RDS instance, click **Configure Whitelist**.

11. After you log on to the RDS instance, choose **SQL Operations** \> **SQL Window** in the top navigation bar.

12. In the SQL window, execute the following statement to create a standard account:

    ```
    CREATE USER name [ [ WITH ] option [ ... ] ]
    where option can be:
       SUPERUSER | NOSUPERUSER
     | CREATEDB | NOCREATEDB
     | CREATEROLE | NOCREATEROLE
     | CREATEUSER | NOCREATEUSER
     | INHERIT | NOINHERIT
     | LOGIN | NOLOGIN
     | REPLICATION | NOREPLICATION
     | CONNECTION LIMIT connlimit
     | [ ENCRYPTED | UNENCRYPTED ] PASSWORD 'password'
     | VALID UNTIL 'timestamp'
     | IN ROLE role_name [, ...]
     | IN GROUP role_name [, ...]
     | ROLE role_name [, ...]
     | ADMIN role_name [, ...]
     | USER role_name [, ...]
     | SYSID uid
    ```

    For example, if you want to create an account named test2 with the password 123456, execute the following statement:

    ```
    create user test2 password '123456';
    ```


## Create a database on an RDS instance that uses local SSDs

1.  Log on to the [ApsaraDB RDS console](/intl.en-US/RDS PostgreSQL Database/Quick start/Connect to an ApsaraDB RDS for PostgreSQL instance.md).

2.  In the SQL window, execute the following statement to create a database:

    ```
    CREATE DATABASE name
     [ [ WITH ] [ OWNER [=] user_name ]
            [ TEMPLATE [=] template ]
            [ ENCODING [=] encoding ]
            [ LC_COLLATE [=] lc_collate ]
            [ LC_CTYPE [=] lc_ctype ]
            [ TABLESPACE [=] tablespace_name ]
            [ CONNECTION LIMIT [=] connlimit ] ]
    ```

    For example, if you want to create a database named test, execute the following statement:

    ```
    create database test;
    ```


## FAQ

After I create accounts on my primary RDS instance, can I manage the accounts on the read-only RDS instances?

No, although the accounts that are created on your primary RDS instance are synchronized to the read-only RDS instances, you cannot manage the accounts on the read-only RDS instances. The accounts only have read permissions on the read-only RDS instances.

## Operations

|Operation|Description|
|---------|-----------|
|[Create account](/intl.en-US/API Reference/Account management/Create account.md)|Creates an account for an ApsaraDB RDS instance.|


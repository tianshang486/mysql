# Create an account on an ApsaraDB RDS for PostgreSQL instance

This topic describes how to create an account on an ApsaraDB RDS for PostgreSQL instance.

## Account types

ApsaraDB RDS for PostgreSQL instances support two types of database accounts: privileged accounts and standard accounts. The following table describes these account types.

|Account type|Description|
|------------|-----------|
|**Privileged account**|-   You can create and manage privileged accounts by using the ApsaraDB for RDS console or API operations.
-   For an ApsaraDB RDS for PostgreSQL instance with local SSDs, you can create only one privileged account. For an ApsaraDB RDS for PostgreSQL instance with cloud disks, you can create multiple privileged accounts. A privileged account allows you to manage all standard accounts and databases in an ApsaraDB RDS for PostgreSQL instance.
-   A privileged account has more permissions, which allows you to perform more fine-grained management operations. For example, you can grant query permissions on different tables to different users.
-   You can use a privileged account to disconnect any accounts from their authorized databases in your ApsaraDB RDS for PostgreSQL instance. |
|**Standard account**|-   You can create and manage standard accounts by using the ApsaraDB for RDS console, API operations, or SQL statements.
-   You can create multiple standard accounts for an ApsaraDB RDS for PostgreSQL instance.
-   You must grant permissions on specific databases to a standard account.
-   You cannot use a standard account to create or manage other accounts, nor disconnect other accounts from databases. |

## Precautions

-   Databases within the same instance share all of the resources that belong to the instance. You can create databases, privileged accounts, and standard accounts for an ApsaraDB RDS for PostgreSQL instance. You can create as many databases as you want. You can also manage standard accounts and databases by using SQL statements.
-   To migrate data from an on-premises database to an ApsaraDB for RDS instance, you must create a database and an account in the RDS instance. Ensure that the database has the same properties as the on-premises database, and the account of the database has the same permissions as the account of the on-premises database.
-   Use service roles to create accounts and follow the principle of least privilege to assign appropriate read-only and read/write permissions to the accounts. When necessary, you can create multiple database accounts and allow each of them to access only data relevant to their own business tasks. If an account does not need to write data to a database, assign the read-only permissions to the account.
-   To ensure database security, set strong account passwords and change the passwords on a regular basis.

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


## Related operations

|Operation|Description|
|---------|-----------|
|[CreateAccount](/intl.en-US/API Reference/Account management/Create account.md)|Creates an account on an ApsaraDB for RDS instance.|


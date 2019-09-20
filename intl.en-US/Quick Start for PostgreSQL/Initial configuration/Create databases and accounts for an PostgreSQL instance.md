# Create databases and accounts for an PostgreSQL instance {#concept_njz_1gg_wdb .concept}

This topic describes how to create accounts and databases for an RDS for PostgreSQL instance.

Before an RDS instance can be used, you must create databases and accounts for it.

-   For PostgreSQL 11 High-availability Edition \(with SSDs\) and PostgreSQL 10 High-availability Edition \(with SSDs\), you can create and manage databases and accounts in the RDS console.
-   For PostgreSQL 10 High-availability Edition \(with local SSDs\), PostgreSQL 10 Basic Edition, and PostgreSQL 9.4, you must create a premier account in the RDS console, and then create and manage databases by using the DMS console or a database client.

## Account types {#section_f7r_5ba_s48 .section}

RDS for PostgreSQL support two types of accounts: premier accounts and standard accounts.

|Account type|Description|
|------------|-----------|
|**Premier accounts**| -   You can create and manage premier accounts only in the console or through APIs.
-   In PostgreSQL 10 High-availability Edition \(with local SSDs\), PostgreSQL 10 Basic Edition, and PostgreSQL 9.4, you can create only one premier account for an RDS instance, and this premier account has the permissions to manage all standard accounts and databases in the RDS instance.
-   In PostgreSQL 11 High-availability Edition \(with SSDs\) and PostgreSQL 10 High-availability Edition \(with SSDs\), you can create one or more premier accounts for an RDS instance, and these premier account each have the permissions to manage all standard accounts and databases in the RDS instance.
-   More permissions are provided for premier accounts to manage permissions at finer levels based on individual needs. For example, you can grant the query permissions for tables by user.
-   A premier account has the permissions to disconnect the other accounts from the corresponding RDS instance.

 |
|**Standard accounts**| -   You can create and manage standard accounts in the console, through APIs, or by running SQL statements.
-   You can create one or more standard accounts for an RDS instance.
-   You must manually grant the permissions for databases to standard accounts.
-   A standard account does not have the permissions to create, manage, or disconnect the other accounts from the corresponding RDS instance.

 |

## Precautions {#section_kcx_dgg_wdb .section}

-   Databases under a single instance share all the resources of this instance. Each RDS for PostgreSQL instance supports one premier account, countless standard accounts, and countless databases. You must create and manage standard accounts and databases through SQL statements.
-   To migrate your on-premises database to an RDS instance, you must create the same databases and accounts for the RDS instance as your on-premises database.
-   When assigning account permissions for each database, follow the minimum permission' principle and consider service roles to create accounts. Alternatively, rationally assign read-only and read/write permissions. When necessary, you can split accounts and databases into smaller units so that each account can only access data for its own services. If the account does not need to write data to a database, assign the read-only permission for the account.
-   For database security, set strong passwords for the accounts and change the passwords regularly.

## PostgreSQL 11 High-availability Edition \(with SSDs\) or PostgreSQL 10 High-availability Edition \(with SSDs\) {#section_r7y_htg_djm .section}

1.  Log on to the [PostgreSQL console](https://postgresql.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156894420949667_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.
6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Account Name**|The name of the account.     -   The account name can contain up to 16 characters in length.
    -   The account name can contain lowercase letters, digits, and underscores \(\_\).
    -   The account name must start with a lowercase letter and end with a lowercase letter or digit.
 |
    |**Account Type**|Select **Premier Account** or **Standard Account**.|
    |**Password**|The password of the account.     -   The account password must contain 8 to 32 characters in length.
    -   The account password must contain at least three of the following types of characters: uppercase letters , lowercase letters, digits, and special characters.
    -   The allowed special characters are as follows:

! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Confirm Password**|Re-enter the password to confirm it.|

    ![创建账号](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/156894420949676_en-US.png)

7.  Click **OK**.
8.  In the left-side navigation pane, click **Databases**.
9.  Click **Create Database**.
10. Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Name**|The name of the database.     -   The database name can contain up to 64 characters in length.
    -   The database name contain lowercase letters, digits, and underscores \(\_\).
    -   The database name must start with a lowercase letter and end with a lowercase letter or digit.
 |
    |**Supported Character Set**|Select the character set supported by the database.|
    |**Collate**|The rule for sorting strings.|
    |**Ctype**|The type of character.|
    |**Database Owner**|The owner of the database. This owner has all permissions for the database.|

    ![创建数据库](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/156894420949678_en-US.png)

11. Click **OK**.

## PostgreSQL 10 High-availability Edition \(local SSDs\), PostgreSQL 10 Basic Edition, or PostgreSQL 9.4 {#section_ixc_fgg_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156894420949667_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.
6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|The name of the account.     -   The account name can contain 2 to 16 characters.
    -   The account name can contain lowercase letters, digits, and underscores \(\_\).
    -   The account name must start with a lowercase letter and end with a lowercase letter or digit.
 |
    |**Password**|The password of the account.     -   The account password must contain 8 to 32 characters in length.
    -   The account password must contain at least three of the following types of characters: uppercase letters , lowercase letters, digits, and special characters.
    -   The allowed special characters are as follows:

! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Re-enter Password**|Re-enter the password to confirm it.|

    ![创建账号页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/156894420939893_en-US.png)

7.  Click **OK**.
8.  In the upper-right corner, click **Log On to DB**.

    You are directed to the RDS Database Logon page in the [Data Management Service console](https://dms-intl.console.aliyun.com/?token=351395c5-8363-4bf6-9b19-7ac06b25ab6a#/dms/login).

9.  Examine the connection address and port information. If the information is correct, enter the username and password, as shown in the following figure.

    ![登录RDS数据库快捷页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7850/15689442092961_en-US.png)

    |No.|Description|
    |---|-----------|
    |**1**|The connection address and port information for the RDS instance.|
    |**2**|The name of the account to access the database.|
    |**3**|The password of the account to access the database|

10. Click **Log On**.

    **Note:** If you want the browser to remember the password for this account, you can select **Remember Password** before you click **Log On**.

11. Optional. If the system prompts you to add the CIDR block where the DMS server is located to the whitelist of the RDS instance, see [Configure a whitelist](../../../../intl.en-US/User Guide/Security/Configure a whitelist.md#).
12. Optional. After the whitelist is properly configured, click **Log On**.
13. After you log on to the RDS instance, choose **SQL Operations** \> **SQL Window** from the main menu.
14. In the SQL window, enter the following command to create a database:

    ``` {#codeblock_1hv_tag_joe}
    CREATE DATABASE name
     [ [ WITH ] [ OWNER [=] user_name ]
            [ TEMPLATE [=] template ]
            [ ENCODING [=] encoding ]
            [ LC_COLLATE [=] lc_collate ]
            [ LC_CTYPE [=] lc_ctype ]
            [ TABLESPACE [=] tablespace_name ]
            [ CONNECTION LIMIT [=] connlimit ] ]
    ```

    For example, if you want to create a database named **test**, then run the following command:

    ``` {#codeblock_e25_t7q_y0q}
    Create database test;
    ```

15. Click **execute** to create the database.
16. In the SQL window, enter the following command to create a standard account:

    ``` {#codeblock_w4o_2oj_wa5}
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

    For example, if you want to create a standard account named **test2** with a password of **123456**, then run the following command:

    ``` {#codeblock_fzv_43b_agm}
    create user test2 password '123456';
    ```

17. Click **execute** to create the standard account.

## FAQ {#section_znt_2jv_fhb .section}

Can I use the accounts created in a master RDS instance to access the read-only instances attached to this master RDS instance?

Yes. The accounts created in a master RDS instance are synchronized to the read-only instances attached to this master RDS instance. However, you cannot manage these accounts in the read-only instances. Additionally, these accounts only have the permissions to read data in the read-only instances.

## APIs {#section_xpk_gdb_kgb .section}

|API|Description|
|---|-----------|
|[CreateAccount](../../../../intl.en-US/API Reference/Account management/CreateAccount.md#)|Used to create an account.|


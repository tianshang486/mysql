# Create accounts and databases {#concept_jyq_tc5_q2b .concept}

This article describes how to create accounts and databases for an RDS for MySQL instance.

## Account types {#section_b3f_whz_q2b .section}

RDS for MySQL supports two types of database accounts: superuser accounts and standard accounts. You can manage all your accounts and databases on the console. For specific privileges, see [Account privileges](#).

|Account Type|Description|
|------------|-----------|
|**Superuser account**| -   Can only be created and managed through the console or API.
-   Each instance can have only one superuser account, which can be used to manage all databases and standard accounts.
-   Has more privileges than standard accounts and can manage privileges at a more fine-grained level. For example, it can assign table-level query privileges to other accounts.
-   Can disconnect the connections established by any other accounts.

 |
|**Standard account**| -   Can be created and managed through the console, API, or SQL statements.
-   Each instance can have up to 200 standard accounts.
-   Need to be manually granted with database privileges.
-   Cannot create or manage other accounts, or disconnect the connections established by other accounts.

 |

## Differences between the superuser account privileges and SUPER privilege {#section_obs_tlg_1gb .section}

**Superuser account privileges**

-   Can manage all databases and standard accounts. [Account privileges](#) lists the privileges of the superuser account.
-   The superuser account can disconnect the connections established by other accounts.
-   Running the `show processlist` command shows processes of the current account, excluding processes on the control level.

**SUPER privilege**

To prevent potential incorrect operations, RDS for MySQL does not provide the SUPER privilege.

-   Can kill any connections.
-   Running the `show processlist` command shows all processes, including processes on the control level.
-   Can use the SET statement to modify any global variables.
-   Can use the CHANGE MASTER and PURGE MASTER LOGS commands.
-   Can perform operations on files stored on the host.

## Create the superuser account {#section_wkq_j35_q2b .section}

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.
3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation pane, choose **Accounts**.
5.  Click **Create Account**.
6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**| Fill in the account name. Requirements are as follows:

     -   Consists of 2 to 16 characters.
    -   Starts with a letter and ends with a letter or digit.
    -   Consists of lower-case letters, digits, or underscores.
 |
    |**Account Type**|Select **Superuser Account**.|
    |**Password**| Set the account password. Requirements are as follows:

     -   Consists of 8 to 32 characters.
    -   Contains at least three of the following types: upper-case letters, lower-case letters, digits, and special characters !@\#$%^&\*\(\)\_+-=
 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Enter relevant information, with up to 256 characters.|

7.  Click **OK**.

## Reset privileges of the superuser account {#section_tnt_dth_w2b .section}

If the superuser account is abnormal \(for example, privileges are unexpectedly revoked\), you can reset the privileges.

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.
3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Reset Account Permissions** for the superuser account.
6.  Enter the superuser account password to reset the account privileges.

## Create a standard account {#section_nym_xr5_q2b .section}

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.
3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation bar, click **Accounts**.
5.  Click **Create Account**.
6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**| Fill in the account name. Requirements are as follows:

     -   Consists of 2 to 16 characters.
    -   Starts with a letter and ends with a letter or digit.
    -   Consists of lower-case letters, digits, or underscores.
 |
    |**Account Type**|Select **Standard Account**.|
    |**Authorized Database**|Grant database privileges to this account. You can also leave this field blank and grant privileges to the account after the account is created.    1.  Select one or more databases from the left, and click **Authorize** to add to the right.
    2.  In the right-hand box, select **Read/Write**, **Read-only**, **DDL Only**, or **DML Only**.

If you want to set the privileges of multiple databases at the same time, click the button \(such as **Grant All Read/Write**\) in the upper-right corner of the right-hand box.

**Note:** The button in the upper-right corner changes as you click.

|
    |**Password**| Set the account password. Requirements are as follows:

     -   Consists of 8 to 32 characters.
    -   Contains at least three of the following types: upper-case letters, lower-case letters, digits, and special characters !@\#$%^&\*\(\)\_+-=
 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Enter relevant information, with up to 256 characters.|

7.  Click **OK**.

## Create a database {#section_efz_yt5_q2b .section}

Each instance can have up to 500 databases.

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.
3.  Locate the target instance and click the instance ID.
4.  In the left-side navigation pane, click **Databases**.
5.  Click **Create Database**.
6.  Set the following parameters.

    |Parameters|Description|
    |----------|-----------|
    |**Database Name**|     -   Consists of 2 to 64 characters.
    -   Starts with a letter and ends with a letter or a digit.
    -   Consists of lower-case letters, digits, underscores \(\_\), or hyphens \(-\).
    -   Must be unique in the instance.
 |
    |**Supported Character Set**|Select utf8, gbk, latin1, or utf8mb4.If you need other character sets, select **all** and then select from the list.

|
    |**Authorized Account**|Select the account that needs to access this database. You can also leave this field blank and set the authorized account after the database is created.**Note:** Only standard accounts are displayed, because the superuser account already has privileges for all databases.

|
    |**Account Type**|Select **Read/Write**, **Read-only**, **DDL only**, or **DML only**.This parameter is displayed only after you select an account to authorize.

|
    |**Remarks**|Enter relevant information, with up to 256 characters.|

7.  Click **OK**.

## Account privileges {#section_qgv_4q5_tfb .section}

|Account type|Privilege type|Privileges|
|------------|--------------|----------|
|**Superuser account**|-|SELECT|INSERT|UPDATE|DELETE|CREATE|
|DROP|RELOAD|PROCESS|REFERENCES|INDEX|
|ALTER|CREATE TEMPORARY TABLES|LOCK TABLES|EXECUTE|REPLICATION SLAVE|
|REPLICATION CLIENT|CREATE VIEW|SHOW VIEW|CREATE ROUTINE|ALTER ROUTINE|
|CREATE USER|EVENT|TRIGGER| | |
|**Standard account**|**Read-only**|SELECT|LOCK TABLES|SHOW VIEW|PROCESS|REPLICATION SLAVE|
|REPLICATION CLIENT| | | | |
|**Read/write**|SELECT|INSERT|UPDATE|DELETE|CREATE|
|DROP|REFERENCES|INDEX|ALTER|CREATE TEMPORARY TABLES|
|LOCK TABLES|EXECUTE|CREATE VIEW|SHOW VIEW|CREATE ROUTINE|
|ALTER ROUTINE|EVENT|TRIGGER|PROCESS|REPLICATION SLAVE|
|REPLICATION CLIENT| | | | |
|**DDL only**|CREATE|DROP|INDEX|ALTER|CREATE TEMPORARY TABLES|
|LOCK TABLES|CREATE VIEW|SHOW VIEW|CREATE ROUTINE|ALTER ROUTINE|
|PROCESS|REPLICATION SLAVE|REPLICATION CLIENT| | |
|**DML only**|SELECT|INSERT|UPDATE|DELETE|CREATE TEMPORARY TABLES|
|LOCK TABLES|EXECUTE|SHOW VIEW|EVENT|TRIGGER|
|PROCESS|REPLICATION SLAVE|REPLICATION CLIENT| | |


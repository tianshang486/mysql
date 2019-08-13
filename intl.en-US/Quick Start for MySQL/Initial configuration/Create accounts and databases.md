# Create accounts and databases {#concept_jyq_tc5_q2b .concept}

This topic describes how to create accounts and databases for an RDS for MySQL instance.

## Account types {#section_b3f_whz_q2b .section}

RDS for MySQL supports two types of database accounts: superuser accounts and standard accounts. You can manage all your accounts and databases on the console. For specific permissions, see [Account permissions](#section_qgv_4q5_tfb) .

|Account Type|Description|
|------------|-----------|
|**Superuser account**| -   Can only be created and managed through the console or API.
-   Each instance can have only one superuser account, which can be used to manage all databases and standard accounts.
-   Has more permissions than standard accounts and can manage permissions at a more fine-grained level. For example, it can assign table-level query permissions to other accounts.
-   Can disconnect the connections established by any other accounts.

 |
|**Standard account**| -   Can be created and managed through the console, API, or SQL statements.
-   Each instance can have up to 200 standard accounts.
-   Need to be manually granted with database permissions.
-   Cannot create or manage other accounts, or terminate the connections established by other accounts.

 |

|Account Type|Number of databases|Number of tables|Number of users|
|------------|-------------------|----------------|---------------|
|Superuser account|Unlimited|< 200,000|Varies depending on the instance kernel parameters.|
|Standard account|500|< 200,000|Varies depending on the instance kernel parameters.|

## Differences between the superuser account permissions and SUPER permissions {#section_obs_tlg_1gb .section}

**Superuser account permissions**

-   Can manage all databases and standard accounts. [Account permissions](#section_qgv_4q5_tfb) lists the permissions of the superuser account.
-   Can terminate the connections established by other accounts.
-   Running the `show processlist` command shows only the processes of the current account, excluding processes on the control level.

**SUPER permissions**

To prevent potential incorrect operations, RDS for MySQL does not provide the SUPER permissions.

-   Can terminate any connections.
-   Running the `show processlist` command shows all processes, including processes on the control level.
-   Can use the `SET` statement to modify any global variables.
-   Can use the CHANGE MASTER and PURGE MASTER LOGS commands.
-   Can perform operations on files stored on the host.

## Create the superuser account {#section_wkq_j35_q2b .section}

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567601136543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.

    ![创建截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17032/156567601142073_en-US.png)

6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|The account name contains 2 to 16 characters, including lowercase letters, digits, and underscores \(\_\). It must begin with a letter and end with a letter or digit.|
    |**Account Type**|Select **Superuser Account**.|
    |**Password**| The password contains 8 to 32 characters, including at least three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters. The allowed special characters are as follows:

 ! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Reset the permissions of the superuser account {#section_tnt_dth_w2b .section}

If the superuser account is abnormal \(for example, the account permissions are unexpectedly revoked\), you can reset the permissions.

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567601136543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Find the superuer account, and click **Reset Permissions** in the **Actions** column.

    ![回收权限](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17032/156567601242075_en-US.png)

6.  Enter the password of the superuser account and click **OK**.

## Create a standard account {#section_nym_xr5_q2b .section}

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567601136543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation bar, click **Accounts**.
5.  Click **Create Account**.

    ![创建截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17032/156567601142073_en-US.png)

6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|The account name contains 2 to 16 characters, including lowercase letters, digits, or underscores \(\_\). It must begin with a letter and end with a letter or digit.|
    |**Account Type**|Select **Standard Account**.|
    |**Authorized Databases**|Grant permissions on one or more databases to the account. This parameter is optional. You can choose to grant permissions to the account after the account is created.     1.  Select one or more databases from the left area and click **Authorize \>** to add them to the right area.
    2.  In the right area, click **Read/Write**, **Read-only**, **DDL Only**, or **DML Only**.

If you want to grant the permissions for multiple databases in batches, select all the databases and in the upper-right corner click the button such as **Full Control Read/Write**.

**Note:** The button in the upper-right corner changes as you click. For example, after you click **Full Control Read/Write**, the permission changes to **Full Control Read-only**.

 |
    |**Password**| The password must contain 8 to 32 characters, including at least three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters. The allowed special characters are as follows:

 ! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Create a database {#section_efz_yt5_q2b .section}

1.  Log on to the [RDS console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567601136543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Databases**.
5.  Click **Create Database**.

    ![创建数据库](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17032/156567601342076_en-US.png)

6.  Set the following parameters.

    |Parameters|Description|
    |----------|-----------|
    |**Database Name**|The account name contains 2 to 16 characters, including lowercase letters, digits, underscores \(\_\), and hyphens \(-\). It must begin with a letter and end with a letter or digit.|
    |**Supported Character Set**|Select **utf8**, **gbk**, **latin1**, or **utf8mb4**. If you need another character set, select **all** and then select the character set from the list.

 |
    |**Authorized Account**|Select the account that needs to access this database. You can also leave this parameter blank and set the authorized account after the database is created. **Note:** Only standard accounts are displayed, because the superuser account has all permissions for all databases.

 |
    |**Account Type**|Select **Read/Write**, **Read-only**, **DDL only**, or **DML only**.|
    |**Remarks**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Account permissions {#section_qgv_4q5_tfb .section}

|Account type|Permission type|Permission|
|------------|---------------|----------|
|**Superuser account**|N/A|SELECT|INSERT|UPDATE|DELETE|CREATE|
|DROP|RELOAD|PROCESS|REFERENCES|INDEX|
|ALTER|CREATE TEMPORARY TABLES|LOCK TABLES|EXECUTE|REPLICATION SLAVE|
|REPLICATION CLIENT|CREATE VIEW|SHOW VIEW|CREATE ROUTINE|ALTER ROUTINE|
|CREATE USER|EVENT|TRIGGER|N/A|N/A|
|**Standard account**|**Read-only**|SELECT|LOCK TABLES|SHOW VIEW|PROCESS|REPLICATION SLAVE|
|REPLICATION CLIENT|N/A|N/A|N/A|N/A|
|**Read/write**|SELECT|INSERT|UPDATE|DELETE|CREATE|
|DROP|REFERENCES|INDEX|ALTER|CREATE TEMPORARY TABLES|
|LOCK TABLES|EXECUTE|CREATE VIEW|SHOW VIEW|CREATE ROUTINE|
|ALTER ROUTINE|EVENT|TRIGGER|PROCESS|REPLICATION SLAVE|
|REPLICATION CLIENT|N/A|N/A|N/A|N/A|
|**DDL only**|CREATE|DROP|INDEX|ALTER|CREATE TEMPORARY TABLES|
|LOCK TABLES|CREATE VIEW|SHOW VIEW|CREATE ROUTINE|ALTER ROUTINE|
|PROCESS|REPLICATION SLAVE|REPLICATION CLIENT|N/A|N/A|
|**DML only**|SELECT|INSERT|UPDATE|DELETE|CREATE TEMPORARY TABLES|
|LOCK TABLES|EXECUTE|SHOW VIEW|EVENT|TRIGGER|
|PROCESS|REPLICATION SLAVE|REPLICATION CLIENT|N/A|N/A|

## FAQ {#section_zd7_bxo_wot .section}

Can I use an account that I create to operate read-only instance?

An account created in your master RDS instance will be synchronized to the read-only instances attached to the master instance. However, you cannot manage the account in the read-only instances. The account only has the read permissions for the read-only instances.

## APIs {#section_ajw_icw_ni0 .section}

|API|Description|
|---|-----------|
|[CreateAccount](../../../../intl.en-US/API Reference/Account management/CreateAccount.md#)|Used to create an account.|
|[CreateDatabase](../../../../intl.en-US/API Reference/Database management/CreateDatabase.md#)|Used to create a database.|


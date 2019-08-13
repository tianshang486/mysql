# Create accounts and databases {#concept_jyq_tc5_q2b .concept}

This topic describes how to create accounts and databases for RDS for MariaDB TX instances.

## Account types {#section_b3f_whz_q2b .section}

RDS for MariaDB instances support two types of database accounts: superuser accounts and standard accounts. You can manage all your accounts and databases in the RDS console.

|Account type|Description|
|------------|-----------|
|**Superuser account**| -   You can create and manage superuser accounts only in the RDS console or through APIs.
-   You can create only one superuser account for an instance. The superuser account can manage all standard accounts and databases under this instance.
-   Additional permissions are available for superuser accounts to meet the requirements for fine-grained, personalized management. For example, you can grant the permission of querying different tables to different users.
-   A superuser account has permissions on all databases under the instance.
-   A superuser account can disconnect any account from the instance.

 |
|**Standard account**| -   You can create and manage standard accounts in the RDS console, through APIs, or by using SQL statements.
-   You can create multiple standard accounts for an instance, depending on the number of instance cores.
-   You need to manually grant permissions on a specific database to a standard account.
-   A standard account cannot create or manage other accounts or disconnect other accounts from the instance.

 |

## Create a superuser account {#section_wkq_j35_q2b .section}

1.  Log on to the [RDS Console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567871936543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.

    ![创建账号](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21120/156567872042077_en-US.png)

6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**| The account name contains 2 to 16 characters, including lowercase letters, numbers, and underscores \(\_\). It must begin with a letter and ends with a letter or digit.

 **Note:** If the name of the superuser account to be created is the same as that of an existing standard account, the standard account will be replaced with the superuser account.

 |
    |**Account Type**|Select **Superuser Account**.|
    |**Password**| The password contains 8 to 32 characters, including at least three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters. The allowed special characters are as follows:

 ! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Reset the permissions of a superuser account {#section_tnt_dth_w2b .section}

If the superuser account is abnormal \(for example, the account permissions are unexpectedly revoked\), you can reset the permissions.

1.  Log on to the [RDS Console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567871936543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Find the supperuser account, and click **Reset Permissions** in the **Actions** column.

    ![重置权限](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21120/156567872042078_en-US.png)

6.  Enter the password of the superuser account and click **OK**.

## Create a standard account {#section_nym_xr5_q2b .section}

1.  Log on to the [RDS Console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567871936543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.

    ![创建账号](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21120/156567872042077_en-US.png)

6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|The account name contains 2 to 16 characters, including lowercase letters, digits, and underscores \(\_\). It must begin with a letter and end with a letter or digit.|
    |**Account Type**|Select **Standard Account**.|
    |**Authorized Databases**|Grant the permissions for one or more databases to the account. This parameter is optional. You can choose to grant permissions to the account after you create it. For more information, see [Create a database](../intl.en-US/User Guide/Database management/Create a database.md#).     1.  Select one or more databases from the left area and click **Add** to add them to the right area.
    2.  In the right area, click **Read/Write**, **Read-only**, **DDL Only**, or **DML Only**.

If you want to grant the permissions for multiple databases in batches, select all the databases and in the upper-right corner click the button such as **Full Control Read/Write**.

**Note:** The button in the upper-right corner changes as you click. For example, after you click **Full Control Read/Write**, the permission changes to **Full Control Read-only**.

 |
    |**Password**| The password contains 8 to 32 characters, including at least three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters. The allowed special characters are as follows:

 ! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Create a database {#section_efz_yt5_q2b .section}

1.  Log on to the [RDS Console](https://rdsnext.console.aliyun.com).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567871936543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Databases**.
5.  Click **Create Database**.

    ![创建数据库](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21120/156567872042079_en-US.png)

6.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Name**|The database name contains 2 to 64 characters including lowercase letters, digits, underscores \(\_\), and hyphens \(-\). It must begin with a letter and end with a letter or digit.|
    |**Supported Character Set**|Select **utf8**, **gbk**, **latin1**, or **utf8mb4**.|
    |**Authorized Account**|Select the account that needs to access this database. You can also leave this parameter blank and set the authorized account after the database is created. For more information, see [Change account permissions](../intl.en-US/User Guide/Account management/Change account permissions.md#). **Note:** Only standard accounts are displayed because the superuser account has all permissions for all databases.

 |
    |**Account Type**|Select **Read/Write**, **Read-only**, **DDL only**, or **DML only**.|
    |**Remarks**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## APIs {#section_2qu_yno_2ba .section}

|API|Description|
|---|-----------|
|[CreateAccount](../intl.en-US/API Reference/Account management/CreateAccount.md#)|Used to create an account.|
|[CreateDatabase](../intl.en-US/API Reference/Database management/CreateDatabase.md#)|Used to create a database.|


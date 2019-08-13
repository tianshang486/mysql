# Create databases and accounts for an RDS for SQL Server 2008 R2 instance {#concept_n3n_1zz_vdb .concept}

This topic is applicable only to RDS for SQL Server 2008 R2 instances. For more information on how to create databases and accounts for other versions, see [EN-US\_TP\_64588.md\#](intl.en-US/Quick Start for SQL Server/Initial configuration/Creating accounts and databases/Create databases and accounts for an RDS for SQL Server 2017 instance.md#) and [EN-US\_TP\_7839.md\#](intl.en-US/Quick Start for SQL Server/Initial configuration/Creating accounts and databases/Create databases and accounts for an RDS for SQL Server 2012 or 2016 instance.md#).

## Create an account {#section_fa3_23n_wto .section}

**Precautions**

-   You can create up to 500 accounts for each RDS for SQL Server 2008 R2 instance.
-   To migrate data from a local database to RDS, you need to create databases and accounts that are the same as those of the local database.
-   When assigning permissions to database accounts, follow the principle of least privilege and create accounts based on the roles required. Assign the appropriate level of permissions to the accounts. When necessary, you can create multiple database accounts and allow each of them to access data relevant to their own business tasks. If an account does not need to write data to a database, assign read-only permissions to the account.
-   For database security, set strong passwords for the accounts and change the passwords regularly.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567790536543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7838/15656779052761_en-US.png)

6.  Enter the account information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7838/15656779052762_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|The account name contains 2 to 16 characters, including lowercase letters, digits, and underscores \(\_\). It must begin with a letter and end with a letter or digit.|
    |**Authorized Databases**|Select the databases for which the account has permissions. If no databases have been created, you can leave this parameter blank. An account can be authorized with multiple databases. To authorize an account to databases, take these steps:

     1.  In the left area, select the target databases.
    2.  Click **Add** to add the selected databases to the right area.
    3.  Set the account's permission on each database, which can be **Read/Write** or **Read-only**. You can also click the button \(for example, **Full Control Read-only**\) in the upper-right corner to set the permissions for the databases in batches.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7838/15656779052763_en-US.png)

 |
    |**Password**| The password contains 8 to 32 characters, including at least three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters. The allowed special characters are as follows:

 ! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Re-enter Password**|Enter the password again.|
    |**Note**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Create a database {#section_c3t_mtx_bfb .section}

You can create up to 50 databases for an RDS for SQL Server 2008 R2 instance.

1.  Log in to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.
3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Databases**.
5.  Click **Create Database**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7838/15656779052764_en-US.png)

6.  Enter the database information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7838/15656779052765_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database Name**|The database name contains 2 to 64 characters, including lowercase letters, digits, underscores \(\_\), and hyphens \(-\). It must begin with a letter and end with a letter or digit.|
    |**Supported Character Set**|Select a character set. If the character set you need is not listed, click **All** and select it from the drop-down list.|
    |**Authorized Account**|Select the account to which you want to assign permissions. If no accounts have been created, you can leave this parameter blank.

 |
    |**Account Type**|This parameter is displayed after you select an authorized account. You can set this parameter to **Read/Write** or **Read-only**.|
    |**Remarks**|Optional. Enter the other account information that helps to better manage the account. You can enter up to 256 characters.|

7.  Click **OK**.

## Resources {#section_lz2_xbp_f2b .section}

 [../DNMYSQ1860058/EN-US\_TP\_7997.md\#](../intl.en-US/User Guide/Data migration/Migrate SQL Server to cloud/Migrate full backup data to RDS for SQL Server 2008 R2.md#)

## APIs {#section_9hh_po2_t6a .section}

|API|Description|
|---|-----------|
|[../DNMYSQ1851749/EN-US\_TP\_8118.md\#](../intl.en-US/API Reference/Account management/CreateAccount.md#)|Used to create an account.|
|[../DNMYSQ1851749/EN-US\_TP\_8112.md\#](../intl.en-US/API Reference/Database management/CreateDatabase.md#)|Used to create a database.|


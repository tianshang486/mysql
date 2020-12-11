# Create an account on an ApsaraDB RDS for MariaDB instance

This topic describes how to create an account that is used to manage the databases of an ApsaraDB RDS for MariaDB instance.

## Account types

ApsaraDB RDS for MariaDB supports two types of accounts: privileged accounts and standard accounts. You can manage all accounts and databases of your RDS instance in the ApsaraDB RDS console.

|Account type|Description|
|------------|-----------|
|**Privileged account**|-   You can create and manage privileged accounts by using the ApsaraDB RDS console or API operations.
-   Only one privileged account is allowed per RDS instance. A privileged account has the permissions to manage all databases and standard accounts of the RDS instance where the privileged account is created.
-   A privileged account allows you to manage permissions at fine-grained levels. For example, you can grant each standard account the permissions to query specific tables of the RDS instance where the privileged account is created.
-   A privileged account has all the permissions on the databases of the RDS instance where the privileged account is created.
-   A privileged account has permissions to disconnect all the standard accounts of the RDS instance where the privileged account is created. |
|**Standard account**|-   You can create and manage standard accounts by using the ApsaraDB RDS console, API operations, or SQL statements.
-   More than one standard account is allowed per RDS instance. The maximum number of standard accounts that are allowed varies based on the used database engine.
-   You must manually grant the permissions on specific databases to each standard account.
-   A standard account does not have the permissions to create, manage, or disconnect other accounts of the RDS instance where the standard account is created. |

## Create a privileged account

1.  Log on to the [ApsaraDB RDS console](https://rdsnext.console.aliyun.com).
2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.
6.  In the Create Account panel, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|Enter the username of the account. The username must meet the following requirements:

    -   The username must be 2 to 16 characters in length.
    -   The username must start with a letter and end with a letter or digit.
    -   The username can contain lowercase letters, digits, and underscores \(\_\).
    -   The username cannot be the same as that of an existing account.
**Note:** If the username of the privileged account is the same as that of an existing standard account, the privileged account replaces the standard account. |
    |**Account Type**|Specify the type of the account. For this example, select **Privileged Account**.|
    |**Password**|Enter the password of the account. The password must meet the following requirements:

    -   The password must be 8 to 32 characters in length.
    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include: ! @ \# $ % ^ & \* \( \) \_ + - = |
    |**Confirm Password**|Enter the password of the account again.|
    |**Description**|Enter a description that helps identify the account. The description can be up to 256 characters in length.|

7.  Click **OK**.

## Reset the permissions of a privileged account

If the permissions of a privileged account are accidentally revoked or encounter other exceptions, perform the following steps to reset the permissions:

1.  Log on to the [ApsaraDB RDS console](https://rdsnext.console.aliyun.com).
2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Find the privileged account and click **Reset Permissions** in the **Actions** column.
6.  In the dialog box that appears, specify a new password and click OK.

## Create a standard account

1.  Log on to the [ApsaraDB RDS console](https://rdsnext.console.aliyun.com).
2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.
6.  In the Create Account panel, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|Enter the username of the account. The username must meet the following requirements:

    -   The username must be 2 to 16 characters in length.
    -   The username must start with a letter and end with a letter or digit.
    -   The username can contain lowercase letters, digits, and underscores \(\_\). |
    |**Account Type**|Specify the type of the account. For this example, select **Standard Account**.|
    |**Authorized Databases**|Specify the authorized databases of the account. You can specify one or more authorized databases. You can also leave this parameter empty. This is because you can grant the permissions on specific databases to the account after the account is created.     1.  Select one or more databases from the Unauthorized Databases section and click the **rightwards arrow** to add the selected databases to the Authorized Databases section.
    2.  In the Authorized Databases section, select the **Read/Write \(DDL + DML\)**, **Read-only**, **DDL Only**, or **DML Only** permissions for each authorized database.

If you want to grant the same permissions on multiple authorized database at a time, select the authorized databases and click the button in the upper-right corner. For example, click **Set All to Read/Write \(DDL + DML\)**.

**Note:** The button in the upper-right corner changes after you click it. For example, after you click **Set All to Read/Write**, the button changes to **Set All to Read-only**. |
    |**Password**|Enter the password of the account. The password must meet the following requirements:

    -   The password must be 8 to 32 characters in length.
    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include: ! @ \# $ % ^ & \* \( \) \_ + - = |
    |**Confirm Password**|Enter the password of the account again.|
    |**Description**|Optional. Enter a description that helps identify the account. The description can be up to 256 characters in length.|

7.  Click **OK**.

## Related operations

|Operation|Description|
|---------|-----------|
|[CreateAccount](/intl.en-US/API Reference/Account management/Create account.md)|Creates an account that is used to manage the databases of an ApsaraDB RDS instance.|


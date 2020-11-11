# Reset the password of an account on an ApsaraDB RDS for SQL Server instance

This topic describes how to reset the password of an account on your ApsaraDB RDS for SQL Server instance. If the password is lost, you can reset the password in the ApsaraDB for RDS console.

## Procedure

**Note:** For data security purposes, we recommend that you change the password of each account on a regular basis.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Accounts**.

5.  Find the account whose password you want to reset, and click **Reset Password** in the Actions column.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6250359951/p4157.png)

6.  In the dialog box that appears, specify a new password and click **OK**.

    **Note:** The password must meet the following requirements:

    -   The password must be 8 to 32 characters in length.
    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include ! @ \# $ % ^ & \* \( \) \_ + - =

## Operations

|Operation|Description|
|---------|-----------|
|[ResetAccountPassword](/intl.en-US/API Reference/Account management/Reset account password.md)|Resets the password of an account on an ApsaraDB for RDS instance.|


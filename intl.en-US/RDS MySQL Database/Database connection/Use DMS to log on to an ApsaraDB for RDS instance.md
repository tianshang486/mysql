# Use DMS to log on to an ApsaraDB for RDS instance

This topic describes how to log on to an ApsaraDB for RDS instance by using Alibaba Cloud Data Management \(DMS\).

DMS is an all-in-one data management service that supports data management, structure management, account authorization, security audit, data trends, data tracking, BI charts, performance trends and optimization, and server management.

To improve data management experience, Alibaba Cloud provides a new version of DMS that includes more functions. In addition, the price of the DMS Enterprise edition is lowered. For more information, see [DMS pricing model changes](~~153131~~).

## Use the new version of DMS to log on to an RDS instance

Prerequisites

-   You have an Alibaba Cloud account or have applied for the credentials of a RAM user who has permissions on the target database on your RDS instance. For more information about how to apply for permissions, see [Manage permissions](~~60371~~).
-   Your RDS instance is registered with DMS by the administrator. For more information, see [Register an ApsaraDB instance](~~159708~~).

1.  Log on to the [DMS console](https://dms.aliyun.com/).

2.  In the left-side navigation pane, choose your RDS instance and click **Please login first**.

    **Note:** If your RDS instance uses the **Security Collaboration** control mode, you do not need to enter the username and password of the account used for the logon. You can choose **Logon-free instance** and double-click the target database to log on to that database.

    ![Please login first](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7150359951/p113304.png)

3.  In the dialog box that appears, enter the username and password of the account used for the logon and click **OK**.

    **Note:** The account used for the logon must have permissions on the target database. Otherwise, the target database is not displayed in the left-side navigation pane. For more information about how to modify the permissions of an account, see [Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Account/Account permission/Modify the permissions of a standard account on an ApsaraDB RDS for MySQL instance.md).

4.  In the left-side navigation pane, choose **Logged in instance** and double-click the target database to switch to that database.


## Use the original version of DMS to log on to an RDS instance

**Note:** If your DMS has been upgraded to the new version, we recommend that you use the new version of DMS to log on to your RDS instance.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID to open the Basic Information page.
4.  In the upper-right corner of the page, click **Log On to DB** to open the RDS Database Logon page.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5922472061/p4253.png)

    **Note:** Alibaba Cloud directs you to the original or new version of DMS based on your previous logon behavior.

5.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Endpoint:Port number**|The endpoint and port number that are used to connect to your RDS instance. The endpoint and port number are in the `<Endpoint>:<Port number>` format. Example: bpxxxxxxx.rds.aliyuncs.com:3433. For more information about how to view the endpoint and port number of an RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md).|
    |**Database Username**|The username of the account that is used to connect to your RDS instance.|
    |**Password**|The password of the account that is used to connect to your RDS instance.|

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7150359951/p4254.png)

6.  Click **Log On**.

    **Note:** If you want the browser to remember the password, select **Remember Password** before you click **Log On**.

7.  If the system prompts you to add the Classless Inter-Domain Routing \(CIDR\) block that contains the IP address of the DMS server to a whitelist of your RDS instance, click **Specify for All Instances** or **Specify for Current Instance**.
8.  Click **Log On**.


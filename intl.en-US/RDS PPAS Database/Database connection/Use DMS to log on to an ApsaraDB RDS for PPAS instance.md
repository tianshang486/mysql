# Use DMS to log on to an ApsaraDB RDS for PPAS instance

This topic describes how to log on to an ApsaraDB RDS for PPAS instance by using Alibaba Cloud Data Management \(DMS\).

## Precautions

You can use only an internal endpoint to log on to the RDS instance by using DMS.

## Procedure

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID. The Basic Information page appears.
4.  In the upper-right corner of the page, click **Log On to DB** to open the [RDS Database Logon page](https://dms.console.aliyun.com/?spm=5176.doc49015.2.5.1qi2e9&token=549cf345-ac05-455c-b3f9-75eadae023fe#/dms/login).

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5922472061/p4253.png)

5.  On the RDS Database Logon page, configure the following parameters:

    -   Endpoint:Port number: Enter the endpoint and port number that are used to log on to your RDS instance in the `<Internal endpoint>:<Internal port number>` format. Example: `rm-bpxxxxxxx.rds.aliyuncs.com:3433`. For more information about how to view the endpoint and port number of an RDS instance, see [View and modify the internal and public endpoints and ports of an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Database connection/View and modify the internal and public endpoints and ports of an ApsaraDB RDS for PPAS instance.md).
    -   Database Username: Enter the username of the account that is used to log on to your RDS instance.
    -   Password: Enter the password of the account that is used to log on to your RDS instance.
    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7150359951/p4254.png)

6.  Click **Log On**.

    **Note:** If you want the browser to remember the password, select **Remember Password** before you click **Log On**.

7.  If the system prompts you to add the classless inter-domain routing \(CIDR\) block of the DMS server to an IP address whitelist of your RDS instance, click **Specify for All Instances** or **Specify for Current Instance**.
8.  Click **Log On**.


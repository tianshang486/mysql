# Authorize the service account of an ApsaraDB RDS for MySQL instance

When you seek help from Alibaba Cloud technical support to locate problems that occurred on your ApsaraDB RDS for MySQL instance, you may need to grant permissions to a service account. The service account is used by Alibaba Cloud technical support to perform operations on the databases of your RDS instance. After the specified expiration time elapses, the service account is automatically deleted.

Your RDS instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 on RDS High-availability Edition \(with local SSDs\) or Enterprise Edition
-   MySQL 5.7 on RDS High-availability Edition \(with local SSDs\) or Enterprise Edition
-   MySQL 5.6 on RDS High-availability Edition
-   MySQL 5.5 on RDS High-availability Edition

## Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Accounts**.

5.  On the **Service Account Permissions** tab, find the permission that you want to grant to the service account, and turn on the switch in the **Permission Status** column.

    -   For problems that are related to IP address whitelists or database parameters, you only need to grant the **Configuration Permission** to the service account.
    -   For database performance problems that are caused by applications, you must grant the **Data Permission** to the service account.
    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5250359951/p4170.png)

6.  In the dialog box that appears, specify the expiration time of the service account and click **OK**.

    ![Set Expiration Time](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5250359951/p4171.png)


## What to do next

After you grant permissions to the service account, you can revoke the permissions or change the expiration time on the **Service Account Permissions** tab at any time.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5250359951/p4172.png)


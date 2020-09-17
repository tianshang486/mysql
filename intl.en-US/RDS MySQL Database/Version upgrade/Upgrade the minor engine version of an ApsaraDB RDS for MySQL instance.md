# Upgrade the minor engine version of an ApsaraDB RDS for MySQL instance

ApsaraDB RDS for MySQL supports automatic and manual updates to the minor engine version of your RDS instance. These updates increase performance, introduce new features, and fix known issues.

The default update mode is the automatic update mode. You can log on to the ApsaraDB for RDS console, go to the **Basic Information** page of your RDS instance, and then in the Configuration Information section view the **Minor Version Upgrade Mode**.

![Configure the automatic update mode](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6330359951/p49037.png)

-   **Auto**: When a new minor engine version is released, you will receive a notification. In addition, the system automatically updates your RDS instance to the new minor engine version during the specified maintenance window. For more information, see [Set the maintenance window of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Change/Set the maintenance window of an ApsaraDB RDS for MySQL instance.md).
-   **Manual**: When the lifecycle of the minor engine version on your RDS instance ends, you will receive a notification. The notification specifies that you must update your RDS instance to the latest stable minor engine version within one month. In most cases, the lifecycle of a minor engine version spans one year. You can manually update the minor engine version on the Basic Information page. For more information, see [\#section\_qb5\_2rv\_13b](#section_qb5_2rv_13b).

    **Note:** A minor engine version is taken offline after its lifecycle ends.


For more information about the features that are provided by various minor engine versions of ApsaraDB RDS for MySQL, see [Release Notes of Minor AliSQL Versions](/intl.en-US/AliSQL Kernel/Release Notes of Minor AliSQL Versions.md).

For more information about how to update the minor engine version of an ApsaraDB RDS for PostgreSQL instance, see [Upgrade the minor engine version of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Upgrade the kernel version of an ApsaraDB RDS for PostgreSQL instance.md).

**Note:** RDS instances that run SQL Server, PPAS, or MariaDB do not support updates to minor engine versions.

## Precautions

-   When you upgrade, migrate, or change the specifications of your RDS instance, the system updates the minor engine version of your RDS instance to improve performance and stability. This applies if the minor engine version of your RDS instance expires or will no longer be maintained.
-   An update to the minor engine version causes your RDS instance to restart. During the restart, a 30-second brief connection error may occur. The restart time can vary based on the specified **Upgrade Time**, which can be set to **Upgrade Immediate** or **Upgrade within maintenance period**. We recommend that you upgrade the minor engine version of your RDS instance during off-peak hours. Alternatively, make sure that you configure your application to automatically reconnect to your RDS instance.
-   After you update the minor engine version of your RDS instance, you cannot cancel the update.
-   When you upgrade your RDS instance, the system automatically updates its minor engine version.

## Configure the minor engine version update mode of an RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the Configuration Information section of the **Basic Information** page, click **Configure** next to **Minor Version Upgrade Mode**.

5.  Select **Auto** or **Manual** and click **OK**.

    ![Configure the minor engine version update mode](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6330359951/p49038.png)


## Manually update the minor engine version of an RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  On the **Basic Information** page, click **Upgrade Minor Version**.

    **Note:** If the Upgrade Minor Version button does not appear, you are using the latest minor engine version.

5.  In the dialog box that appears, specify the **Upgrade Time** and click **OK**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2050359951/p49040.png)


## FAQ

-   After I updated the minor engine version of my RDS instance, why does the SELECT @@version statement still return the minor engine version that I used before the update?

    The SELECT @@version statement returns the minor version of Alibaba Cloud. If you want to query the minor engine version of your RDS instance, run the `show variables like '%rds_release_date%'` command.

-   Is each update targeted only for the next minor engine version?

    No, each update is targeted for the latest minor engine version.


## Related operations

|Operation|Description|
|---------|-----------|
|[Upgrade minor version](/intl.en-US/API Reference/Version upgrade/Upgrade minor version.md)|Updates the minor engine version of an ApsaraDB for RDS instance.|


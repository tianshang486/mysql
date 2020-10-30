# Migrate the data of an ApsaraDB RDS for PostgreSQL instance from the ApsaraDB RDS for PostgreSQL console

This topic describes how to migrate the data of an ApsaraDB RDS for PostgreSQL instance from the ApsaraDB RDS for PostgreSQL console to the ApsaraDB RDS console.

-   The source RDS instance runs PostgreSQL 11.
-   The source RDS instance runs the latest minor engine version.

    **Note:** You can log on to the ApsaraDB RDS for PostgreSQL console and go to the **Basic Information** page for an RDS instance to view its minor engine version. If the RDS instance does not run the latest minor engine version, you can click **Upgrade Minor Version** to upgrade its minor engine version.

-   The `wal_level` parameter is set to `logical` for the source RDS instance.
-   The source RDS instance is managed in the ApsaraDB RDS for PostgreSQL console.

    **Note:** You can determine in which console an RDS instance is managed based on the domain name of the console. If the domain name is postgresql.console.aliyun.com, the RDS instance is managed in the ApsaraDB RDS for PostgreSQL console. If the domain name is rdsnext.console.aliyun.com, the RDS instance is managed in the ApsaraDB RDS console.


Due to historical reasons, the ApsaraDB RDS for PostgreSQL console was used for a short period of time. This console differs from the ApsaraDB RDS console in terms of UI design and functionality. In addition, the ApsaraDB RDS console provides better services at lower prices. We recommend that you migrate the data of your RDS instance from the ApsaraDB RDS for PostgreSQL console to the ApsaraDB RDS console.

## Impact

The migration causes a transient connection error. We recommend that you perform the migration during off-peak hours.

## Precautions

Each migration task is used to migrate the data of only a single database. If you want to migrate the data of more than one database, create a migration task for each of the databases.

## Migration process

1.  [Configure the source RDS instance](#section_9nj_qts_28q)
2.  [Configure the destination RDS instance](#section_4xr_c2x_mf1)
3.  [Use DTS to migrate data](#section_xk0_6bm_s01)
4.  [Switch over your workloads to the destination RDS instance](#section_izm_8yc_cny)

## Configure the source RDS instance

1.  Log on to the [ApsaraDB RDS for PostgreSQL console](https://postgresql.console.aliyun.com/).

2.  In the top navigation bar, select the region where the source RDS instance resides.

3.  Find the source RDS instance and click its ID.

4.  On the **Basic Information** page, click **Apply for Public Endpoint**. In the message that appears, click **OK**.

    **Note:** You can view the public endpoint only after an IP address whitelist is configured. We recommend that you choose **Data Security** \> **Whitelist Configuration** in the left-side navigation pane and then enter 0.0.0.0/0 in the **Allowed IP Addresses** field for the IP address whitelist labeled default. This allows all devices to access the source RDS instance.


## Configure the destination RDS instance

1.  Log on to the [ApsaraDB RDS console](https://rds-buy.aliyun.com/nextBuy/?#/create/rds/mysql) and create an RDS instance that runs PostgreSQL 11. This RDS instance is the destination RDS instance. For more information, see [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md).

2.  Create a privileged account on the destination RDS instance. For more information, see [Create an account on an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Account/Create an account on an ApsaraDB RDS for PostgreSQL instance.md).

3.  Create databases on the destination RDS instance. We recommend that each database on the source RDS instance has a counterpart with an identical name on the destination RDS instance. For more information, see [Create a database on an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Database/Create a database on an ApsaraDB RDS for PostgreSQL instance.md).


## Use DTS to migrate data

For more information about the precautions, see [Migrate incremental data from a user-created PostgreSQL database \(version 10.1 to 12\) to an ApsaraDB RDS for PostgreSQL instance]().

1.  Log on to the [DTS console](https://dts.console.aliyun.com/).

2.  In the left-side navigation pane, click **Data Migration**. In the upper-right corner of the page, click **Create Migration Task**.

3.  Configure the following parameters.

    |Section|Parameter|Description|
    |:------|:--------|:----------|
    |None|Task Name|Enter the name that Alibaba Cloud Data Transmission Service \(DTS\) generates for the migration task. We recommend that you specify an informative name for easy identification. You do not need to use a unique task name.|
    |Source Database|Instance Type|Select **User-Created Database with Public IP Address**.|
    |Instance Region|Select the region to which the source RDS instance belongs.|
    |Database Type|Select **PostgreSQL**.|
    |Hostname or IP Address|Enter the public endpoint of the source RDS instance.|
    |Port Number|Enter the port number that is associated with the public endpoint of the source RDS instance.|
    |Database Name|Enter the name of the source database whose data you want to migrate from the source RDS instance. **Note:** Each migration task is used to migrate the data of only a single database. If you want to migrate the data of more than one database, create a migration task for each of the databases. |
    |Database Account|Enter the username of the account that you want to use to log on to the source RDS instance. We recommend that you use the privileged account or a standard account that has read and write permissions on the source database.|
    |Database Password|Enter the password of the account that you want to use to log on to the source RDS instance. **Note:** After you specify the source database parameters, click **Test Connectivity** next to **Database Password** to verify whether the specified parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the source database parameters based on the check results. |
    |Destination Database|Instance Type|Select **RDS Instance**.|
    |Instance Region|Select the region to which the destination RDS instance belongs.|
    |RDS Instance ID|Select the ID of the destination RDS instance.|
    |Database Name|Enter the name of the destination database to which you want to migrate data on the destination RDS instance.|
    |Database Account|Enter the username of the account that you want to use to log on to the destination RDS instance. We recommend that you use the privileged account or a standard account that has read and write permissions on the destination database.|
    |Database Password|Enter the password of the account that you want to use to log on to the source RDS instance. **Note:** After you specify the destination database parameters, click **Test Connectivity** next to **Database Password** to verify whether the parameters are valid. If the specified parameters are valid, the **Passed** message appears. If the **Failed** message appears, click **Check** next to **Failed**. Modify the destination database parameters based on the check results. |

4.  In the lower-right corner of the page, click **Set Whitelist and Next**.

5.  Select migration types and objects.

    |Configuration item|Description|
    |:-----------------|:----------|
    |Migration types|Select all of the migration types. The supported migration types are **Schema Migration**, **Full Data Migration**, and **Incremental Data Migration**.|
    |Migration objects|Select objects in the **Available** section and click the ![Right arrow](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p40698.png) icon to move them to the **Selected** section.|

6.  In the lower-right corner of the page, click **Precheck**.

    **Note:**

    -   A precheck is performed before the migration task starts. The migration task can start only after it passes the precheck.
    -   If the migration task fails the precheck, click the ![Info icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3457359951/p47468.png) icon next to each failed check item to view details about the failure. After all of the identified failures are rectified, you must perform a precheck again.
7.  After the task passes the precheck, click **Next**.

8.  In the **Confirm Settings** dialog box, specify **Channel Specification**, read and select Data Transmission Service \(Pay-As-You-Go\) Service Terms, and then click **Buy and Start**.


## Switch over your workloads to the destination RDS instance

**Warning:** To prevent data losses that may occur during the switchover, you must stop your workloads for a short period of time. We recommend that you perform the switchover during off-peak hours.

1.  Wait until the migration task enters the **Incremental Data Migration** phase. The state of the incremental data migration phase must show **The migration task is not delayed** or a delay shorter than 5 seconds.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1940359951/p72817.png)

2.  Stop your workloads and forbid new writes to the source database.

3.  Log on to the source database and run the following command to verify that no new sessions are created to write data:

    ```
    select * from pg_stat_activity;
    ```

4.  Wait until the state of the **Incremental Data Migration** phase changes to **The migration task is not delayed** and stays in that state for one minute or longer. Then, manually terminate the migration task.

    ![The migration task is not delayed](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2940359951/p47604.png)

5.  On the **Basic Information** page for the source RDS instance, click **Lock Instance to Read-only**. In the message that appears, click **OK**.

6.  Update the endpoints of the destination RDS instance to your application.


The data migration is complete. Observe the performance of the source RDS instance for a period of time. If your workloads run properly on the destination RDS instance, we recommend that you release or[submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to unsubscribe from the source RDS instance..


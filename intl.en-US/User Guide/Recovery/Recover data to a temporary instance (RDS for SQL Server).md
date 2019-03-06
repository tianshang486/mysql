# Recover data to a temporary instance \(RDS for SQL Server\) {#concept_en3_pfn_ydb .concept}

**Note:** This function is different from the clone instance function.

The data recovery function minimizes damage caused by database misoperations. We recommend that you recover data to the master instance through a temporary instance. That is, recover data to a temporary instance, verify the data, and then migrate the data to the master instance. This avoids the impact of data recovery on the master instance.

## Prerequisite {#section_oqz_thr_zgb .section}

-   The instance type is one of the following:
    -   SQL Server 2012 Enterprise Basic Edition
    -   SQL Server 2012/2016 Web
    -   SQL Server 2008 R2
-   The instance has data backups.
-   To recover data to a point in time, the instance must also has log backs.

## Attentions {#section_qn5_l2n_ydb .section}

-   Creating a temporary instance does not affect the master instance.
-   The temporary instance inherits the account and password of the backup file.
-   The network type of the temporary instance is classic network.
-   A master instance can have only one temporary instance at a time. Before creating a temporary instance, delete the existing temporary instance of the master instance.
-   The temporary instance is free of charge, but will be released automatically 48 hours after being created.

## Create a temporary instance {#section_vbm_n2n_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/) and select the region where the target instance is located.
2.  Click the ID of the target instance to go to the Basic information page.
3.  Click **Backup and Recovery** in the left-side navigation pane.
4.  Click the **Temporary Instance** tab.
5.  Select a point in time for recovery and click **Create Temporary Instance**.
6.  In the displayed dialog box, click **OK**.
7.  Go back to the **Instances** page.

## Recover data from the temporary instance to the master instance {#section_xm5_phv_l2b .section}

1.  After the temporary instance is created successfully, click the ID of the master instance to go to the Basic information page.
2.  Click **Create Data Migration Task** in the upper right corner to go to the [Data Transmission Service console](http://dts.console.aliyun.com/).
3.  Click **Data migration** in the left-side navigation pane.
4.  Click **Create migration task**.
5.  Set parameters. 
    -   Task name: A default task name is generated. You can modify it so that you can identify it more easily later.
    -   Source database information:
        -   Instance type: Select **RDS instance**.
        -   Instance region: Select the region where the master instance is located.
        -   RDS instance ID: Select the ID of the temporary instance.
        -   Database account: It is the same as the account name of the master instance. Make sure that this account has read and write permissions on the data to be migrated.
        -   Database password: It is the same as the account password of the master instance.
    -   Target database information:
        -   Instance type: Select **RDS instance**.
        -   Instance region: Select the region where the master instance is located.
        -   RDS instance ID: Select the master instance that has a temporary instance.
        -   Database account: Enter the account name of the master instance. Make sure that this account has read and write permissions on the data to be migrated.
        -   Database password: Enter the account password of the master instance.
6.  Click **Authorization whitelist and enter into next step**.
7.  Select the migration type.
8.  In the left pane, select the objects to be migrated and click **\>** to add them to the right pane. If you want to modify the name of a migrated object in the target database, you can hover the mouse over the database that needs to be modified in the Selected objects pane and click the displayed **Edit** button.
9.  Click **Pre-check and start**.
10. If the pre-check fails, click **!** next to the failed check item to view detailed failure information, and perform troubleshooting accordingly. After the troubleshooting, find the migration task in the Migration task list page and restart the pre-check.
11. After the pre-check is passed, click **OK** to start the migration task.


# \[Important\] RDS network link upgrade

To ensure stability and high performance, we recommend that you upgrade the network connection mode of your ApsaraDB for RDS instance from the safe mode \(database proxy mode\) to the high-performance mode \(standard mode\).

## Potential risks of not performing the upgrade

If you do not perform the upgrade, network jitter may occur when you attempt to access resources. This causes interruptions to your business. To ensure stability, we recommend that you perform the upgrade as soon as possible.

## Benefits of the upgrade

-   Your RDS instance is more stable.
-   The average response time decreases by 20%, and the performance of your RDS instance increases.

## Instances that need to be upgraded

You must upgrade the network connection modes of all your RDS instances that run MySQL, PostgreSQL, PPAS, or HybridDB for PostgreSQL engines in safe mode \(database proxy mode\) with read/write splitting disabled. To check whether an RDS instance is in safe mode, follow these steps:

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click Database Connection. In the Database Connection section of the Instance Connection tab, check the setting of **Database Proxy \(Safe Mode\)**.
    -   If the mode is **Disabled**, you do not need to upgrade the network connection mode of the RDS instance.
    -   If the mode is **Enabled**, you must upgrade the network connection mode of the RDS instance.

        **Note:**

        -   If the RDS instance is a primary instance to which read-only instances are attached, you only need to upgrade the network connection mode of the RDS instance. The system automatically upgrades the network connection modes of the read-only instances.

## Impacts of the upgrade

-   While you perform the upgrade, there may be a 30-second brief disconnection. Make sure that your application is configured to automatically reconnect to your RDS instance.
-   In database proxy mode, the multi-statement function is enabled at the protocol layer by default. If the multi-statement function is disabled after the upgrade and you execute multiple SQL statements, the system reports SQL statement execution errors. We recommend that you check and add connection parameters before the upgrade. For example, add the allowMultiQueries parameter in the JDBC API as follows:

    ```
    dbc:mysql:///test? allowMultiQueries=true
    ```


## Method 1 to perform the upgrade

1.  Navigate to the **Database Connection** page in the ApsaraDB for RDS console and click **Switch Access Mode**.
2.  In the dialog box that appears, click **Confirm** to disable the database proxy mode.
3.  Verify that your database services are properly running.

    **Note:** Do not skip this step.


## Method 2 to perform the upgrade

**Note:** This method is suitable only for some RDS instances.

1.  Navigate to the **Database Proxy** page in the ApsaraDB for RDS console and click the slider next to **Database Proxy \(Safe Mode\)**.
2.  In the dialog box that appears, click **Confirm** to disable the database proxy mode.
3.  Verify that your database services are properly running.

    **Note:** Do not skip this step.


## FAQ

1.  How do I determine whether I need to upgrade the network connection mode of my RDS instance?

    For more information, see the "[Instances that need to be upgrade](#section_hzy_lkr_mgb)" section.

2.  Why am I unable to upgrade the network connection mode of my RDS instance?

    If read/write splitting is enabled, you cannot upgrade the network connection mode of your RDS instance. An upgrade solution is under development for RDS instances that have read/write splitting enabled.

3.  Which configuration data do I need to modify on my application after the upgrade?

    While you upgrade the network connection mode, there may be a 30-second brief disconnection. You must configure your application to automatically reconnect to your RDS instance. If no automatic reconnection mechanism is configured, you may need to manually restart services. After the upgrade, the endpoints and IP addresses of your RDS instance remain unchanged. You do not need to update this information on your application.

4.  Can I switch the network connection mode of my RDS instance to the safe mode \(database proxy mode\)?

    Yes, you can switch the network connection mode of your RDS instance to the safe mode \(database proxy mode\). However, you do not need to do so. The safe mode is suitable for communication over both the Internet and an internal network. These types of communication are also supported by the high-performance mode \(standard mode\).

5.  If my RDS instance is attached with read-only instances, do I need to upgrade the network connection mode of each read-only instance separately?

    No, you only need to upgrade the network connection of your RDS instance. The system automatically upgrades the network connection modes of the attached read-only instances.



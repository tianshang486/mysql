# Switch between master and slave instances {#concept_ftz_42j_wdb .concept}

Each high-availability instance consists of a master instance and a slave instance. The master and slave instances are located in different zones within the same region.

The data in the master instance is synchronized to the slave instance in real time. You can only access the master instance. The slave instance exists only as a backup. However, when the rack \(where the master instance is located\) encounters an error, the master and slave instances can be switched. After the switch, the original master instance becomes a backup instance, and rack-level disaster tolerance can be realized.

This topic describes how to switch between master and slave instances.

## Prerequisites {#section_2t5_i2x_06t .section}

Your RDS instance is created in the High-availability or AlwaysOn edition.

**Note:** 

An RDS instance in the Basic Edition does not have a slave instance and therefore does not support the switch.

## Precautions {#section_bwn_r2j_wdb .section}

-   Switching between master and slave instances may result in transient disconnection. Make sure that your application has a reconnection configuration.
-   If read-only instances are mounted to the master instance, the data in the read-only instances shows a few minutes' delay due to data replication link reestablishment and incremental data synchronization after the switching is complete.

## Procedure {#section_qjt_s2j_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper left-corner, select the region where the target instance is located.
3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, select **Instance Availability**.
5.  In the Availability Information section, click **Switch Master/Slave Instance**.
6.  Select **Switch now** or **Switch within maintenance period**.

    **Note:** During the switch, many operations cannot be performed. Therefore, we recommend that you choose to switch within the maintenance period.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7885/15656820593021_en-US.png)

    **Note:** To change the maintenance period, you can take these steps:

    1.  Click **Modify** to open the Basic Information page.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7885/15656820603022_en-US.png)

    2.  In the Configuration Information area at the lower left corner, select a maintenance period and click **Save**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7885/15656820603023_en-US.png)

    3.  Go back to the page for switching between master and slave instances and refresh the page.
7.  Click **OK**.


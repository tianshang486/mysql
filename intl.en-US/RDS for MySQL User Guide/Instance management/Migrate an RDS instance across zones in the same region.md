# Migrate an RDS instance across zones in the same region {#concept_zwp_gdj_wdb .concept}

You can migrate your RDS instance from one zone to another in the same region. The attributes, configuration, and connection addresses of the instance remain unchanged after the migration. The time required for the migration varies depending on the data volume of the instance. In typical cases, the migration takes a few hours.

## Precautions {#section_mvn_bfl_bhb .section}

During the migration, the connection to your RDS instance remains unavailable for 30 seconds. Make sure that your application can be reconnected to your RDS instance after the migration. The main risks are as follows:

-   The migration changes the virtual IP address. Therefore, we recommend that you use the connection address but not the IP address in your application to establish a connection.
-   You must delete cached data on the client in a timely manner. Otherwise, data can be read but cannot be written.
-   A change to the virtual IP address has temporary impact on the availability of DRDS. You must update and view the connection information on the [DRDS console](https://drds.console.aliyun.com/prectrl/home/index) in a timely manner.
-   A change to the virtual IP address has temporary impact on [DMS](https://www.alibabacloud.com/help/doc-detail/47550.htm) and [DTS](https://www.alibabacloud.com/help/doc-detail/26592.htm), which automatically return to normal after the migration is complete.

## Migration scenarios {#section_sbx_p15_z2b .section}

|Migration scenario|Description|
|------------------|-----------|
|Migrate an RDS instance from one zone to another|The zone where the RDS instance is located is overloaded or cannot meet the performance requirements of the instance.|
|Migrate an RDS instance from one zone to multiple zones|The master and slave nodes are located in different equipment rooms in different zones to enhance disaster tolerance. A multi-zone instance is superior to a single-zone instance because it can survive more disasters. For example, a single-zone instance can survive server and rack faults while a multi-zone instance can survive equipment room faults.

 |
|Migrate an RDS instance from multiple zones to one zone|This scenario is provided to meet the requirements of specific functions.|

## Fees {#section_phl_55t_z2b .section}

This function is free of charge. No fee is charged even when you migrate an RDS instance from one zone to multiple zones.

## Prerequisites {#section_gr3_3rt_z2b .section}

Instance types: MySQL 5.5, MySQL 5.6, and MySQL 5.7 \(with local SDDs\).

Regions: This function is available only when the region where RDS instance is located consists of multiple zones. For more information about regions and zones, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

## Procedure {#section_own_qdj_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![Select a region.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156697457036543_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  In the **Basic Information** section of the Basic Information page, click **Migrate Across Zones**.

    ![跨可用区迁移](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7884/15669745703015_en-US.png)

5.  In the displayed dialog box, specify the destination zone, VSwitch, and migration time, and click **OK**.

    **Note:** If you want to change the maintenance window, follow these steps:

    1.  Click **Change**.

        ![修改时间窗](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7884/15669745703017_en-US.png)

    2.  In the **Configuration Information** section, specify the maintenance window and click **Save**.

        ![时间窗](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7884/156697457021079_en-US.png)

    3.  Refresh the page, and perform the migration again.

## APIs {#section_hcn_555_jgb .section}

|API|Description|
|---|-----------|
|[MigrateToOtherZone](../intl.en-US/API Reference/Instance management/MigrateToOtherZone.md#)|Used to migrate an RDS instance across zones.|


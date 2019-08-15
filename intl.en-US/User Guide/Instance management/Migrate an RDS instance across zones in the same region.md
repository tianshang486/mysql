# Migrate an RDS instance across zones in the same region {#concept_zwp_gdj_wdb .concept}

You can migrate your RDS instance from one zone to another in the same region. The attributes, configuration, and connection address of the instance remain unchanged after the migration. The time required for the migration varies depending on the data volume of the instance. In typical cases, the migration takes a few hours.

## Precautions {#section_mvn_bfl_bhb .section}

Services may be disconnected for 30 seconds during cross-zone migration. Make sure that your application is configured to reconnect to the instance after the application is disconnected. Pay attention to the following information:

-   Cross-zone migration causes changes to virtual IP addresses \(VIPs\). We recommend that you connect your application to the connection address of the instance instead of the VIP.
-   Clear the cache on the client to prevent data write-in failures.
-   Any change to the VIP affects the availability of DRDS for a short period of time. Refresh the page and view the connection information in the [DRDS console](https://drds-intl.console.aliyun.com/prectrl/home/index#/overview).
-   Any change to the VIP affects the operation of [DMS](https://www.alibabacloud.com/help/zh/doc-detail/47550.htm) and [DTS](https://www.alibabacloud.com/help/zh/doc-detail/26592.htm) for a short period of time. After the migration is complete, you can use DMS and DTS normally.

## Migration types {#section_sbx_p15_z2b .section}

|Migration type|Scenario|
|--------------|--------|
|Migrate an RDS instance from one zone to another|The zone where the RDS instance is located is in full load or cannot meet the performance requirements of the instance.|
|Migrate an RDS instance from one zone to multiple zones|The master and slave nodes are deployed in different equipment rooms in different zones to enhance disaster tolerance. Compared with single-zone instances, multi-zone instances can withstand disasters at higher levels. For example, single-zone instances can tolerate server- and rack-related faults, whereas multi-zone instances can tolerate data center-related faults.

 |
|Migrate an RDS instance from multiple zones to one zone|Specific function requirements are required.|

## Fees {#section_phl_55t_z2b .section}

This feature is free of charge even if you migrate instances from one zone to multiple zones.

## Prerequisites {#section_gr3_3rt_z2b .section}

The instance type is one of the following:

-   MySQL 5.5, MySQL 5.6, and MySQL 5.7 \(based on local SSDs\)
-   SQL Server 2008 R2
-   PostgreSQL 10 High-availability Edition and PostgreSQL 9.4
-   PPAS 10

The region where the RDS instance is located consists of multiple zones. For more information about regions and zones, see [Regions and zones](https://www.alibabacloud.com/help/zh/doc-detail/40654.htm).

## Procedure {#section_own_qdj_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![Region screenshot](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156586103037169_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  Click **Migrate Across Zones**.

    ![迁移可用区](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7884/15658610303015_en-US.png)

5.  In the displayed dialog box, specify the destination zone, VSwitch, and migration time, and then click **OK**.

    **Note:** To change the maintenance window, follow these steps:

    1.  Click **Change**.

        ![修改维护时间](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7884/15658610303017_en-US.png)

    2.  In the Configuration Information section, change the maintenance window and click **Save**.

        ![修改维护时间](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7884/156586103121079_en-US.png)

    3.  Refresh the page, and perform the migration again.


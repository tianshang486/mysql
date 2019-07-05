# Upgrade SQL Server 2008 R2 {#concept_t13_1wj_dhb .concept}

You can upgrade RDS for SQL Server 2008 R2 to a later version, and migrate instances across zones during the upgrade. We recommend that you use a temporary instance to test the version compatibility before performing the upgrade.

## Prerequisites {#section_x1y_gwj_dhb .section}

-   The storage capacity of your SQL Server 2008 R2 instance is at least 20 GB.
-   The [TDE](../intl.en-US/User Guide/Security/Set TDE.md#) feature of your SQL Server 2008 R2 instance is disabled.

## Precautions {#section_olz_cjr_dhb .section}

-   Your instance cannot be rolled back to SQL Server 2008 R2 after the upgrade is completed.

    **Warning:** We recommend that you use [a temporary instance of the target version](#) to test the version compatibility before the upgrade.

-   You can upgrade an instance from SQL Server 2008 R2 to SQL Server 2012/2016 Enterprise Edition or SQL Server 2016 Standard Edition only.
-   If SSL is enabled for your instance, you can upgrade your instance version directly. After the upgrade is completed, the instance connection address remains unchanged, but SSL is disabled by default. You need to re-enable it. For more information, see [Set SSL encryption](../intl.en-US/User Guide/Security/Set SSL encryption.md#).
-   The TDE feature remains after you upgrade your instance from SQL Server 2008 R2 to SQL Server 2012/2016 Enterprise Edition, but does not exist after you upgrade your instance to SQL Server 2016 Standard Edition.
-   After the upgrade is completed, you need to switch over services. The downtime caused by the switchover varies depending on the instance size. In most cases, the switchover is completed within 20 minutes. We recommend that you switch over services when the system is being maintained. Make sure each application can be reconnected in the event of a disconnection.

## Procedure {#section_wwz_hv4_dhb .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  Select the region where your instance is located.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156230605236543_en-US.png)

3.  Click the ID of your instance.
4.  On the Basic Information page, click **Upgrade Version**. In the message that appears, click **Confirm**.

    ![Upgrade the database version](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/142817/156230605241115_en-US.png)

5.  On the Upgrade Engine Version page, modify your instance configurations as follows.

    |Parameter|Description|
    |---------|-----------|
    |**Upgrade To**|Select the target version. The **Edition**, **Storage Type**, and **Type** settings vary depending on the selected target version.|
    |**Edition**|Select **High-availability**: The classic HA architecture allows your instance to work in primary/secondary mode to achieve balanced performance in all aspects.|
    |**Storage Type**|Select **SSD**.|
    |**Zone**|Select the zone to which you want to migrate your instance. Multi-zone migration is supported.|
    |**Type**|Each instance type supports a specific number of CPU cores, memory, maximum number of connections, and maximum IOPS. For more information, see [Instance type list](../intl.en-US/Product Introduction/Instance types/Instance type list.md#).|
    |**Network Type**|**Classic Network** is unavailable. You must specify the VPC information.     -   If your instance is accessed through a classic network before the upgrade, you can change its network type to VPC and configure a VSwitch.
    -   If your instance is accessed through a VPC or through both a classic network and a VPC before the upgrade, you are not allowed to change its VPC. However, you can change its VSwitch. The available VSwitches vary depending on the specified **zone** and VPC.
 |
    |**VSwitch**|Select the target VSwitch. If you select multiple zones for your instance, you need to select multiple target VSwitches.|
    |**Switching Time**|     -   **Switch Immediately After Data Migration**: Data is migrated and then services are switched over immediately.
    -   **Switch Within Maintenance Window**: Data is migrated immediately, and services are switched over during a maintenance period.
 |

    ![Upgrade configuration](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/142817/156230605241116_en-US.png)

6.  Select the terms of service and click **Confirm**.

## Change the database connection address {#section_c54_3z4_dhb .section}

After the upgrade, the instance can only be accessed through a VPC. The following table describes how to change the database connection address for the instance after the upgrade based on the original network type of the instance.

|Original network type|Change rule|
|---------------------|-----------|
|Classic network|The instance after the upgrade is accessed through both a classic network and a VPC: -   The original connection address of the classic network still applies to the instance after the upgrade. This address does not expire.
-   A VPC connection address is generated for the instance after the upgrade based on the VPC that is specified during the upgrade.

 |
|VPC|A VPC connection address is generated for the instance after the upgrade based on the VPC that is specified during the upgrade. This address replaces the original VPC connection address of the instance.|
|Classic network and VPC|The instance after the upgrade is accessed still through both a classic network and a VPC. The original classic network and VPC connection addresses still apply to the instance after the upgrade. The expiration time of the classic network connection address remains unchanged.|

## Create a temporary instance of the target version {#section_hw0_nlc_1uk .section}

Before the upgrade, we recommend that you create a temporary instance of the target version to test the version compatibility.

**Note:** You can create a temporary instance of the target version only for an SQL Server 2008 R2 instance whose TDE and SSL are disabled.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  Select the region where your instance is located.
3.  Click the ID of your instance.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  On the Temporary Instance tab, specify the time at which you want to clone data, and click **Create Temporary Instance of Higher Version**.

    ![Select a temporary instance of the target version](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/142817/156230605246604_en-US.png)

6.  In the dialog box that appears, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Zone**|Select the zone where you can create a temporary instance.|
    |**Upgrade To**|Select the target version. The available target versions are as follows:     -   2016 SE
    -   2016 EE
    -   2012 EE
 |
    |**VPC**|Select a VPC. You must select the VPC where the ECS instance to be connected is located. Otherwise, the temporary instance cannot communicate with the ECS instance through the internal network.|
    |**VSwitch**|Select a VSwitch from the specified VPC.|

    **Note:** The system provides a default instance type and a default storage type for a temporary instance. The temporary instance will be automatically released after seven days.

    ![Temporary instance of the target version](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/142817/156230605346602_en-US.png)

7.  Click **OK**.

## Related APIs {#section_f11_51p_dhb .section}

|API|Description|
|---|-----------|
|[UpgradeDBInstanceEngineVersion](../intl.en-US/API Reference/Instance management/UpgradeDBInstanceEngineVersion.md#)|Upgrades the database version of an instance.|


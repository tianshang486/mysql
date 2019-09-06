# Restore an RDS for MySQL instance or table {#concept_ocr_swk_ngb .concept}

This topic describes how to restore an RDS for MySQL instance or table by using a backup set.

## Prerequisites {#section_o5q_1p4_ydb .section}

-   The DB engine version is RDS for MySQL 5.6 High-availability Edition.
-   The region is Singapore. If the RDS instance is located in any other region, you must enable the XXX function in the console \(navigation path: **Backup and Restoration** \> **Backup Settings**\). 地域为新加坡。 如果实例位于其它地域，请在控制台**Backup and Restoration** \> **Backup Settings**里开启单库单表恢复功能。

    ![控制台开通库表恢复](images/44546_en-US.png)

    **Notice:** 开通单库单表恢复功能后，备份格式会修改，用于支持库表恢复，且开通之后无法关闭该功能。

-   If you want to restore data to the original RDS instance, the original RDS instance must meet the following conditions:
    -   The instance is in **Running** state and is not locked.
    -   The instance is not involved in any migration task.
    -   If you want to restore data from a time point, the log backup function is enabled.
    -   If you want to restore data from a backup set, the instance must have at least one backup set.
-   If you want to restore data to a new RDS instance, the original instance must meet the following conditions:
    -   The instance is in **Running** state and is not locked.
    -   If you want to restore data from a time point, the log backup function is enabled.
    -   If you want to restore data from a backup set, the instance must have at least one backup set.

## Precautions {#section_slr_ynq_ngb .section}

-   单库单表恢复功能会将备份文件从tar压缩包变成xbstream文件包，备份文件占用的存储空间会略微增大，请您关注[备份使用量](../../../../intl.en-US/User Guide/Backup/View the free quota of the backup space.md#)。 超出免费备份空间额度的部分将会产生额外费用，请合理设计备份周期，以满足业务需求的同时，兼顾备份空间的合理利用。
-   实例内的表低于50000张才可以使用单库单表恢复功能，超过50000张表时无法使用。
-   每次最多选择50个库或者表。

## Procedure {#section_m3j_zlb_3gb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.
3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click Backup and Restoration.
5.  In the upper-right corner, click **数据库 库/表级别恢复**. In the displayed dialog box, set the following parameters.

    **Note:** If the **数据库 库/表级别恢复** button is unavailable, see [Prerequisites](#section_o5q_1p4_ydb).

    ![库/表级别恢复](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/156775924237783_en-US.png)

    ![库/表级别恢复参数设置1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/115355/156775924337784_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**回档位置**|     -   **回档到原实例**: restores the RDS instance or table to the original RDS instance. 将库/表恢复到原实例中。
    -   **回档到新实例**: purchases a new RDS instance and restores the RDS instance or table to the new RDS instance. 新购实例，并将库/表恢复到新实例中。
 |
    |**还原方式**|     -   **按备份集**
    -   **按时间点**: You can specify any time point within the log retention period. For information about how to view or change the log retention period, see [Back up RDS data](../../../../intl.en-US/User Guide/Backup/Back up RDS data.md#).
 **Note:** The **按时间点** option is available only when the log backup function is enabled.

 |
    |**备份集**|Select the backup set used for restoring the RDS instance or table. **Note:** This parameter is available when you set the **还原方式** parameter to **按备份集**.

 |
    |**还原时间**|Select the time point from which you want to restore the RDS instance or table. **Note:** This parameter is available when you set the **还原方式** parameter to **按备份集**.

 |
    |**需要恢复的库和表**|Select the RDS instance or table you want to restore. 勾选需要恢复的库或表。|
    |**已选择的库和表**|     -   Displays the selected RDS instance and table, and allows you to specify the names of the RDS instance and table to which data is restored. 显示已勾选的库和表，并可预设恢复后的库/表名称。
    -   Displays the total size of the selected RDS instance and table as well as the remaining storage space of the instance. Make sure that the remaining storage space is sufficient. 显示已勾选的库和表的总大小，以及该实例剩余存储空间，请关注剩余存储空间是否足够。
 |

6.  单击**确定**。

    **Note:** 若**回档位置**选择的是**回档到新实例**，会跳转到实例购买页面，设置新实例的参数并完成支付即可。

    ![库/表级别恢复新建实例](images/37786_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**系列**|     -   基础版: The DB system has only one instance. In this edition, compute is separated from storage, which is cost-effective. We recommend that you do not use this edition in production environments.
    -   高可用版: The DB system has two instances: one master instance and one slave instance. The two instances work in a classic high-availability architecture.
 For more information about the product series, see [Product series overview](../../../../intl.en-US/Product Introduction/Product series/Product series overview.md#). The product series available in the console vary depending on the used DB engine version.

 |
    |**可用区**| A zone is an independent physical location in a region. Zones in the same region are basically the same. 可用区是地域中的一个独立物理区域，不同可用区之间没有实质性区别。

 You can create an RDS instance in the same or different zone from your ECS instance. 您可以选择将RDS实例与ECS实例创建在同一可用区或不同的可用区。 **Note:** The new RDS instance must be in the same region as the original RDS instance.

 |
    |**规格**| Each specification corresponds to specific number of CPU cores, memory space, maximum number of connections, and maximum IOPS. For more information, see [Instance types](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md#). 每种规格都有对应的CPU核数、内存、最大连接数和最大IOPS。 具体请参见[实例规格表](../../../../intl.en-US/Product Introduction/Instance types/Instance types.md)。

 RDS instances fall into the following types:

    -   通用型: A general-purpose instance owns dedicated memory and I/O resources but shares CPU and storage resources with the other general-purpose instances on the same server.
    -   独享型: A dedicated instance owns dedicated CPU, memory, storage, and I/O resources.
    -   独占物理机型: A dedicated-host instance owns all the CPU, memory, storage, and I/O resources on the server where it is deployed.
 For example, **8核32GB** is the specification for a general-purpose instance, **8核32GB（独享套餐）** is the specification for a dedicated instance, and **30核220GB（独占主机）** is the specification for a dedicated-host instance.|
    |**存储空间**|Used to store data files, system files, binary log files, and transaction files.|
    |**网络类型**|     -   **经典网络**: a classic network.
    -   **专有网络** \(recommend\): A Virtual Private Cloud \(VPC\) is an isolated network that is superior to a classic network in terms of security and performance.
 |



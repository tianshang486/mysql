# Release or unsubscribe from an ApsaraDB RDS for MySQL instance

This topic describes how to manually release a pay-as-you-go ApsaraDB RDS for MySQL instance. It also describes how to manually unsubscribe from a subscription ApsaraDB RDS for MySQL instance.

## Precautions

-   After you release or unsubscribe from an RDS instance, the RDS instance and its data are immediately deleted. Before you release or unsubscribe from an RDS instance, we recommend that you back up the RDS instance and download the required backup file. For more information, see [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md) and [Download data and log backup files of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md).
-   If you want to release the last read-only RDS instance that is attached with a primary RDS instance, you must disable the read/write splitting function for the primary RDS instance. For more information, see [Disable read/write splitting for an RDS MySQL instance](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Disable read/write splitting for an RDS MySQL instance.md).

**Note:** The download of backup files is not supported for RDS instances that run MySQL 5.7 or 8.0 on RDS Basic or High-availability Edition with standard or enhanced SSDs.

## Release a pay-as-you-go RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Use one of the following methods to open the **Release Instance** message:

    -   Find your RDS instance. In the **Actions** column, click **More** and select **Release Instance** from the menu that appears.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8150359951/p11173.png)

    -   1.  Find your RDS instance and click its ID.
2.  On the **Basic Information** page, click **Release Instance**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8150359951/p3024.png)

4.  In the message that appears, click **Confirm**.


## Unsubscribe from a subscription RDS instance

If you want to unsubscribe from your RDS instance, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## FAQ

-   If I release a read-only RDS instance, will my workloads be interrupted?

    Yes, if you release a read-only RDS instance, your workloads on the read-only RDS instance will be interrupted. Before you release a read-only RDS instance, we recommend that you set the read weight of the read-only RDS instance to 0. For more information, see [Modify the latency threshold and read weights of ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Shared proxy (phased-out)/Modify the latency threshold and read weights of ApsaraDB RDS for MySQL instances.md).

    **Note:** The cached connections to the read-only RDS instance that you have released remains valid. If you want to route the read requests over the cached connections to the other read-only RDS instances, you must establish new connections.

-   After I release an RDS instance, how do I retrieve the data of the RDS instance?

    If you have specified to retain the backup files of an RDS instance after the RDS instance is released, you can go to the **Backup for Deleted Instances** page in the ApsaraDB for RDS console to restore data. For more information, see [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).


## Operations

|Operation|Description|
|---------|-----------|
|[Delete instance](/intl.en-US/API Reference/Instance management/Delete instance.md)|Releases a pay-as-you-go ApsaraDB for RDS instance. \(You cannot unsubscribe from a subscription ApsaraDB for RDS instance by calling an API operation.\)|


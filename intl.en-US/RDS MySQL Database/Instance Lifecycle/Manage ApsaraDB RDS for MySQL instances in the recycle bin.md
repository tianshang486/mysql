# Manage ApsaraDB RDS for MySQL instances in the recycle bin

This topic describes how to manage expired and overdue ApsaraDB RDS for MySQL instances in the recycle bin. You can unlock, rebuild, or destroy these instances in the recycle bin.

## Unlock an overdue RDS instance

If a pay-as-you-go-billed RDS instance is locked due to overdue payments, check the payment method of your Alibaba Cloud account in the [Billing Management console](https://billing.console.aliyun.com/?#/account/overview).

## Unlock an expired RDS instance

If a subscription-billed RDS instance is locked due to expiration, you can go to the recycle bin and renew the RDS instance.

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Unlock** to renew the RDS instance.


After the renewal is complete, the RDS instance is immediately unlocked.

## Rebuild an RDS instance

After a subscription-billed RDS instance expires, it will be retained for a specified period of time. After the specified retention period elapses, the RDS instance will be released. However, the backups of the RDS instance can still be retained for eight more days. During the eight-day retention period, you can restore the data of the RDS instance from a backup to a new RDS instance by using the instance rebuild function. For more information, see [Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md).

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Recreate Instance**.


By default, ApsaraDB for RDS creates an RDS instance with the same specifications in the same zone. You can also specify different specifications and zones for the new RDS instance.

## Destroy an RDS instance

You can destroy an expired or overdue RDS instance in the recycle bin.

**Warning:** After you destroy an RDS instance, all the backups of the RDS instance are destroyed. These include regular data backups, archived data backups, and log backups. However, these do not include cross-region backups. In addition, these do not include the backups that can be retained after the RDS instance is released. Proceed with caution. For more information, see [Back up an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md) and [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Destroy**.


## References

[Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md)


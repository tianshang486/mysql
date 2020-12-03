# Manage ApsaraDB RDS for PPAS instances in the recycle bin

This topic describes how to manage expired and overdue ApsaraDB RDS for PPAS instances in the recycle bin. You can unlockor destroy these instances in the recycle bin.

## Unlock an overdue RDS instance

If a pay-as-you-go RDS instance is locked due to overdue payments, check the billing method of your Alibaba Cloud account in the [Billing Management console](https://billing.console.aliyun.com/?#/account/overview).

## Unlock an expired RDS instance

If a subscription RDS instance is locked due to expiration, you can go to the recycle bin and renew the RDS instance.

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).
2.  In the top navigation bar, select the region where the RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Unlock**.

    The RDS instance is immediately unlocked after the renewal is complete.


## Rebuild an RDS instance

After a subscription RDS instance expires, it will be retained for a specified period of time. After the specified retention period elapses, the RDS instance will be released. However, the backups of the RDS instance can still be retained for eight more days. During the eight-day retention period, you can restore the data of the RDS instance from a backup to a new RDS instance by using the instance rebuild function. For more information, see [Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md).

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).
2.  In the top navigation bar, select the region where the RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Recreate Instance**.

    By default, the system creates an RDS instance with the same specifications in the same zone. You can also create an RDS instance with different specifications in a different zone.


## Destroy an RDS instance

If an RDS instance is locked due to overdue payments or expiration, you can destroy it in the recycle bin.

**Warning:** After you destroy an RDS instance, all of the backups are destroyed. Proceed with caution.

Procedure

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).
2.  In the top navigation bar, select the region where the RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Destroy**.

## References

[Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md)


# Manage ApsaraDB RDS for SQL Server instances in the recycle bin

This topic describes how to manage expired and overdue ApsaraDB RDS for SQL Server instances in the recycle bin. You can unlock, rebuild, or destroy these instances in the recycle bin.

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

After a subscription-billed RDS instance that runs SQL Server 2008 R2 is released due to overdue payments or expiration, its data backup files will continue to be retained for eight more days. During the eight-day retention period, you can restore the data of the RDS instance to a new RDS instance by using a data backup file. Eight days after expiration, the data backup files will also be deleted, and you can no longer retrieve the data of the RDS instance.

**Note:** You cannot rebuild RDS instances that run SQL Server 2012 or 2016.

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Recreate Instance**.


## Destroy an RDS instance

If an RDS instance is locked due to overdue payments or expiration, you can destroy it in the recycle bin.

**Warning:** After you destroy an RDS instance, all of the backup files are destroyed. Proceed with caution.

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the RDS instance and click **Destroy**.


## References

[Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md)


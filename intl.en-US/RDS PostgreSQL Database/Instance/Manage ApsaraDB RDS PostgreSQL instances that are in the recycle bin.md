# Manage ApsaraDB RDS PostgreSQL instances that are in the recycle bin

Expired or overdue ApsaraDB for RDS instances are locked in the recycle bin. You can unlock, rebuild, or destroy them in the recycle bin.

## Unlock an overdue pay-as-you-go instance

If a pay-as-you-go instance is locked due to overdue payments, check the [billing method](https://billing.console.aliyun.com/?#/account/overview) of your Alibaba Cloud account.

## Unlock an expired subscription instance

If a subscription instance is locked because it is expired, you can go to the recycle bin to renew it.

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).
2.  In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click **Unlock** to renew it.

    The target RDS instance is unlocked immediately after the renewal.


## Rebuild a subscription instance

After a subscription instance expires, it is retained for a specific period of time. After the period of time you specify elapses, the instance is released. The data backup files of the instance are retained for eight days. During the eight-day retention period, you can use the data backup files to rebuild a new instance. For more information, see [Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md).

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).
2.  In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click **Recreate Instance**.

    By default, the target RDS instance is rebuilt with the same specifications and in the same zone. You also have the option to rebuild the target RDS instance with different specifications and in a different zone.


## Destroy an instance

If an instance is locked due to expiration or overdue payments, you can destroy it in the recycle bin.

**Warning:** Destroying an instance destroys all backups. Proceed with caution.

Procedure

1.  Log on to the [recycle bin](https://rdsnext.console.aliyun.com/#/rdsList/cn-hangzhou/recyclelist/lock).
2.  In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click **Destroy**.

## Related documentation

[Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md)


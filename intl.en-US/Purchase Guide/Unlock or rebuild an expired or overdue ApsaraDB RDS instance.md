# Unlock or rebuild an expired or overdue ApsaraDB RDS instance

This topic describes how to unlock or rebuild an expired or overdue ApsaraDB RDS instance within the specified retention period.

**Warning:** If your RDS instance expires or becomes overdue, it may be stopped. You will be notified in these cases. To ensure service availability, you must immediately renew your RDS instance or top up your Alibaba Cloud account.

|Billing method|Instance status|Operation|
|--------------|---------------|---------|
|Subscription|-   If auto-renewal is enabled but the automatic renewal fails:
    -   During the first day to the fifteenth day after your RDS instance expires, the instance still runs as normal.
    -   On the sixteenth day after your RDS instance expires, the instance is stopped.
    -   On the thirty-first day after your RDS instance expires, the instance is released. However, the backups of the instance are still retained until the thirty-eighth day.
    -   On the thirty-ninth day after your RDS instance expires, the backups of the instance are released.
-   If auto-renewal is not enabled:
    -   During the first day to the fifteenth day after your RDS instance expires, the instance is stopped.
    -   On the sixteenth day after your RDS instance expires, the instance is released. However, the backups of the instance are still retained until the twenty-third day.
    -   On the twenty-fourth day after your RDS instance expires, the backups of the instance are released.

|-   Before your RDS instance is released, manually renew the instance. The instance is immediately available. For more information, see [Manually renew an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Renew/Manually renew an ApsaraDB RDS for MySQL instance.md).
-   After your RDS instance is released and before the backups are released, rebuild the instance from the recycle bin and restore the data of the instance to a new RDS instance. For more information, see [Manage ApsaraDB RDS for MySQL instances in the recycle bin](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Manage ApsaraDB RDS for MySQL instances in the recycle bin.md). The time that is required for the restoration varies based on the performance and data volume of your RDS instance.
-   After the backups are released, your RDS instance cannot be restored. |
|Pay-as-you-go|If you have an overdue payment in your Alibaba Cloud account, all of the pay-as-you-go instances under this account change to the Overdue state. -   During the first day to the fifteenth day after your RDS instance becomes overdue, the instance still runs as normal.
-   On the sixteenth day after your RDS instance becomes overdue, the instance is stopped.
-   On the thirty-first day after your RDS instance becomes overdue, the instance is released with the backups and cannot be restored.

|-   Before the backups are released, check the payment method of your Alibaba Cloud account and top up this account in the [Billing Management console](https://billing.console.aliyun.com/#/account/overview).
-   After the backups are released, your RDS instance cannot be restored. |

**Note:** If your RDS instance runs MySQL, the cross-region backups are retained after the instance is released due to expiration or overdue payments. In addition, the backups that remain within the specified retention period are also retained. For more information, see [Back up an ApsaraDB RDS for MySQL instance across regions](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance across regions.md) and [Back up an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).

## Suggestions

-   Before your subscription RDS instance expires, we recommend that you manually renew the instance or enable auto-renewal. For more information, see [Manually renew an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Renew/Manually renew an ApsaraDB RDS for MySQL instance.md) and [Enable auto-renewal for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Renew/Enable auto-renewal for an ApsaraDB RDS for MySQL instance.md).
-   Make sure that the balance in your Alibaba Cloud account is sufficient.

## FAQ

My Alibaba Cloud account has overdue payments because I have subscription RDS instances that are charged at additional fees. These fees include the fees for excess backup usage beyond the provided free quota and the fees for features such as SQL Explorer. What will happen in these cases?

In these cases, your subscription RDS instances still run as normal. However, all of the pay-as-you-go RDS instances under your Alibaba Cloud account become overdue.


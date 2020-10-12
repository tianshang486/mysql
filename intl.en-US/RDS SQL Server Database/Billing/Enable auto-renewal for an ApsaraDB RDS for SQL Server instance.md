# Enable auto-renewal for an ApsaraDB RDS for SQL Server instance

This topic describes how to enable auto-renewal for an ApsaraDB RDS for SQL Server instance. If your RDS instance uses subscription billing, you can enable auto-renewal. This relieves the need to manually renew your RDS instance. Make sure that your Alibaba Cloud account has a sufficient balance, and your RDS instance will never expire.

If your RDS instance uses the subscription billing method, subscription instances can expire. If you do not renew your RDS instance before it expires, your service is interrupted and data may be lost. For more information, see [Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md).

**Note:** RDS instances that use the pay-as-you-go billing method do not expire and therefore do not require renewal.

## Precautions

-   If you enable auto-renewal, the first time when the system deducts fees from your Alibaba Cloud account comes at 08:00:00 three days before your RDS instance expires. If the deduction fails, the system will attempt to deduct the fee every day for the next two days.

    **Note:** Make sure that the balance of your Alibaba Cloud account is sufficient. Otherwise, the renewal fails. If all the three automatic fee deduction attempts fail, you must manually renew your RDS instance in a timely manner to avoid service interruption and data loss.

-   If you manually renew your RDS instance before the automatic fee deduction, the system will automatically renew the instance next time before the expiration.
-   After you enable auto-renewal, it takes effect the next day. If your RDS instance is due to expire the next day, renew it manually to avoid service interruption. For more information, see [Manually renew an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Billing/Manually renew an ApsaraDB RDS for SQL Server instance.md).

## Enable auto-renewal when you purchase an RDS instance

**Note:** If you select auto-renewal when you purchase an RDS instance, the system automatically renews the instance based on the selected renewal cycle. The renewal cycle is one month or one year. For example, if you select auto-renewal when you purchase a six-month RDS instance, the system automatically renews the instance for one month each time the instance is due to expire.

When you purchase a subscription RDS instance, select **Auto-Renew Enabled**.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p11146.png)

## Enable auto-renewal after you purchase an RDS instance

**Note:** After you enable auto-renewal, the system automatically renews the subscription based on the selected renewal cycle. For example, if you select a three-month renewal cycle, you are charged for a three-month subscription in each renewal cycle.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

    ![Renew](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  Click the Manual or Nonrenewal tab. Specify the filter conditions to find the target instance. You can enable auto-renewal for a single or multiple instances at a time.
    -   Enable auto-renewal for a single instance.
        1.  Find the target instance and click **Enable Auto Renewal** in the Actions column.

            ![Enable auto-renewal for a single instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48534.png)

        2.  In the dialog box that appears, select a value for **Unified Auto Renewal Cycle** and click **Auto Renew**.

            ![Settings for enabling auto-renewal for a single instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48535.png)

    -   Enable auto-renewal for multiple instances.

        Select multiple instances and click **Enable Auto Renewal**.

        ![Enable auto-renewal for multiple instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48536.png)

    -   In the dialog box that appears, select a value for **Unified Auto Renewal Cycle** and click **Auto Renew**.

        ![Settings for enabling auto-renewal for multiple instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48537.png)


## Change the auto-renewal cycle

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

    ![Renew](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  Click the Auto tab. Specify the filter conditions to find the target instance. Click **Edit Auto Renewal** in the Actions column.

    ![Modify auto-renewal](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7940359951/p48538.png)

4.  In the dialog box that appears, change the auto-renewal cycle and click **OK**.

## Disable auto-renewal

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

    ![Renew](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  Click the Auto tab. Specify the filter conditions to find the target instance. Click **Enable Manual Renewal** in the Actions column.

    ![Disable auto-renewal](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7940359951/p48539.png)

4.  In the message that appears, click **OK**.

## Related operations

|Operation|Description|
|:--------|:----------|
|[Create instance](/intl.en-US/API Reference/Instance management/Create instance.md)|Creates an RDS instance. **Note:** Enable auto-renewal when you create an RDS instance. |
|[t8084.md\#](/intl.en-US/API Reference/Billing/Manual renewal.md)|Renews an RDS instance. **Note:** Enable auto-renewal after you create an RDS instance. |


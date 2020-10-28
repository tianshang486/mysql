# Enable auto-renewal for an ApsaraDB RDS for MySQL instance

This topic describes how to enable auto-renewal for an ApsaraDB RDS for MySQL instance that uses the subscription billing method. If you enable auto-renewal for your RDS instance, you do not need to manually renew your subscription or be concerned about service interruptions caused by subscription expiration.

If do not renew your RDS instance before the expiration date, your RDS instance expires. As a result, your workloads are interrupted and your data may be lost. For more information, see [Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md).

**Note:** RDS instances that use the pay-as-you-go billing method do not expire and therefore do not require renewal.

## Precautions

-   If you enable auto-renewal, the first time when the system deducts the subscription fee from your Alibaba Cloud account comes at 08:00:00 three days before the expiration date. If the deduction fails, the system attempts to deduct the fee every day for the next two days.

    **Note:** Make sure that the balance of your Alibaba Cloud account is sufficient. Otherwise, the renewal fails. If all the three automatic fee deduction attempts fail, you must manually renew your RDS instance before the expiration date. This allows you to avoid service interruptions and data losses.

-   If you manually renew your RDS instance before the system starts automatic fee deduction attempts, the system will automatically renew the instance next time before the expiration date.
-   After you enable auto-renewal, it takes effect the next day. If your RDS instance is due to expire the next day, renew it manually to avoid service interruptions. For more information, see [Manually renew an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Instance Lifecycle/Renew/Manually renew an ApsaraDB RDS for MySQL instance.md).

## Enable auto-renewal when you purchase an RDS instance

**Note:** If you select auto-renewal when you purchase an RDS instance, the system automatically renews the RDS instance based on the specified renewal cycle. The renewal cycle is one month or one year. For example, if you select auto-renewal when you purchase an RDS instance with a six-month subscription, the system automatically renews the RDS instance with a one-month subscription each time the instance is due to expire.

When you purchase a subscription RDS instance, select **Auto-Renew Enabled**.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p11146.png)

## Enable auto-renewal after you purchase an RDS instance

**Note:** After you enable auto-renewal for a created RDS instance, the system automatically renews the RDS instance based on the selected renewal cycle. For example, if you select a three-month renewal cycle, you are charged for a three-month subscription in each renewal cycle.

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

    ![Renew](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  On the Manual or Nonrenewal tab, specify the filter conditions to find the RDS instance for which you want to enable auto-renewal. You can enable auto-renewal for one or more RDS instances at a time.
    -   Enable auto-renewal for a single RDS instance.
        1.  Find the RDS instance and in the Actions column click **Enable Auto Renewal**.

            ![Enable auto-renewal for a single RDS instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48534.png)

        2.  In the dialog box that appears, specify the **Unified Auto Renewal Cycle** parameter and click **Auto Renew**.

            ![Enable auto-renewal for a single RDS instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48535.png)

    -   Enable auto-renewal for multiple RDS instances.

        Select the RDS instances and click **Enable Auto Renewal** below the instance list.

        ![Enable auto-renewal for multiple RDS instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48536.png)

    -   In the dialog box that appears, specify the **Unified Auto Renewal Cycle** parameter and click **Auto Renew**.

        ![Enable auto-renewal for multiple RDS instances](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940359951/p48537.png)


## Change the auto-renewal cycle

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

    ![Renew](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  On the Auto tab, specify filter conditions to find the RDS instance for which you want to enable auto-renewal. Then, select the RDS instance and click **Edit Auto Renewal** in the Actions column.

    ![Change the auto-renewal cycle](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7940359951/p48538.png)

4.  In the dialog box that appears, change the auto-renewal cycle and click **OK**.

## Disable auto-renewal

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, choose **Expenses** \> **Renewal Management**.

    ![Renew](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  On the Auto tab, specify filter conditions to find the RDS instance for which you want to enable auto-renewal. Then, select the RDS instance and click **Enable Manual Renewal** in the Actions column.

    ![Disable auto-renewal](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7940359951/p48539.png)

4.  In the message that appears, click **OK**.

## Related operations

|Operation|Description|
|:--------|:----------|
|[Create instance](/intl.en-US/API Reference/Instance management/Create instance.md)|Creates an ApsaraDB RDS instance. **Note:** You can call this operation to enable auto-renewal for an RDS instance that you want to create. |
|[Manually renew an ApsaraDB for RDS instance](/intl.en-US/API Reference/Billing/Manually renew an ApsaraDB for RDS instance.md)|Renews an ApsaraDB RDS instance. **Note:** You can call this operation to enable auto-renewal for a created RDS instance. |


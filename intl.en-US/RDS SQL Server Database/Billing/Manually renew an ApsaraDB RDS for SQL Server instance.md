# Manually renew an ApsaraDB RDS for SQL Server instance

This topic describes how to manually renew an ApsaraDB RDS for SQL Server instance. If your RDS instance uses subscription billing, you must renew it before it expires. This allows you to prevent service interruptions and data loss.

For more information about the impacts caused by subscription expiration, see [Unlock or rebuild an expired or overdue ApsaraDB for RDS instance](/intl.en-US/Purchase Guide/Unlock or rebuild an expired or overdue ApsaraDB for RDS instance.md).

**Note:** RDS instances that use the pay-as-you-go billing method do not expire and therefore do not require renewal.

You can manually renew your RDS instance before it expires or within 15 days after it expires.

## Method 1: Renew an RDS instance in the RDS console

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the target region.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2150359951/p48527.png)

3.  Find the target RDS instance and in the **Actions** column click **Renew**.
4.  On the Renew Subscription page, select a duration. The longer the duration, the bigger discount you have.

    ![选择续费时长](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p11150.png)

5.  Read and confirm you agree to **Terms of Service, Service Level Agreement, and Terms of Use** by selecting the checkbox, confirm the order details, and click **Pay Now**

## Renew an RDS instance in the Renew console

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-right corner of the page, choose **Billing Management** \> **Renew**.

    ![Renewal console](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3150359951/p48528.png)

3.  On the Manual tab, you can search for the instance to manually renew it. You can manually renew a single instance or multiple instances at a time.
    -   Renew a single instance
        1.  Find the instance and click **Renew**.

**Note:**

-   The preceding figure shows the procedure of disabling auto-renewal for the RDS instance in the new renewal console. If you are using the old console, you must select **ApsaraDB for RDS** in the left-side navigation pane, and then disable the auto-renewal feature.
-   If the instance that you want to manually renew is in the Auto or Nonrenewal tab, click **Enable Manual Renewal**. In the message box that appears, click **OK**.
        2.  Select a renewal duration, select the Terms of Service option, and click **Pay Now** to complete the renewal.
    -   Renew multiple instances
        1.  Select multiple instances that you want to manually renew, and click **Bulk Renewal**.

        2.  Select a **renewal duration**, click **Pay Now** to complete the payment.

## Enable auto-renewal

If you enable auto-renewal for your RDS instance, you do not need to manually renew your RDS instance. If your Alibaba Cloud account has a sufficient balance, your RDS instance never expires. For more information, see [Automatically renew the subscription of an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Billing/Automatically renew an RDS SQL Server instance.md).


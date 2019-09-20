# Switch from pay-as-you-go billing to subscription billing {#concept_gtz_lbj_wdb .concept}

This topic describes how to change the billing method of an RDS for MySQL instance from pay-as-you-go to \(monthly or annual\) subscription.

## Impacts {#section_abl_gc4_z2b .section}

Changing the billing method does not interrupt the running of your RDS instance.

## Precautions {#section_ljb_pbj_wdb .section}

-   A read-only RDS instance is charged only by the pay-as-you-go billing method.
-   You cannot change the billing method of an RDS instance from subscription to pay-as-you-go. To optimize your cost plan, you must evaluate your usage model thoroughly before you change the billing method of your RDS instance.
-   If an RDS instance has an unpaid subscription order, the subscription order becomes invalid after you upgrade the instance type. In such case, you must first go to the [Orders](https://expense.console.aliyun.com/#/order/list/) page in the RDS console to cancel the subscription order, and then change the billing method to subscription again.

## Prerequisites {#section_egl_rbj_wdb .section}

-   The instance type cannot be a historical one, which means that the instance type must be available for sale. For more information about historical instance types, see [Instance types](../intl.en-US/Product Introduction/Instance types/Instance types.md#). Before you change the billing method of a historical-type RDS instance to subscription, you must change the instance type to one that is available for sale. For detailed steps, see [Change the configuration of an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Instance management/Change the configuration of an RDS for MySQL instance.md#).
-   The RDS instance uses the pay-as-you-go billing method.
-   The RDS instance is in the **Running** state.
-   The RDS instance does not have an unpaid subscription order.

## Procedure {#section_hv1_5bj_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![Select a region.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156896120436543_en-US.png)

3.  Find the target RDS instance and use one of the following two methods to open the Switch to Subscription Billing page.
    -   In the **Actions** column, click **Subscription Billing**.
    -   Click the instance ID. Then in the **Status** section of the Basic Information page, click **Subscription Billing**.

        ![转包年包月](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/15689612043011_en-US.png)

4.  Select a duration of purchase.
5.  Select **Terms of Service, Service Level Agreement, and Terms of Use**. Then click **Pay Now**.

    **Note:** The system generates a subscription order. If this order is not paid or canceled, you cannot change the billing method of this RDS instance from pay-as-you-go to subscription or purchase a new RDS instance. You can go to the [Orders](https://expense.console.aliyun.com/#/order/list/) page to pay for or cancel this order.

6.  Complete the payment.


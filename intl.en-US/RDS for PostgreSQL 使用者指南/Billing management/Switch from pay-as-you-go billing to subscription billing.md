# Switch from pay-as-you-go billing to subscription billing {#concept_gtz_lbj_wdb .concept}

This topic describes how to change the billing method of an RDS for PPAS instance from pay-as-you-go to \(monthly or annual\) subscription.

## Impact {#section_abl_gc4_z2b .section}

Changing billing methods does not impact the performance of your ApsaraDB RDS for PostgreSQL instances.

## Notes {#section_ljb_pbj_wdb .section}

-   You cannot change the billing method from subscription to pay-as-you-go. To optimize your cost plan, evaluate your usage model carefully before you change your billing method.
-   You cannot upgrade the specifications of a subscription-based instance if the purchase order of the instance has not been paid. Otherwise, the unpaid order will be invalid. You need to cancel this order on the [Orders](https://expense.console.aliyun.com/#/order/list/) page and change the billing method again.

## Prerequisites {#section_egl_rbj_wdb .section}

-   The instance type cannot be an end-of-sales \(EOS\) instance types that are no longer available for sale. For more information about the EOS instance types, see [End-of-sales instance types](../intl.en-US/Product Introduction/Instance types/Instance types.md#section_bpx_khx_5db). You need to change the instance type from EOS instance type to an available instance type before you change the billing method for the instance to subscription. For more information, see [Change the specifications](intl.en-US/RDS for PostgreSQL 使用者指南/Instance management/Change the specifications.md#).
-   The billing method of the instance is pay-as-you-go.
-   The instance is in the **running** state.
-   You do not have an unpaid order of subscription-based instance.

## Procedure {#section_hv1_5bj_wdb .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com).
2.  In the upper-left corner of the page, select the region of the instance.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156888308836543_en-US.png)

3.  Locate the instance that you want to change the billing method. You can use either of the following methods to enter the Switch to Subscription Billing page.
    -   Click **Subscription Billing** in the Actions column of the instance.
    -   Click the instance ID to open the Details page. In the Status section, click **Subscription Billing**, as shown in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/15688830893011_en-US.png)

4.  Select the duration of the subscription.
5.  Click **Pay Now**.

    **Note:** The system will generate an order for you to switch to the subscription billing method. If this order is not paid or canceled, you cannot purchase new instances or switch billing method of the instance to subscription. You can **pay for** or **cancel** this order on the [Orders](https://expense.console.aliyun.com/#/order/list/) page.

6.  Pay the order as prompted.


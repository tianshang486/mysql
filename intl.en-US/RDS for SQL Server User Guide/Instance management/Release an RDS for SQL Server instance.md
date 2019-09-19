# Release an RDS for SQL Server instance {#concept_r1p_jgj_wdb .concept}

This topic describes how to release an RDS for SQL Server instance, which can use the pay-as-you-go or subscription billing method.

**Note:** After an RDS instance is released, its data is deleted immediately. We recommend that you back up the instance data before you release the instance.

## Release a pay-as-you-go-based RDS instance {#section_ojf_5f8_1k8 .section}

**Precautions**

If the RDS instance you want to release is the last read-only instance of a master instance, you must [disable the cluster management function](intl.en-US/RDS for SQL Server User Guide/SQL Server read__write splitting/Disable cluster management for an RDS for SQL Server instance.md#) of the master instance before releasing the last read-only instance.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156888717436543_en-US.png)

3.  Use one of the following two methods to open the Release Instance dialog box:
    -   Method 1:

        Find the target RDS instance and in the **Actions** column choose **More** \> **Release Instance**.

        ![释放实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7887/156888717411173_en-US.png)

    -   Method 2:
        1.  Find the target RDS instance and click the instance ID.
        2.  On the Basic Information page, find the **Status** section and click **Release Instance**.

            ![释放实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7887/15688871743024_en-US.png)

4.  In the Release Instance dialog box, click **Confirm**.

## Release a subscription-based RDS instance {#section_f7s_k3w_o0k .section}

You can [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to apply for releasing a subscription-based RDS instance.

## APIs {#section_kqf_sck_3yf .section}

|API|Description|
|---|-----------|
|[DeleteDBInstance](../intl.en-US/API Reference/Instance management/DeleteDBInstance.md#)|Used to release a pay-as-you-go-based RDS instance. \(A subscription-based RDS instance cannot be released by calling an API action.\)|


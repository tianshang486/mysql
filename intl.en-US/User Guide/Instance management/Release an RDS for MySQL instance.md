# Release an RDS for MySQL instance {#concept_r1p_jgj_wdb .concept}

As your business needs change, you can manually release a Pay-As-You-Go instance.

## Prerequisites {#section_xjf_ngj_wdb .section}

-   The instance is a Subscription instance. Subscription instances are released automatically when they are overdue.
-   The instance is in the **Running** state.
-   If the instance is the only read-only instance attached to a master instance for which the read/write splitting function is enabled, make sure that the read/write splitting function is disabled. For more information, see [Disable read/write splitting](intl.en-US/User Guide/Read__write splitting/Disable read__write splitting.md#).

## Method 1 {#section_f51_pnd_m28 .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156592452937169_en-US.png)

3.  Find the target RDS instance and in the **Actions** column choose **More** \> **Release Instance**.

    ![释放实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7887/156592452911173_en-US.png)

4.  In the displayed dialog box, click **Confirm**.

## Method 2 {#section_dsk_4gj_wdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156592452937169_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  On the Basic Information page, find the **Status** section and click **Release Instance**.

    ![释放实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7887/15659245303024_en-US.png)

5.  In the displayed dialog box, click **Confirm**


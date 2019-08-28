# Configure a whitelist {#concept_sfx_kdg_wdb .concept}

After an RDS instance is created, you must configure a whitelist so that external devices can access the RDS instance. The default whitelist is an IP address whitelist that contains only the default IP address **127.0.0.1**. This default IP address means that no devices can access the RDS instance.

To configure a whitelist, follow these steps:

-   Configure an IP address whitelist: Add IP addresses to a whitelist so that these IP addresses can access the RDS instance.
-   Configure a VPC security group whitelist: Add a VPC security group to a whitelist so that all ECS instances in the VPC security group can access the RDS instance.

    **Note:** You can configure VPC security groups only in PostgreSQL 10 High-availability Edition \(with local SSDs\), PostgreSQL 10 Basic Edition, and PostgreSQL 9.4


We recommend that you periodically check and adjust your whitelists to maintain RDS security. Configuring a whitelist does not affect the normal running of the RDS instance.

## PostgreSQL 11 High-availability Edition \(with SSDs\) or PostgreSQL 10 High-availability Edition \(with SSDs\) {#section_ndi_q87_zg2 .section}

**Precautions**

-   The default IP address whitelist can be modified or cleared but cannot be deleted.
-   Up to 1,000 IP addresses or CIDR blocks can be added to each IP address whitelist. If you want to add a large number of IP addresses, we recommend that you merge them into CIDR blocks, for example, **192.168.1.0/24**.

**Procedure**

1.  Log on to the [PostgreSQL console](https://postgresql.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156698652449667_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, choose **Data Security** \> **Whitelist Configuration**.
5.  On the displayed page, find the whitelist named **default** and in the **Actions** column choose **⋮** \> **Edit**.

    **Note:** You can also click **Create Whitelist** to create a whitelist.

    ![编辑白名单-点击编辑按钮](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7848/156698652449689_en-US.png)

6.  In the Edit Whitelist dialog box, enter IP addresses or CIDR blocks and click **OK**. Detailed rules are as follows:

    -   If you enter a CIDR block, for example, **10.10.10.0/24**, then any IP addresses in 10.10.10.X format can access the RDS instance.
    -   If you want to enter more than one IP address or CIDR block, you must separate them by using commas \(,\) and leave no spaces preceding or following the commas, for example, **192.168.0.1,172.16.213.9**.
    -   If you select **Load Internal IP** for **Creation Method**, then you can select an IP address from the **Load Internal IP** drop-down list.
    **Note:** After you add IP addresses or CIDR blocks to the **default** whitelist, the system automatically deletes the default IP address **127.0.0.1**.

    ![创建白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7848/156698652449771_en-US.png)


## PostgreSQL 10 High-availability Edition \(with local SSDs\), PostgreSQL 10 Basic Edition, or PostgreSQL 9.4 {#section_wyv_ws4_ydb .section}

**Precautions**

-   The default IP address whitelist can be modified or cleared but cannot be deleted.
-   Up to 1,000 IP addresses or CIDR blocks can be added to each IP address whitelist. If you want to add a large number of IP addresses, we recommend that you merge them into CIDR blocks, for example, **192.168.1.0/24**.
-   If you attempt to connect the RDS instance to DMS without adding the IP address of DMS to a whitelist of the RDS instance, the system displays a message, stating that you can connect to DMS only after you add the IP address of DMS to a whitelist of the RDS instance.
-   Before configuring a whitelist, you must confirm which network isolation mode the RDS instance works in. Then you can decide which operations you must take accordingly.

![白名单设置-1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156698652435435_en-US.png)

![白名单设置-2](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156698652535436_en-US.png)

**Configure an enhanced whitelist**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156698652449667_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab, select the whitelist you want to modify. Detailed steps are as follows:

    -   If you want to connect the RDS instance to an ECS instance that is located in a VPC, click **Edit** in the default VPC whitelist.
    -   If you want to connect the RDS instance to an ECS instance that is located in a classic network, click **Edit** in the default Classic Network whitelist.
    -   If you want to connect the RDS instance to a server or host that is located outside the Alibaba Cloud, click **Edit** in the default Classic Network whitelist.
    **Note:** 

    -   If you want to connect the RDS instance to an ECS instance through a private IP address \(on a VPC or classic network\), make sure that the RDS instance and ECS instance have the same network type. If their network types are different, they cannot communicate. For more information, see [Set network type](../intl.en-US/User Guide/Instance management/Set network type.md#).
    -   You can also click **Create Whitelist** to create a whitelist. In the displayed dialog box, you can select the **VPC** or **Classic Network/Public IP** network type.
    ![默认经典网络白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156698652535445_en-US.png)

6.  In the displayed dialog box, enter IP addresses or CIDR blocks and click **OK**. Detailed rules are as follows,

    -   If you enter a CIDR block, for example, **10.10.10.0/24**, then any IP addresses in 10.10.10.X format can access the RDS instance.
    -   If you want to enter more than one IP address or CIDR block, you must separate them by using commas \(,\) and leave no spaces preceding or following the commas, for example, **192.168.0.1,172.16.213.9**.
    -   If you click **Add Internal IP Addresses of ECS Instances**, then the IP addresses of all ECS instances under your Alibaba Cloud account are displayed in the **Whitelist** field.
    **Note:** After you add IP addresses or CIDR blocks to the **default** whitelist, the system automatically deletes the default IP address 127.0.0.1.

    ![编辑白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15669865251795_en-US.png)


**Configure a standard whitelist**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156698652449667_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab, click **Edit** in the **default** whitelist.

    **Note:** You can also click **Create Whitelist** to create a whitelist.

    ![编辑白名单-编辑按钮](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15669865251794_en-US.png)

6.  In the Edit Whitelist dialog box, enter IP addresses or CIDR blocks and click **OK**. Detailed rules are as follows,

    -   If you enter a CIDR block, for example, **10.10.10.0/24**, then any IP addresses in 10.10.10.X format can access the RDS instance.
    -   If you want to enter more than one IP address or CIDR block, you must separate them by using commas \(,\) and leave no spaces preceding or following the commas, for example, **192.168.0.1,172.16.213.9**.
    -   If you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all ECS instances under your Alibaba Cloud account are displayed in the **Whitelist** field.
    **Note:** After you add IP addresses or CIDR blocks to the **default** whitelist, the system automatically deletes the default IP address **127.0.0.1**.

    ![编辑白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15669865251795_en-US.png)


## Common configuration errors {#section_yfw_d16_fm2 .section}

-   The whitelist contains only the default IP address **127.0.0.1**. The IP address **127.0.0.1** indicates that no devices are allowed to access the RDS instance. Therefore, you must add the IP addresses of the devices to be connected to the RDS instance to the whitelist.
-   The IP addresses you add to the whitelist are in 0.0.0.0 format, but the correct format is 0.0.0.0/0.

    **Note:** The entry **0.0.0.0/0** indicates that all devices can access the RDS instance.

-   [The enhanced whitelist mode](../intl.en-US/User Guide/Security/Switch the IP whitelist to enhanced security mode.md#) is enabled for the RDS instance, and the IP addresses are added to an inappropriate whitelist. When you add IP addresses:
    -   If you want the ECS instance to communicate with the RDS instance through a private endpoint in a VPC, make sure that the private IP address of the ECS instance is added to the **default VPC** whitelist.
    -   If you want the ECS instance to communicate with the RDS instance through a private endpoint in a classic network, make sure that the private IP address of the ECS instance is added to the **default Classic Network** whitelist.
    -   If you use [ClassicLink](https://www.alibabacloud.com/help/zh/doc-detail/65412.htm) to access the private endpoint of the RDS instance, make sure that the private IP address of the ECS instance is added to the **default VPC** whitelist.
    -   If you want the ECS instance to communicate with the RDS instance through the Internet, make sure that the public IP address of the ECS instance is added to the **default Classic Network** whitelist. The default VPC whitelist cannot be used for communication through the Internet.
-   The public IP address you added to a whitelist are invalid. This may occur if the public IP address you added is not the real outbound IP address. Possible reasons are as follows:

    -   The public IP address dynamically changes.
    -   The IP address query tool or website yields inaccurate results.
    For more information, see [How do I locate the IP address connected to an RDS for PostgreSQL or RDS for PPAS instance?](../intl.en-US/FAQs/How to connect__cannot connect/How do I locate the IP address connected to an RDS for PostgreSQL or RDS for PPAS instance?.md#).


## Configure a VPC security group {#section_dsr_nt4_ydb .section}

A VPC security group is a virtual firewall that is used to set network access control for one or more ECS instances. After a VPC security group is added to a whitelist for the RDS instance, all ECS instances in the VPC security group can access the RDS instance.

For more information, see [Create a security group](https://www.alibabacloud.com/help/doc-detail/25468.htm).

**Precautions**

-   The DB versions and editions that support VPC security groups are PostgreSQL 10 High-availability Edition \(with local SSDs\), PostgreSQL 10 Basic Edition, and PostgreSQL 9.4.
-   The regions that support VPC security groups are China \(Hangzhou\), China \(Qingdao\), and China \(Hong Kong\).
-   You can have one VPC security group whitelist and multiple IP address whitelists. All IP addresses in the IP address whitelists and all ECS instances in the VPC security group whitelist can access the RDS instance.
-   One RDS instance supports only one VPC security group whitelist.
-   After you update the VPC security group whitelist, the new VPC security group whitelist takes effect immediately.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7846/156698652449667_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab, click **Add Security Group**.

    **Note:** An ECS security group with a VPC tag is located in a VPC.

6.  Select an ECS security group and click **OK**.

## APIs {#section_kmf_bcb_kgb .section}

|API|Description|
|---|-----------|
|[DescribeDBInstanceIPArrayList](../intl.en-US/API Reference/Security management/DescribeDBInstanceIPArrayList.md#)|Used to view the IP address whitelists of an RDS instance.|
|[ModifySecurityIps](../intl.en-US/API Reference/Security management/ModifySecurityIps.md#)|Used to modify the IP address whitelists of an RDS instance.|


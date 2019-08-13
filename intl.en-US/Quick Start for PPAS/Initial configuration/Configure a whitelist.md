# Configure a whitelist {#concept_lwb_qqg_wdb .concept}

After you create an RDS instance, you must configure a whitelist to allow external devices to access the instance. The default whitelist contains only 127.0.0.1. Before you add new IP addresses to the whitelist, no devices are allowed to access the RDS instance.

A whitelist can be used to improve the security of your RDS instance. We recommend that you update the whitelist on a regular basis. Configuring a whitelist does not affect the normal operation of your RDS instance.

## Precautions {#section_bjz_gfy_ggb .section}

-   The default whitelist can only be edited or cleared, but cannot be deleted.
-   If you log on to DMS but your IP address has not been added to the whitelist, DMS will prompt you to add the address, and will automatically generate a whitelist containing your IP address.
-   You must confirm which **network isolation mode** the instance is in before configuring a whitelist. Refer to the corresponding operations based on the network isolation mode.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567815435435_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567815435436_en-US.png)

**Note:** The internal networks to which RDS instances belong are divided into two types: **classic network** and **VPC**.

-   Classic network: Alibaba Cloud allocates IP addresses automatically. Users only need to perform simple configurations. This network type is suitable for new users.
-   VPC: Users customize the network topology and IP addresses. It supports leased line connection, and is suitable for advanced users.

## Procedure {#section_wyv_ws4_ydb .section}

**Enhanced whitelist**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567815536543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, follow the following instructions based on your usage scenario:

    -   Accessing an RDS instance from an ECS located in a VPC: Click **Edit** next to the default VPC whitelist.
    -   Accessing an RDS instance from an ECS located in a classic network: Click **Edit** next to the default Classic Network whitelist.
    -   Accessing an RDS instance from an ECS or host located in a public network: Click **Edit** next to the default Classic Network whitelist.
    **Note:** 

    -   If the ECS instance accesses the RDS instance by using the VPC or classic network, you must make sure that the two instances are in the same region and have the same [network type](../intl.en-US/User Guide/Instance management/Set network type.md#). Otherwise, the connection fails.
    -   You can also click **Create Whitelist**. In the displayed Create Whitelist dialog box, select **VPC** or **Classic Network/Public IP**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567815535445_en-US.png)

6.  Specify IP addresses or CIDR blocks used to access the instance, and then click **OK**.

    -   If you specify the CIDR block 10.10.10.0/24, any IP addresses in the 10.10.10.X format are allowed to access the RDS instance.
    -   To add multiple IP addresses or CIDR blocks, separate each entry with a comma \(without spaces\), for example, 192.168.0.1,172.16.213.9.
    -   After you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all the ECS instances under your Alibaba Cloud account are displayed. You can quickly add internal IP addresses to the whitelist.
    **Note:** After you add an IP address or CIDR block to the **default** whitelist, the default address 127.0.0.1 is automatically deleted.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656781551795_en-US.png)


**Standard whitelist**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567815536543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, click **Edit** corresponding to the **default** whitelist.

    **Note:** You can also click **Create Whitelist** to configure a whitelist.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656781561794_en-US.png)

6.  In the displayed Edit Whitelist dialog box, specify the IP addresses or CIDR blocks used to access the instance, and then click **OK**.

    -   If you specify the CIDR block 10.10.10.0/24, any IP addresses in the 10.10.10.X format are allowed to access the RDS instance.
    -   To add multiple IP addresses or CIDR blocks, separate each entry with a comma \(without spaces\), for example, 192.168.0.1,172.16.213.9.
    -   After you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all the ECS instances under your Alibaba Cloud account are displayed. You can quickly add internal IP addresses to the whitelist.
    **Note:** After you add an IP address or CIDR block to the **default** whitelist, the default address 127.0.0.1 is automatically deleted.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656781551795_en-US.png)


**Common errors**

-   The default address 127.0.0.1 in the **Whitelist Settings** tab indicates that no device is allowed to access the RDS instance. Therefore, you need to add IP addresses of devices to the whitelist to allow access to the instance.
-   The IP address in the whitelist is set to 0.0.0.0, but the correct format is 0.0.0.0/0.

    **Note:** 0.0.0.0/0 indicates that all devices are allowed to access the RDS instance. Exercise caution when using this IP address.

-   If you turn on the [enhanced whitelist](../intl.en-US/User Guide/Security/Switch the IP whitelist to enhanced security mode.md#) mode, you must make sure that:
    -   If the network type is VPC, the internal IP address of the ECS instance is added to the whitelist whose network isolation mode is VPC.
    -   If the network type is classic network, the internal IP address of the ECS instance is added to the whitelist whose network isolation mode is classic network.
    -   If you are connecting to the RDS instance through [ClassicLink](https://www.alibabacloud.com/help/zh/doc-detail/65412.htm), the internal IP address of the ECS instance must be added to the **default VPC** whitelist.
    -   If you are connecting to the RDS instance through a public network, the public IP address of the instance or host must be added to the whitelist whose network isolation mode is classic network.
-   The public IP address that you add to the whitelist may not be the real egress IP address. The reasons are as follows:

    -   The public IP address is not fixed and may dynamically change.

    -   The tools or websites used to query the public IP addresses provide wrong IP addresses.

    For more information, see [How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?](../intl.en-US/FAQs/How to connect__cannot connect/How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?.md#).


## APIs {#section_hcn_555_jgb .section}

|API|Description|
|---|-----------|
|[DescribeDBInstanceIPArrayList](../intl.en-US/API Reference/Security management/DescribeDBInstanceIPArrayList.md#)|Used to view the IP address whitelist of an RDS instance.|
|[ModifySecurityIps](../intl.en-US/API Reference/Security management/ModifySecurityIps.md#)|Used to modify the IP address whitelist of an RDS instance.|


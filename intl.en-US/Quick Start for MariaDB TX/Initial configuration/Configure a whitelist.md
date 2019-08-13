# Configure a whitelist {#concept_pdr_k2f_vdb .concept}

After you create an RDS instance, you must configure a whitelist to allow external devices to access the instance. The default whitelist contains only 127.0.0.1. Before you add new IP addresses to the whitelist, no devices are allowed to access the RDS instance.

To configure a whitelist, you can perform the following operations:

-   Configure a whitelist: Add IP addresses to the whitelist to allow access to the RDS instance.
-   Configure an ECS security group: Add an ECS security group for the RDS instance to allow ECS instances in the group to access the RDS instance.

A whitelist can be used to improve the security of your RDS instance. We recommend that you update the whitelist on a regular basis. Configuring a whitelist does not affect the normal operation of your RDS instance.

## Configure an IP address whitelist {#section_byp_zif_mc2 .section}

**Precautions**

-   The default IP whitelist can only be edited or cleared, but cannot be deleted.
-   You must confirm which **network isolation mode** your RDS instance is in before configuring the whitelist. Refer to the corresponding operations based on the network isolation mode.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567880435435_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567880535436_en-US.png)

    **Note:** The intranet where an RDS for MariaDB instance is located must be a VPC.


**Configure an enhanced whitelist**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567880536543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, follow these instructions based on your usage scenario:

    -   Accessing an RDS instance from an ECS instance located within a VPC: Click **Edit** next to the default VPC whitelist.
    -   Accessing an RDS instance from an ECS instance located within a classic network: RDS for MariaDB TX instances do not support classic networks. Therefore, you can apply for an Internet IP address for your RDS for MariaDB TX instance and then use the Internet IP address to connect to your RDS for MariaDB TX instance.
    -   Accessing an RDS instance from an instance or host located in a public network: Click **Edit** next to the default Classic Network whitelist.
    **Note:** 

    -   If the ECS instance accesses the RDS instance by using the VPC, you must make sure that the two instances are in the same region and have the same [network type](../intl.en-US/User Guide/Instance management/Set network type.md#). Otherwise, the connection fails.
    -   You can also click **Create Whitelist**. In the displayed Create Whitelist dialog box, select a network type, **VPC** or **Classic Network/Public IP**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567880535445_en-US.png)

6.  In the displayed Edit Whitelist dialog box, specify IP addresses or CIDR blocks used to access the instance, and then click **OK**.

    -   If you specify the CIDR block 10.10.10.0/24, any IP addresses in the 10.10.10.X format are allowed to access the RDS instance.
    -   To add multiple IP addresses or CIDR blocks, separate each entry with a comma \(without spaces\), for example, 192.168.0.1,172.16.213.9.
    -   After you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all the ECS instances under your Alibaba Cloud account are displayed. You can quickly add internal IP addresses to the whitelist.
    **Note:** After you add an IP address or CIDR block to the **default** whitelist, the default address 127.0.0.1 is automatically deleted.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656788051795_en-US.png)


**Configure a standard whitelist**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567880536543_en-US.png)

3.  Find the target instance and click its ID。
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, click **Edit** corresponding to the **default** whitelist.

    **Note:** You can also click **Create Whitelist** to create a whitelist.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656788061794_en-US.png)

6.  In the displayed Edit Whitelist dialog box, specify the IP addresses or CIDR blocks used to access the instance, and then click **OK**.

    -   If you specify the CIDR block 10.10.10.0/24, any IP addresses in the 10.10.10.X format are allowed to access the RDS instance.
    -   To add multiple IP addresses or CIDR blocks, separate each entry with a comma \(without spaces\), for example, 192.168.0.1,172.16.213.9.
    -   After you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all the ECS instances under your Alibaba Cloud account are displayed. You can select the internal IP addresses to add to the whitelist.
    **Note:** After you add a new IP address or CIDR block to the **default** whitelist, the default address 127.0.0.1 is automatically deleted.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656788051795_en-US.png)


**Common errors**

-   The default address 127.0.0.1 in **Data Security** \> **Whitelist Settings** indicates that no device is allowed to access the RDS instance. Therefore, you need to add IP addresses of devices to the whitelist to allow access to the instance.
-   The IP address in the whitelist is set to 0.0.0.0, but the correct format is 0.0.0.0/0.

    **Note:** 0.0.0.0/0 indicates that all devices are allowed to access the RDS instance. Exercise caution when using this IP address.

-   If you enable the [enhanced whitelist](../intl.en-US/User Guide/Security/Switch the IP whitelist to enhanced security mode.md#) mode, you must make sure that:
    -   If the network type is **VPC**, the internal IP address of the ECS instance is added to the whitelist whose network isolation mode is **default VPC**.
    -   If you are connecting to the RDS instance through [ClassicLink](https://www.alibabacloud.com/help/zh/doc-detail/65412.htm), the internal IP address of the ECS instance must be added to the **default VPC** whitelist.
    -   If you are connecting to the RDS instance through a public network, the public IP address of the device must be added to the whitelist whose network isolation mode is **default Classic Network** .
-   The Internet IP address that you add to the whitelist may not be the real egress IP address. The reasons are as follows:

    -   The Internet IP address is not fixed and may dynamically change.
    -   The tools or websites used to query the Internet IP addresses provide wrong IP addresses.
    For more information, see [How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?](../intl.en-US/FAQs/How to connect__cannot connect/How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?.md#)


## Configure an ECS security group {#section_75x_0mu_myg .section}

An ECS security group is a virtual firewall that is used to control the inbound and outbound traffic of ECS instances in a security group. After an ECS security group is added to the RDS whitelist, the ECS instances in the security group can access the RDS instance.

For more information, see [Create a security group](https://www.alibabacloud.com/help/doc-detail/25468.htm?spm=a2c63.p38356.a3.2.42187afeEXhLP9).

**Precautions**

-   Regions that support ECS security groups are China \(Hangzhou\), China \(Qingdao\), and Hong Kong.
-   You can configure both an IP address whitelist and an ECS security group. The IP addresses in the whitelist and the ECS instances in the security group can all access the RDS instance.
-   You can only add one ECS security group to an RDS instance.
-   Updates to the ECS security group are automatically synchronized to the IP address whitelist in real time.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567880536543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, click **Add Security Group**.
6.  Select the security group to be added and click **OK**.

    **Note:** Security groups with a VPC tag are security groups that are within VPCs.


## APIs {#section_j0x_oay_p8s .section}

|API|Description|
|---|-----------|
|[DescribeDBInstanceIPArrayList](../intl.en-US/API Reference/Security management/DescribeDBInstanceIPArrayList.md#)|Used to view the IP address whitelist of an RDS instance.|
|[ModifySecurityIps](../intl.en-US/API Reference/Security management/ModifySecurityIps.md#)|Used to modify the IP address whitelist of an RDS instance.|


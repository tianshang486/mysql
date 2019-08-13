# Configure a whitelist {#concept_pdr_k2f_vdb .concept}

After you create an RDS instance, you must configure a whitelist to allow external devices to access the instance. The default whitelist contains only 127.0.0.1. Before you add new IP addresses to the whitelist, no devices are allowed to access the RDS instance.

To configure a whitelist, you can perform the following operations:

-   Configure a IP address whitelist: Add IP addresses to the whitelist to allow access to the RDS instance.
-   Configure an ECS security group: Add an ECS security group for the RDS instance to allow ECS instances in the group to access the RDS instance.

A whitelist can be used to improve the security of your RDS instance. We recommend that you update the whitelist on a regular basis. Configuring a whitelist does not affect the normal operation of your RDS instance.

## Configure an IP address whitelist {#section_wyv_ws4_ydb .section}

**Precautions**

-   The default IP whitelist can only be edited or cleared, but cannot be deleted.
-   If you log on to DMS but the DMS server IP address has not been added to the whitelist, DMS prompts you to add the IP address and automatically generates a whitelist containing the IP address.
-   You must confirm which **network isolation mode** your RDS instance is in before configuring the whitelist. Refer to the corresponding operations based on the network isolation mode.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567928735435_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567928735436_en-US.png)

**Note:** The internal networks to which RDS instances belong are divided into two types: **classic network** and **VPC**.

-   Classic network: Alibaba Cloud automatically allocates IP addresses. Users only need to perform simple configurations. This network type is suitable for new users.
-   VPC: You can customize the network topology and IP addresses. It supports leased line connection, and is suitable for advanced users.

**If the network isolation mode is enhanced whitelist mode**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region where the target instance is located.

    ![Select a region](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156567928836543_en-US.png)

3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, follow these instructions based on your scenario:

    -   To access the RDS instance from an ECS instance located within a VPC, click **Edit** for default VPC whitelist.
    -   To access the RDS instance from an ECS instance located within the classic network, click **Edit** for the default Classic Network whitelist.
    -   To access the RDS instance from a server or computer located in a public network, click **Edit** for the default Classic Network whitelist.
    **Note:** 

    -   To allow ECS to access RDS through the intranet \(VPC or classic network\), make sure that the two instances are in the same region and have the same [network type](../../../../intl.en-US/User Guide/Instance management/Set network type.md#). Otherwise, the connection fails.
    -   You can also click **Create Whitelist** to create a new whitelist. In the displayed Create Whitelist dialog box, select a network type: **VPC** or **Classic Network/Public IP**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/156567928835445_en-US.png)

6.  In the displayed Edit Whitelist dialog box, add the IP addresses that need to access the instance, and then click **OK**.

    -   If you add an IP address range, such as 10.10.10.0/24, any IP address in the 10.10.10.X format can access the RDS instance.
    -   To add multiple IP addresses or IP address ranges, separate them with a comma \(without spaces\), for example, 192.168.0.1,172.16.213.9.
    -   You can click **Add Internal IP Addresses of ECS Instances** to display the IP addresses of all the ECS instances under your Alibaba Cloud accoun. and add to the whitelist.
    **Note:** After you add any IP address to the **default** whitelist, the default IP address 127.0.0.1 is automatically removed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656792881795_en-US.png)


**If the network isolation mode is standard whitelist mode**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner of the page, select the region where the target instance is located.
3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, click **Edit** for the **default** whitelist.

    **Note:** You can also click **Create Whitelist** to create another whitelist.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656792881794_en-US.png)

6.  In the displayed Edit Whitelist dialog box, add the IP addresses that need to access the instance, and then click **OK**.

    -   If you add an IP address range, such as 10.10.10.0/24, any IP address in the 10.10.10.X format can access the RDS instance.
    -   To add multiple IP addresses or IP address ranges, separate them with a comma \(without spaces\), for example, 192.168.0.1,172.16.213.9.
    -   You can click **Add Internal IP Addresses of ECS Instances** to display the IP addresses of all the ECS instances under your Alibaba Cloud accoun. and add to the whitelist.
    **Note:** After you add any IP address to the **default** whitelist, the default address 127.0.0.1 is automatically removed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15656792881795_en-US.png)


**Common incorrect settings**

-   If the IP address whitelist contains only the default address 127.0.0.1, no device is allowed to access the RDS instance. Therefore, you need to add IP addresses of devices to the whitelist to allow access to the instance.
-   The IP address in the whitelist is 0.0.0.0, but the correct format is 0.0.0.0/0.

    **Note:** 0.0.0.0/0 indicates that all devices are allowed to access the RDS instance. Exercise caution when using this IP address.

-   If the [enhanced whitelist](../../../../intl.en-US/User Guide/Security/Switch the IP whitelist to enhanced security mode.md#) mode is enabled, check the following:
    -   To connect to the RDS instance through the VPC address of the RDS instance, ensure that the internal IP address of the ECS instance is added to the **default VPC** whitelist.
    -   To connect to the RDS instance through the classic network address of the RDS instance, ensure that the internal IP address of the ECS instance is added to the **default Classic Network** whitelist.
    -   To connect to the RDS instance through [ClassicLink](https://www.alibabacloud.com/help/doc-detail/65412.htm), ensure that the internal IP address of the ECS instance is added to the **default VPC** whitelist.
    -   To connect to the RDS instance through the public address of the RDS instance, ensure that the public IP address of the device is added to the **default Classic Network** whitelist.
-   The public IP address that you add to the whitelist may not be the real outbound IP address. The reasons are as follows:

    -   The public IP address is not fixed and may dynamically change.
    -   The tools or websites used to query the public IP addresses may provide wrong IP addresses.
    For more information, see [How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?](../../../../intl.en-US/FAQs/How to connect__cannot connect/How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?.md#).


## Configure an ECS security group {#section_dsr_nt4_ydb .section}

An ECS security group is a virtual firewall that is used to control the inbound and outbound traffic of ECS instances in the security group. After an ECS security group is added to the RDS whitelist, the ECS instances in the security group can access the RDS instance.

For more information, see [Create a security group](https://www.alibabacloud.com/help/doc-detail/25468.htm?spm=a2c63.p38356.a3.2.42187afeEXhLP9).

**Precautions**

-   RDS versions that support an ECS security group are MySQL 5.6 and 5.7.
-   You can configure both the IP address whitelists and an ECS security group. The IP addresses in the whitelists and the ECS instances in the security group can all access the RDS instance.
-   You can only add one ECS security group to an RDS instance.
-   Updates to the ECS security group are automatically synchronized to the whitelist in real time.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target instance is located.
3.  Find the target instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab page, click **Add Security Group**.

    **Note:** Security groups with a VPC tag are within VPCs.

6.  Select a security group and click **OK**.

## APIs {#section_hcn_555_jgb .section}

|API|Description|
|---|-----------|
|[DescribeDBInstanceIPArrayList](../../../../intl.en-US/API Reference/Security management/DescribeDBInstanceIPArrayList.md#)|Used to view the IP address whitelist of an RDS instance.|
|[ModifySecurityIps](../../../../intl.en-US/API Reference/Security management/ModifySecurityIps.md#)|Used to modify the IP address whitelist of an RDS instance.|


# Configure a whitelist for an ApsaraDB RDS for MariaDB TX instance

This topic describes how to control access to your ApsaraDB RDS for MySQL instance. This allows only the specified external devices to access your RDS instance.

ApsaraDB for RDS provides two types of whitelists:

-   IP address whitelist
    -   Standard whitelist mode

        **Note:** ApsaraDB RDS for MariaDB TX instances can be deployed only in VPCs.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4450359951/p12628.png)

    -   Enhanced whitelist mode

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4450359951/p12629.png)

-   Security group

The configuration of IP address whitelists and security groups provides high security for your RDS instance and does not interrupt the operation of your RDS instance. We recommend that you update the IP address whitelists and security groups configured for your RDS instance on a regular basis.

## Precautions for configuring an IP address whitelist

-   You can modify or clear the IP address whitelist labeled default. However, you cannot delete this IP address whitelist.
-   Up to 200 IP address whitelists are allowed per RDS instance.
-   Up to 1,000 IP addresses and Classless Inter-Domain Routing \(CIDR\) blocks are allowed per RDS instance. If you want to add a large number of IP addresses, we recommend that you combine these IP addresses into CIDR blocks, such as 10.10.10.0/24. The length of the IP address prefix ranges from 1 bits to 32 bits. For example, /24 indicates that the length of the prefix is 24 bits. For more information, see [CIDR block FAQ](~~54484~~).
-   When you access an Alibaba Cloud service, the service automatically creates an IP address whitelist that contains the required IP address on your RDS instance. For example, [Alibaba Cloud Data Management \(DMS\)](https://www.alibabacloud.com/help/zh/doc-detail/47550.htm) creates an IP address whitelist named **ali\_dms\_group**, and Alibaba Cloud Database Autonomy Service \(DAS\) creates an IP address whitelist named **hdm\_security\_ips**. Do not modify or delete these IP address whitelists. If you modify or delete these IP address whitelists, the related services cannot access your RDS instance.

    **Note:** Do not add your own IP address to these IP address whitelists. If you add your own IP address to these IP address whitelists, your IP address will be overwritten by the updated IP addresses of the related services. If your IP address is overwritten, your workloads are interrupted.


## Configure an IP address whitelist in enhanced whitelist mode

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  Confirm your connection scenario and perform its required operations.

    ![Network type](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4450359951/p35445.png)

    ![Modify a whitelist](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0648272061/p1795.png)

    |Connection scenario|Operation|
    |-------------------|---------|
    |\(Recommended\) Your ECS and RDS instances reside in the same VPC.|    1.  On the **Whitelist Settings** tab of the Data Security page, click **Edit** to the right of the IP address whitelist labeled **default VPC**.
    2.  In the dialog box that appears, enter the private IP address of your ECS instance in the IP Addresses field and click **OK**.

**Note:** Applications running on your ECS instance can only connect to the internal endpoint of your RDS instance. |
    |Your ECS and RDS instances reside in different VPCs.|    1.  On the **Database Connection** page, click **Switch to Classic Network**. In the message that appears, click OK.
    2.  Click **Switch to VPC**. In the dialog box that appears, select the VPC that hosts your ECS instance and click OK.

**Note:** Your ECS and RDS instances can be migrated to the same VPC only when they reside in the same region. If they reside in different regions, we recommend that you use Alibaba Cloud Data Transmission Service \(DTS\) to migrate your RDS instance to the region where your ECS instance resides. This allows you to ensure service availability. For more information, see [Migrate data between ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Data Migration/Migrate data between ApsaraDB RDS for MySQL instances.md).

    3.  On the **Whitelist Settings** tab of the Data Security page, click **Edit** to the right of the IP address whitelist labeled **default VPC**.
    4.  In the dialog box that appears, enter the private IP address of your ECS instance in the IP Addresses field and click **OK**.

**Note:** Applications running on your ECS instance can only connect to the internal endpoint of your RDS instance. |
    |Your ECS instance resides in the classic network. Your RDS instance resides in a VPC.

|    1.  Migrate your ECS instance to the VPC that hosts your RDS instance. For more information, see [Migrate an ECS instance](https://www.alibabacloud.com/help/zh/doc-detail/57954.htm).

**Note:** Your ECS and RDS instances can be migrated to the same VPC only when they reside in the same region. If they reside in different regions, we recommend that you use DTS to migrate your RDS instance to the region where your ECS instance resides. This allows you to ensure service availability. For more information, see [Migrate data between ApsaraDB RDS for MySQL instances](/intl.en-US/RDS MySQL Database/Data Migration/Migrate data between ApsaraDB RDS for MySQL instances.md).

    2.  On the **Whitelist Settings** tab of the Data Security page, click **Edit** to the right of the IP address whitelist labeled **default VPC**.
    3.  In the dialog box that appears, enter the private IP address of your ECS instance in the IP Addresses field and click **OK**.

**Note:** Applications running on your ECS instance can only connect to the internal endpoint of your RDS instance. |
    |The host that requires access to your RDS instance resides outside the cloud.|    1.  On the **Whitelist Settings** tab of the Data Security page, click **Edit** to the right of the IP address whitelist labeled **default Classic Network**.
    2.  In the dialog box that appears, enter the public IP address of the on-premises server in the IP Addresses field and click **OK**.

**Note:**

        -   Applications running on the on-premises server can only connect to the public endpoint of your RDS instance.
        -   For more information about how to obtain the public IP address of an on-premises server, see [Determine the public IP address of an external server or client for an apsaradb RDS for MySQL or MariaDB instance](/intl.en-US/FAQs/Connections and Networks/How do I locate the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?.md) |

    **Note:**

    -   On the Whitelist Settings tab of the Data Security page, you can click **Create Whitelist**. In the Create Whitelist dialog box, you can set the Network Type parameter to **VPC** or **Classic Network/Public IP**.
    -   If you enter more than one IP address or CIDR block, you must separate them with commas \(,\). Example: 192.168.0.1,172.16.213.9.
    -   If you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all of the ECS instances that are created in your Alibaba Cloud account appear. Then, you can select the IP addresses that you want to add to the IP address whitelist.

## Configure an IP address whitelist in standard whitelist mode

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  On the **Whitelist Settings** tab, click **Edit** to the right of the IP address whitelist labeled **default**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5450359951/p1794.png)

    **Note:** You can also click **Create Whitelist** to create an IP address whitelist.

6.  In the **Edit Whitelist** dialog box, enter the required IP addresses or CIDR blocks in the IP Addresses field and click **OK**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0648272061/p1795.png)

    **Note:**

    -   After you add IP addresses or CIDR blocks to the IP address whitelist labeled **default**, the system deletes the default IP address 127.0.0.1.
    -   If you enter more than one IP address or CIDR block, you must separate them with commas \(,\). Example: 192.168.0.1,172.16.213.9.
    -   If you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all of the ECS instances that are created in your Alibaba Cloud account appear. Then, you can select the IP addresses that you want to add to the IP address whitelist.

## Configure an IP address whitelist in standard whitelist mode

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  On the **Whitelist Settings** tab, click **Edit** to the right of the IP address whitelist labeled **default**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5450359951/p1794.png)

    **Note:** You can also click **Create Whitelist** to create an IP address whitelist.

6.  In the **Edit Whitelist** dialog box, enter the required IP addresses or CIDR blocks in the IP Addresses field and click **OK**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0648272061/p1795.png)

    **Note:**

    -   After you add IP addresses or CIDR blocks to the IP address whitelist labeled **default**, the system deletes the default IP address 127.0.0.1.
    -   If you enter more than one IP address or CIDR block, you must separate them with commas \(,\). Example: 192.168.0.1,172.16.213.9.
    -   If you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all of the ECS instances that are created in your Alibaba Cloud account appear. Then, you can select the IP addresses that you want to add to the IP address whitelist.

## Common whitelist configuration errors

-   Your RDS instance has only one IP address whitelist that contains only the default IP address 127.0.0.1 in the **Data Security** \> **Whitelist Settings** navigation path.

    The default IP address 127.0.0.1 indicates that no devices can access your RDS instance. You must add the IP addresses of the devices that require access to your RDS instance to the IP address whitelist.

-   An IP address whitelist contains only one entry, 0.0.0.0.

    An IP address whitelist must contain entries similar to 0.0.0.0/0.

    **Note:** The 0.0.0.0/0 entry indicates that all devices can access your RDS instance. Exercise caution when you specify this entry.

-   When you configure an enhanced IP address for your RDS instance, the system reports IP address errors.

    For more information, see [Switch to the enhanced whitelist mode for an RDS instance]().

    -   If your RDS instance resides in a VPC and is connected by using its internal endpoint, make sure that the private IP address of your ECS instance is added to the IP address whitelist labeled **default VPC**.
    -   If your RDS instance resides in the classic network and is connected by using its internal endpoint, make sure that the private IP address of your ECS instance is added to the IP address whitelist labeled **default Classic Network**.
    -   If your RDS instance resides in a VPC and is connected by using [ClassicLink](https://www.alibabacloud.com/help/zh/doc-detail/65412.htm), make sure that the private IP address of your ECS instance is added to the IP address whitelist labeled **default VPC**.
    -   If your RDS instance is connected over the Internet, make sure that the public IP address of your ECS instance is added to the IP address whitelist labeled **default Classic Network**. \(The IP address whitelist labeled default VPC cannot be used to control access over the Internet.\)
-   The public IP addresses that you add to an IP address whitelist are not the actual egress IP addresses.

    This problem may occur due to the following reasons:

    -   Public IP addresses dynamically change.
    -   The tool or website that you use to query public IP addresses returns inaccurate results.
    For more information, see [Determine the public IP address of an external server or client for an apsaradb RDS for MySQL or MariaDB instance](/intl.en-US/FAQs/Connections and Networks/How do I locate the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?.md).


## Precautions for configuring a security group

-   You can configure both IP address whitelists and security groups for your RDS instance. All of the IP addresses in the configured IP address whitelists and all of the ECS instances in the configured security groups can access your RDS instance.
-   Up to 10 security groups are allowed per RDS instance.
-   Updates to a security group are automatically synchronized to your RDS instance.
-   You can add only a security group that has the same network type as your RDS instance. In this case, the network types of your RDS instance and the security group that you want to add must both be VPC or classic network.

    **Note:** After you change the network type of your RDS instance, the security group that you have added becomes invalid. You must add the security group with the required network type again.


## Configure a security group

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Data Security**.

5.  On the **Whitelist Settings** tab, click **Add Security Group**.

6.  Select the target security group and click **OK**.

    **Note:** Security groups followed by a VPC tag contain ECS instances that reside in VPCs.


## FAQ

-   Does an IP address whitelist immediately take effect after it is configured?

    No, an IP address whitelist requires about 1 minute to take effect after it is configured.

-   Why do I find IP address whitelists that I did not create?

    If these IP address whitelists contain private IP addresses, they are probably generated by other Alibaba Cloud services, such as DMS and DAS. In this case, these IP address whitelists do not affect your business data, and no further actions are required.

    ![IP address whitelist created by HDM](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5450359951/p68936.png)

-   If I disable Internet access and enable only internal network access, will my RDS instance be exposed to security risks?

    Yes, if you disable Internet access and enable only internal network access, your RDS instance will be exposed to security risks. We recommend that you change the network type of your RDS instance to VPC. In this case, only the ECS instances that reside in the same VPC as your RDS instance are granted access after the required IP addresses are added to an IP address whitelist of your RDS instance. For more information, see [Change the network type of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)


## Related operations

|Operation|Description|
|---------|-----------|
|[t8127.md\#](/intl.en-US/API Reference/Security management/Query IP address whitelists.md)|Queries the IP address whitelists of an ApsaraDB for RDS instance.|
|[t8132.md\#](/intl.en-US/API Reference/Security management/Modify IP address whitelist.md)|Modifies an IP address whitelist of an ApsaraDB for RDS instance.|


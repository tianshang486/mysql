# Configure a whitelist for an ApsaraDB RDS for SQL Server instance

This topic describes how to control access to your ApsaraDB RDS for MySQL instance. This allows only the specified external devices to access your RDS instance.

Whitelists make your RDS instance more secure and do not interrupt the operation of your RDS instance during configuration. We recommend that you maintain whitelists on a regular basis.

**Note:** The IP address whitelist labeled default contains only the default IP address 127.0.0.1, which denies all entities access to your RDS instance.

## Precautions for configuring an IP address whitelist

-   You can modify or clear the IP address whitelist labeled default. However, you cannot delete this IP address whitelist.
-   Up to 200 IP address whitelists are allowed per RDS instance.
-   Up to 1,000 IP addresses and Classless Inter-Domain Routing \(CIDR\) blocks are allowed per RDS instance. If you want to add a large number of IP addresses, we recommend that you combine these IP addresses into CIDR blocks, such as 10.10.10.0/24. The length of the IP address prefix ranges from 1 bits to 32 bits. For example, /24 indicates that the length of the prefix is 24 bits. For more information, see [CIDR block FAQ](~~54484~~).
-   When you access an Alibaba Cloud service, the service automatically creates an IP address whitelist that contains the required IP address on your RDS instance. For example, [Alibaba Cloud Data Management \(DMS\)](https://www.alibabacloud.com/help/zh/doc-detail/47550.htm) creates an IP address whitelist named **ali\_dms\_group**, and Alibaba Cloud Database Autonomy Service \(DAS\) creates an IP address whitelist named **hdm\_security\_ips**. Do not modify or delete these IP address whitelists. If you modify or delete these IP address whitelists, the related services cannot access your RDS instance.

    **Note:** Do not add your own IP address to these IP address whitelists. If you add your own IP address to these IP address whitelists, your IP address will be overwritten by the updated IP addresses of the related services. If your IP address is overwritten, your workloads are interrupted.


## Procedure

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

## Common errors

-   Your RDS instance has only one IP address whitelist that contains only the default IP address 127.0.0.1 in the **Data Security** \> **Whitelist Settings** navigation path.

    The default IP address 127.0.0.1 indicates that no devices can access your RDS instance. You must add the IP addresses of the devices that require access to your RDS instance to the IP address whitelist.

-   An IP address whitelist contains only one entry, 0.0.0.0.

    An IP address whitelist must contain entries similar to 0.0.0.0/0.

    **Note:** The 0.0.0.0/0 entry indicates that all devices can access your RDS instance. Exercise caution when you specify this entry.

-   The public IP addresses that you add to a whitelist may not be the real egress IP addresses of the devices that require access to your RDS instance. Possible reasons are as follows:
    -   Public IP addresses are not static and may change.
    -   The tool or website you use to query public IP addresses yields inaccurate results.

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


# Configure a whitelist {#concept_rpj_hs4_ydb .concept}

After an RDS instance is created, you must configure a whitelist so that external devices can access the RDS instance. The default whitelist is an IP address whitelist that contains only the default IP address **127.0.0.0.1**. This default IP address means that no devices can access the RDS instance.

You can configure the following two types of whitelists:

-   IP address whitelist: Add IP addresses to a whitelist so that these IP addresses can access the RDS instance.
-   ECS security group whitelist: Add an ECS security group to a whitelist so that all ECS instances in the ECS security group can access the RDS instance.

We recommend that you periodically check and adjust your whitelists to maintain RDS security. Configuring a whitelist does not affect the normal running of the RDS instance.

## Configure an IP address whitelist {#section_wyv_ws4_ydb .section}

Precautions:

-   The default IP address whitelist can be modified or cleared but cannot be deleted.
-   If you attempt to log on to CloudDBA or DMS without adding their IP addresses to a whitelist, the system displays a message, stating that you can log on to them only after you add their IP addresses to a whitelist.

Procedure:

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156645484137169_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the **Whitelist Settings** tab, find the **default** section and click **Edit**.

    **Note:** You can also click **Create Whitelist** to create a whitelist.

    ![编辑默认白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7948/15664548414139_en-US.png)

6.  In the Edit Whitelist dialog box, enter IP addresses or CIDR blocks and click **OK**.

    -   If you enter a CIDR block, for example, **10.10.10.0/24**, then any IP addresses in 10.10.10.X format can access the RDS instance.
    -   If you enter multiple IP addresses or CIDR blocks, you must separate them by using commas \(,\) and leave no spaces preceding or following the commas, for example, **192.168.0.1,172.16.213.9**.
    -   If you click **Add Internal IP Addresses of ECS Instances**, the IP addresses of all ECS instances under your Alibaba Cloud account are displayed in the **Whitelist** field.
    **Note:** After you add IP addresses or CIDR blocks to the **default** whitelist, the system automatically deletes the default IP address 127.0.0.1.

    ![修改默认白名单对话框](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7816/15664548411795_en-US.png)


Common errors:

-   The **default** whitelist contains only the default IP address **127.0.0.0.1**, which means that no devices can access the RDS instance. In such case, you must add the IP address of the peer device you want to access the RDS instance.
-   The IP addresses you add to the whitelist are in 0.0.0.0 format, but the correct format is 0.0.0.0/0.

    **Note:** The value **0.0.0.0/0** indicates that all devices can access the RDS instance. Do proceed with caution.

-   The enhanced whitelist function is enabled. For more information, see [Switch the IP whitelist to enhanced security mode](intl.en-US/User Guide/Security/Switch the IP whitelist to enhanced security mode.md#). In such case, check the following configuration:
    -   If you want the ECS instance to communicate with the RDS instance through the intranet in a VPC, make sure that the private IP address of the ECS instance is added to the VPC group.
    -   If you want the ECS instance to communicate with the RDS instance through the intranet in a classic network, make sure that the private IP address of the ECS instance is added to the classic network group.
    -   If you want the ECS instance to communicate with the RDS instance through the Internet, make sure that the public IP address of the ECS instance is added to the classic network group. The VPC group cannot be used for communication through the Internet.
-   The public IP address that you add to the whitelist is not the real outbound IP address of the ECS instance. Possible reasons are as follows:

    -   The public IP address dynamically changes.
    -   The IP address query tool or website yields inaccurate results.
    You can resolve the problem with the following resources:

    -   [How do I locate the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?](../intl.en-US/FAQs/How to connect__cannot connect/How do I locate the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX?.md#)
    -   [How do I locate the IP address connected to an RDS for SQL Server instance?](../intl.en-US/FAQs/How to connect__cannot connect/How do I locate the IP address connected to an RDS for SQL Server instance?.md#)
    -   [How do I locate the IP address connected to an RDS for PostgreSQL or RDS for PPAS instance?](../intl.en-US/FAQs/How to connect__cannot connect/How do I locate the IP address connected to an RDS for PostgreSQL or RDS for PPAS instance?.md#)

## Configure an ECS security group whitelist {#section_dsr_nt4_ydb .section}

An ECS security group is a virtual firewall that is used to set network access control for one or more ECS instances. After an ECS security group is added to a whitelist for an RDS instance, all ECS instances in the ECS security group can access the RDS instance.

For more information, see [Create a security group](https://www.alibabacloud.com/help/doc-detail/25468.htm?spm=a2c63.p38356.a3.2.42187afeEXhLP9).

Precautions:

-   The database engines that support ECS security groups are MySQL 5.6, PostgreSQL, and MariaDB TX.
-   The regions that support ECS security groups are China \(Hangzhou\), China \(Qingdao\), and China \(Hong Kong\).
-   You can have one ECS security group whitelist and multiple IP address whitelists. All IP addresses in the IP address whitelists and all ECS instances in the ECS security group whitelist can access the RDS instance.
-   One RDS instance supports only one ECS security group whitelist.
-   After you update the ECS security group whitelist, the new ECS security group whitelist takes effect immediately.

Procedure:

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156645484137169_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the **Whitelist Settings** tab, click **Add Security Group**.

    **Note:** An ECS security group with a VPC tag is located in a VPC.

6.  Select an ECS security group and click **OK**.


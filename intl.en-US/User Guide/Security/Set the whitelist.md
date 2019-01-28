# Set the whitelist {#concept_rpj_hs4_ydb .concept}

After an RDS instance is created, you need to set the whitelist so that servers can connect to the RDS instance. By default, the whitelist contains only the default IP address 127.0.0.1 and has no security group. This means that no server can access the RDS instance. The whitelist only controls access to the RDS instance and does not affect instance performance.

You can use either of the following methods to set the whitelist:

-   Set the IP whitelist: Add IP addresses to the whitelist so that these IP addresses can access the RDS instance.
-   Set the ECS security group: Add an ECS security group to the whitelist so that ECS instances in the security group can access the RDS instance.

We recommend that you periodically check and adjust the whitelist according to your requirements to maintain RDS security.

## Attention {#section_wqz_5s4_ydb .section}

-   The default IP whitelist group can only be modified or cleared, and cannot be deleted.
-   % or 0.0.0.0/0 indicates that any IP address is allowed to access the RDS instance. This configuration greatly reduces the security of the database and is not recommended.
-   If you cannot connect to the RDS instance after adding the application service IP address to the whitelist, you can obtain the actual IP address of the application by referring to [How to locate the local IP address using ApsaraDB for MySQL](https://www.alibabacloud.com/help/faq-detail/41754.htm).

## Procedure {#section_wyv_ws4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper left corner, select the region where the target instance is located.
3.  Locate the target instance and click its ID.
4.  In the left-side navigation pane, click **Security** to visit the Security page.
5.  On the Whitelist Settings tab page, find the **default** whitelist group and click **Modify**.

    **Note:** You can also click **Add a Whitelist Group** to create a new group.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7948/15486593994139_en-US.png)

6.  In the White List field of the displayed dialog box, add the IP addresses or IP address segments that need to access the RDS instance, and click **OK**.

    **Note:** 

    -   If you enter an IP address segment, such as 10.10.10.0/24, it indicates that any IP address in the format of 10.10.10.X can access the RDS instance.
    -   If you want to enter multiple IP addresses or IP address segments, separate them by comma \(but do not add blank spaces before or after commas\), such as **192.168.0.1,172.16.213.9**.
    -   If you click **Upload ECS Intranet IP Address**, the system displays the IP addresses of all ECS instances under your Alibaba Cloud account, and you can quickly add intranet IP addresses of ECS instances.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7948/15486593994140_en-US.png)


## Precautions for adding an ECS security group {#section_tsz_lt4_ydb .section}

You can configure both the IP whitelist and ECS security group. Your RDS instance allows access from servers whose IP addresses are in the IP whitelist and ECS instances that are in the security group.

-   Currently, only MySQL 5.6 and the Hangzhou, Qingdao, and Hong Kong regions support ECS security groups.
-   One RDS instance supports one security group.
-   Updates to the ECS security group are automatically applied to the whitelist.

## Add an ECS security group {#section_dsr_nt4_ydb .section}

A security group is a virtual firewall that is used to set network access control for one or more ECS instances. For more information about ECS security groups, see [Create a security group](https://www.alibabacloud.com/help/doc-detail/25468.htm).

**Precautions**

-   RDS instances that support ECS security groups are MySQL 5.6, PostgreSQL, and MariaDB TX.
-   Regions that support ECS security groups: Hangzhou, Qingdao, and Hongkong.
-   You can set both the IP whitelist and ECS security group. All ECS instances specified in either the IP whitelist or security group can access the RDS instance.
-   Currently each RDS instance can have only one ECS security group.

**Procedure**

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper left corner, select the region where the target instance is located.
3.  Locate the target instance and click its ID.
4.  In the left-side navigation pane, click **Security** to visit the Security page.
5.  On the Whitelist Settings tab page, click **Add to Security Group**.

    **Note:** Security groups marked with "VPC" are in VPCs.

6.  Select a security group and click **OK**.


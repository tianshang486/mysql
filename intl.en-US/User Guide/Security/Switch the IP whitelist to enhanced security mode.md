# Switch the IP whitelist to enhanced security mode {#concept_vzw_gq2_x2b .concept}

## IP whitelist modes {#section_ywn_rz2_x2b .section}

RDS instances provide two IP whitelist modes:

-   **Standard mode**: IP addresses in the whitelist apply to both classic networks and VPCs. This has security risks, so it is recommended that you switch to the enhanced security mode.
-   **Enhanced security mode**: IP addresses in the whitelist are classified into two types: \(1\) IP addresses for classic networks and the Internet; \(2\) IP addresses for VPCs. In this mode, you need to specify the network type when you create an IP whitelist group.

    Currently, RDS for MySQL, PostgreSQL, and PPAS instances support the enhanced security mode.


## Changes after switching to the enchanced security mode {#section_ppy_wr2_x2b .section}

-   If the instance network type is VPC, a new whitelist group is generated and contains all IP addresses in the original whitelist. The new IP whitelist group applies only to VPCs.
-   If the instance network type is classic network, a new whitelist group is generated and contains all IP addresses in the original whitelist. The new IP whitelist group applies only to classic networks.
-   If the instance is in [hybrid access mode](intl.en-US/User Guide/Connection management/Hybrid access solution for smooth migration from classic networks to VPCs.md) \(namely, an instance uses both a classic network and a VPC\), two new whitelist groups are generated and each contain all IP addresses in the original whitelist. One of the whitelist group applies to VPCs and the other applies to classic networks.

**Note:** The switch does not affect the [ECS security group](intl.en-US/User Guide/Security/Set the whitelist.md#section_dsr_nt4_ydb) in the instance whitelist.

## Attention {#section_mfd_4t2_x2b .section}

An IP whitelist can be switched from the standard mode to the enhanced security mode, and the switch is irreversible.

## Procedure {#section_jjp_1r2_x2b .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the instance is located.
3.  Click the ID of instance.
4.  In the left-side navigation pane, select **Security**.
5.  On the Whitelist Settings tab page, click **Enable Enhanced Security Whitelist \(Recommended\)**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18575/155282831910072_en-US.png)

6.  In the displayed dialog box, click **Confirm**.


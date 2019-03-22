# Hybrid access solution for smooth migration from classic networks to VPCs {#concept_ytc_d1y_wdb .concept}

[Virtual Private Cloud \(VPC\)](https://www.alibabacloud.com/help/doc-detail/34217.htm) is a private network logically isolated from other virtual networks. A VPC allows you to build an isolated network environment with better security and performance than classic networks. With these benefits, VPCs have become a preferred networking choice for cloud users.

To meet the increasing network migration needs, RDS has added a new feature called hybrid access mode. This feature enables smooth migration from classic networks to VPCs with no intermittent service interruption or access interruption. The feature also offers the option to migrate a master instance and its read-only instances separately to a VPC without any interference with each other.

This document explains how to migrate from a classic network to a VPC on the RDS console using the hybrid access solution.

## Background information {#section_lqq_w1y_wdb .section}

With a traditional solution, migrating an RDS instance from a classic network to a VPC causes immediate release of classic network IP address. As a result, an intermittent interruption for up to 30 seconds may be caused, and ECS on the classic network can no longer access the RDS instance using the intranet IP address, which may have negative impact on your services. In many large companies, a database is usually designed for access by more than one application system. When they decide to migrate the database from a classic network to a VPC, it would be quite difficult to migrate the network of all the applications simultaneously, which may result in bigger impact on their services. Therefore, a transitional period is required. To accommodate the need for smooth migration, RDS has added the hybrid access feature, making it possible to have such a transitional period.

Hybrid access refers to the ability of an RDS instance to be accessed by ECSs on both a classic network and a VPC. During the hybrid access period, the RDS instance reserves the intranet IP address of the original classic network and adds an intranet IP address for a VPC, which prevents any intermittent interruption during migration. We recommend that you use a VPC only for purposes of security and performance. For this reason, hybrid access is available for a limited period of time. That means the intranet IP address of the original classic network is released when the hybrid access period expires. In this case, your applications cannot access the database using the intranet IP address of the classic network. You must configure the intranet IP address for a VPC in all your applications during the hybrid access period to guarantee smooth network migration and minimize the impact on your services.

For example, a company wants to migrate its database from a classic network to a VPC. The hybrid access solution can be used to provide a transitional period during which some of their applications can access the database through a VPC, and the others can continue to access the database through original classic network. When all the applications can access the database through the VPC, the intranet IP address of the original classic network can be released, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7944/15532444354743_en-US.png)

## Functional Limits {#section_tzs_y1y_wdb .section}

The following functional limits are proposed during the hybrid access period:

-   Switch to classic networks is not supported.
-   Zone migration is not supported.

## Prerequisites {#section_rzd_nx2_zdb .section}

-   The current network type is classic network.
-   There are available VPC and vSwitch in the zone where the RDS instance is located. If not, create them by referring to [Create VPC](https://www.alibabacloud.com/help/doc-detail/53604.htm) and [Create vSwitch](https://www.alibabacloud.com/help/doc-detail/53670.html).

## Procedure {#section_cy4_px2_zdb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the Basic Information page.
4.  In the left-side navigation pane, click **Connection Options** to enter the Connection Options page.
5.  On the Instance Connection tab page, click **Switch to VPC**.
6.  On the Switch to VPC confirmation page, select the target VPC and Vswitch.
7.  Check **Reserve original classic endpoint**, and select the **Expiration time** for the basic intranet IP address of the original network, as shown in the following figure.

    **Note:** 

    -   From the seventh day before the date on which the intranet IP address of the original classic network is to be released, the system sends a text message of a notice to the mobile number bound to your account every day.
    -   When the reservation ages out, the intranet IP address of the classic network is automatically released and can no longer be used to access the database. To prevent service interruption, set a reservation period as necessary. After the hybrid access configuration is complete, you can change the expiration date.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7944/15532444354745_en-US.png)

8.  Click **OK**.

    The **Original classic endpoint** area is displayed, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7944/15532444354747_en-US.png)


## Change the expiration time of the original classic network {#section_pwp_wx2_zdb .section}

During the hybrid access period, you can change the reservation period of the intranet IP address of the original classic network at any time as needed, and the expiration date is recalculated from the new date. For example, if the intranet IP address of the original classic network is set to August 18, 2017, and you change the expiration time to 14 days later on August 15, 2017, the address is released on August 29, 2017.

Follow these steps to change the expiration time:

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  Select the region where the target instance is located.
3.  Click the ID of the instance to visit the Basic Information page.
4.  In the left-side navigation pane, click **Connection Options** to enter the Connection Options page.
5.  On the Instance Connection tab page, click **Change Expiration time**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7944/15532444354748_en-US.png)

6.  On the Change Expiration Time confirmation page, select an expiration time and click **OK**.


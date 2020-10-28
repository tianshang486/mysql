# Change the network type of an ApsaraDB RDS for PostgreSQL instance

This topic describes how to change the network type of an ApsaraDB RDS for PostgreSQL instance between classic network and virtual private cloud \(VPC\).

## Network types

-   Classic network: RDS instances in the classic network are not isolated. You can block unauthorized access only by configuring IP address whitelists on these instances.
-   VPC: Each VPC is an isolated network. VPCs are more secure than the classic network. Therefore, we recommend that you select the VPC network type.

    You can configure route tables, Classless Inter-Domain Routing \(CIDR\) blocks, and gateways in a VPC. You can also connect your self-managed data center to a VPC by using leased lines or VPNs. This allows you to build a virtual data center, in which you can migrate applications to the cloud without service interruptions.


**Note:**

-   You can select the classic or VPC network type and change between the two network types free of charge.
-   Before you change the network type, you must switch the RDS instance to the enhanced whitelist mode. For more information, see [Switch an ApsaraDB RDS for PostgreSQL instance to the enhanced whitelist mode](/intl.en-US/RDS PostgreSQL Database/Data security/Switch an ApsaraDB RDS for PostgreSQL instance to the enhanced whitelist mode.md).

## Change the network type from VPC to classic network

Precautions

-   After you change the network type from VPC to classic network, the internal endpoint of the RDS instance remains unchanged. However, the IP address that is associated with the internal endpoint changes.
-   After you change the network type from VPC to classic network, you cannot connect an Alibaba Cloud Elastic Compute Service \(ECS\) instance to the RDS instance by using the internal endpoint. This applies if the ECS instance resides in a VPC. After you change the network type, make sure that you immediately update the endpoint information on your application.
-   When you change the network type, a transient connection error of about 30 seconds may occur. To avoid interruptions to your workloads, we recommend that you perform the network type change during off-peak hours. Alternatively, make sure that your application is configured to automatically reconnect to the RDS instance.
-   If the RDS instance runs PostgreSQL 10, 11, or 12 on RDS Basic Edition, you cannot change the network type from VPC to the classic network.

Procedure

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where the RDS instance resides.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1650359951/p49697.png)

3.  Find the RDS instance and click its ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  On the Instance Connection tab, click **Switch to Classic Network**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3350359951/p12632.png)

6.  In the message that appears, click **OK**.

    After the network type is changed to classic network, only a classic network-housed ECS instance can connect to the RDS instance by using the internal endpoint. You must modify the ECS instance to configure the internal endpoint that is used to connect to the RDS instance.

7.  Configure an IP address whitelist. This allows a classic network-housed ECS instance to connect to the RDS instance by using the internal endpoint.
    -   If the RDS instance runs in standard whitelist mode, you can add the private IP address of the classic network-housed ECS instance to an IP address whitelist of the classic or VPC network type.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3350359951/p12631.png)

    -   If the RDS instance runs in enhanced whitelist mode, you can add the private IP address of the classic network-housed ECS instance only to an IP address whitelist of the classic network type. For more information, see [Switch an ApsaraDB RDS for PostgreSQL instance to the enhanced whitelist mode](/intl.en-US/RDS PostgreSQL Database/Data security/Switch an ApsaraDB RDS for PostgreSQL instance to the enhanced whitelist mode.md). If no IP address whitelists of the classic network type are available, create one.

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3350359951/p12630.png)


## Change the network type from classic network to VPC

Procedure

1.  Log on to the [ApsaraDB RDS console](https://rds.console.aliyun.com/).
2.  In the top navigation bar, select the region where the RDS instance resides.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1650359951/p49697.png)

3.  Find the RDS instance and click its ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  On the Instance Connection tab, click **Switch to VPC**.
6.  In the dialog box that appears, select a VPC and a VSwitch and specify whether to retain the classic network endpoint.
    -   Select a VPC. We recommend that you select the VPC where the ECS instance that houses your application resides. If the ECS and RDS instances reside in different VPCs, these instances cannot communicate by using the internal endpoint unless you create a Cloud Enterprise Network \(CEN\) instance or gateway between the VPCs of these instances.For more information, see [Alibaba Cloud CEN tutorials](https://www.alibabacloud.com/help/zh/doc-detail/64648.htm) and [Establish a connection between two VPCs](/intl.en-US/User Guide/Configure IPsec-VPN connections/Establish a connection between two VPCs.md).
    -   Select a VSwitch. If no VSwitches are available in the selected VPC, create one in the same zone where the RDS instance resides. For more information, see [Create a VSwitch](/intl.en-US/VPCs and VSwitches/VSwitch management/Create a VSwitch.md).

        ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3350359951/p3260.png)

    -   Clear or select the **Reserve Original Classic Network Endpoint** option. For more information, see the following table.

        |Action|Description|
        |------|-----------|
        |Clear the Reserve Original Classic Network Endpoint option|The classic network endpoint is not retained and will become a VPC endpoint.

When you change the network type from classic network to VPC, a transient connection error of about 30 seconds will occur. In this case, the connection between each classic network-housed ECS instance and the RDS instance is closed.|
        |Select the Reserve Original Classic Endpoint option|The classic network endpoint is retained, and a new VPC endpoint is generated. In this case, the RDS instance runs in hybrid access mode. Both classic network- and VPC-housed ECS instances can connect to the RDS instance by using the internal endpoint. For more information, see [Configure a hybrid access solution to smoothly migrate an RDS instance from the classic network to a VPC](/intl.en-US/RDS PostgreSQL Database/Network, VPC, and VSwitch/Configure a hybrid access solution to smoothly migrate the database from the classic network to a VPC.md).

When you change the network type from classic network to VPC, no transient connection errors will occur. The connection between each classic network-housed ECS instance and the RDS instance remains available until the classic network endpoint expires.

Before the classic network endpoint expires, you must add the VPC endpoint to the ECS instance that houses your application. This allows you to migrate your workloads to the selected VPC without interruptions. In addition, before the classic network endpoint expires, the system will send a text message to the phone number that is bound to your Alibaba Cloud account for seven consecutive days.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5350359951/p12639.png)

For more information, see [Configure a hybrid access solution to smoothly migrate the database from the classic network to a VPC](/intl.en-US/RDS PostgreSQL Database/Network, VPC, and VSwitch/Configure a hybrid access solution to smoothly migrate the database from the classic network to a VPC.md). |

7.  Add the private IP address of the ECS instance that houses your application in the selected VPC to an IP address whitelist of the VPC network type. This allows the ECS instance to connect to the RDS instance by using the internal endpoint. If no IP address whitelists of the VPC network type are available, create one.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5350359951/p12638.png)

8.  -   Add the VPC endpoint of the RDS instance to the ECS instance that houses your application. If you have selected the Reserve Original Classic Network Endpoint option, add the generated VPC endpoint to each VPC-housed ECS instance before the classic network endpoint expires.
-   If you have cleared the Reserve Original Classic Network Endpoint option, the connection between each classic network-housed ECS instance and the RDS instance is immediately closed after you change the network type. You must immediately add the generated VPC endpoint to each VPC-housed ECS instance after you change the network type. Add the VPC endpoint of the RDS instance to the ECS instance that houses your application.
    **Note:** If you want to connect a classic network-housed ECS instance to the VPC-housed RDS instance by using the internal endpoint, you can use ClassicLink to establish a connection. Alternatively, you can migrate the ECS instance to the same VPC as the RDS instance. For more information, see [Overview](/intl.en-US/VPC network connections/ClassicLink/Overview.md).


## FAQ

How do I change the VPC of my RDS instance?

You cannot directly change the VPC of your RDS instance. You can change the VPC by using the following methods:

-   If your RDS instance supports changes between the classic and VPC network types, perform the following steps:
    1.  Change the network type from VPC to classic network.
    2.  Change the network type from classic network to VPC. During this process, select the VPC that you want.
-   If your RDS instance does not support changes between the classic and VPC network types, perform the following steps:

    Purchase a new RDS instance. During this process, select the VPC that you want. Then, migrate the data of your RDS instance to the new RDS instance. For more information, see [Migrate data between ApsaraDB for RDS instances](/intl.en-US/RDS PostgreSQL Database/Data Migration/Migrate data between ApsaraDB for RDS instances.md).


## Related operations

|Operation|Description|
|---------|-----------|
|[ModifyDBInstanceNetworkType](/intl.en-US/API Reference/Network management/Change the network type of an ApsaraDB for RDS instance.md)|Changes the network type of an ApsaraDB RDS instance.|


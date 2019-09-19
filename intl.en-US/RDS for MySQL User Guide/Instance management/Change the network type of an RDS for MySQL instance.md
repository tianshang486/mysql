# Change the network type of an RDS for MySQL instance {#concept_zqv_gxx_wdb .concept}

This topic describes how to change the network type of an RDS for MySQL instance.

## Network types {#section_54g_4u9_7w6 .section}

-   Classic network: Instances in a classic network are not isolated. Access control is implemented for instances by using whitelists.
-   Virtual Private Cloud \(VPC\): A VPC is an isolated network environment. We recommend that you use VPC because it is more secure.

    You can customize the routing table, IP address range, and gateway of the VPC. To smoothly migrate applications to the cloud, you can use a leased line or VPN to connect your own data center to a VPC on the cloud to make a virtual data center.


**Note:** 

-   You can use the classic network or VPC and switch between the network types for free.
-   For PostgreSQL instances, you must switch the IP whitelist mode to the enhanced whitelist mode before switching the network type. For more information, see [Switch to the enhanced whitelist mode for an RDS for MySQL instance](intl.en-US/RDS for MySQL User Guide/Data security/Switch to the enhanced whitelist mode for an RDS for MySQL instance.md#).

## Switch from VPC to classic network {#section_gjc_1ws_6k0 .section}

**Precautions** 

-   After the network type of an RDS instance is switched to classic network, the endpoints remain unchanged, but the corresponding IP addresses change.
-   After the network type of an RDS instance is switched to classic network, ECS instances in VPCs cannot access the RDS instance by using the internal endpoint. Make sure that you change the endpoint on the application.
-   Switching the network type may result in a disconnection of 30 seconds. To avoid impacts that arise from this operation, we recommend that you perform the switching during off-peak hours, or configure automatic reconnection policies for your application.
-   Instances of PostgreSQL 11 High-availability Edition \(cloud disk\), PostgreSQL 10 High-availability Edition \(cloud disk\), and PostgreSQL 10 Basic Edition do not support the classic network. Therefore, you cannot switch these instances to the classic network.

**Procedure**

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62164/156888523949697_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  In the Database Connection section, click **Switch to Classic Network**.

    ![切换为经典网络](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/156888523912632_en-US.png)

6.  In the message that appears, click **OK**.

    After the network type is switched, only ECS instances in classic networks can access the RDS instance over the internal network. Make sure that you configure the endpoint of the RDS instance on the ECS instance in the classic network.

7.  Configure the whitelist of the RDS instance to allow access from the ECS instance over the internal network.
    -   If the RDS instance applies the standard whitelist mode, as shown in the following figure, you must add the internal endpoint of the ECS instance in the classic network to any whitelist of the RDS instance.

        ![通用白名单模式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/156888523912631_en-US.png)

    -   If the RDS instance applies the [enhanced whitelist mode](intl.en-US/RDS for MySQL User Guide/Data security/Switch to the enhanced whitelist mode for an RDS for MySQL instance.md#), as shown in the following figure, you must add the internal endpoint of the ECS instance in the classic network to the **default classic network whitelist** of the RDS instance. If there is no classic network whitelist, you must create a new whitelist.

        ![高安全白名单模式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/156888523912630_en-US.png)


## Switch from classic network to VPC {#section_bec_zzf_7gb .section}

**Procedure**

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62164/156888523949697_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Database Connection**.
5.  Click **Switch to VPC**.
6.  In the dialog box that appears, select a VPC and a VSwitch, and specify whether to retain the classic network address.
    -   Select a VPC. We recommend that you select the VPC where your ECS instance is located. Otherwise, the ECS and RDS instances cannot connect to each other over the internal network unless [Express Connect](../../../../../intl.en-US/Peering connections/Interconnect two VPCs under the same account.md#) or [VPN Gateway](../../../../../intl.en-US/User Guide/Configure IPsec-VPN connections/Establish a connection between two VPCs.md) are created to connect the two VPCs.
    -   Select a VSwitch. If there is no VSwitch in the VPC that you select, as shown in the following figure, you must create a VSwitch in the zone where the instance is located. For more information, see [Manage VSwitches](../../../../../intl.en-US/VPCs and VSwitches/VSwitch management/Create a VSwitch.md#).

        ![管理交换机](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/15688852393260_en-US.png)

    -   Select or clear **Reserve Original Classic Endpoint** as needed. The following table describes the details.

        |Action|Description|
        |------|-----------|
        |Clear| The classic network address is not retained. The original classic network address is changed to the VPC address.

 If you do not retain the classic network address, the RDS instance will be disconnected for 30 seconds, and the access from the ECS instance in the classic network to the RDS instance over the internal network is immediately disconnected when you switch the network type.|
        |Select| The classic network address is retained, and a new VPC address is generated, as shown in the following figure. It indicates that the [hybrid access mode](intl.en-US/RDS for MySQL User Guide/Network management/Configure a hybrid access solution to smoothly migrate an RDS instance from the classic network to a VPC.md#) is enabled, and the RDS instance can be accessed by ECS instances in both a classic network and a VPC.

 If you retain the classic network address, the RDS instance will not be disconnected when you switch the network type. The internal access from the ECS instance in the classic network to the RDS instance is only disconnected when the classic network address expires.

 Before the classic network address expires, make sure that the VPC address has been configured in the ECS instance in the VPC to smoothly migrate your services to the VPC. The system will send an SMS message to the phone number bound to your Alibaba Cloud account every day in the seven days before the classic network address expires.

 ![数据库连接](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/156888523912639_en-US.png)

 For more information, see [Configure a hybrid access solution to smoothly migrate an RDS instance from the classic network to a VPC](intl.en-US/RDS for MySQL User Guide/Network management/Configure a hybrid access solution to smoothly migrate an RDS instance from the classic network to a VPC.md#).

 |

7.  Add the internal IP address of the ECS instance in the VPC to the **VPC whitelist** of the RDS instance, so that the ECS instance can access the RDS instance over the internal network, as shown in the following figure. If there is no VPC whitelist, you must create a new whitelist.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/156888524012638_en-US.png)

8.  Perform one of the following operations as needed:

    -   If you retain the classic network address, you must configure the VPC address of the RDS instance in the ECS instance that is in the VPC.
    -   If you do not retain the classic network address, the access from the ECS instance in the classic network to the RDS instance over the internal network is immediately disconnected when you switch the network type. You must configure the VPC address of the RDS instance in the ECS instance that is in the VPC.
    **Note:** If you need to use the ECS instance in the classic network to access the RDS instance in the VPC, you can use the [ClassicLink](../../../../../intl.en-US/VPC network connections/ClassicLink/ClassicLink overview.md#) function or migrate the ECS instance to the VPC.


## Related operations {#section_9ky_y1v_ifu .section}

|Operation|Description|
|---------|-----------|
|[ModifyDBInstanceNetworkType](../intl.en-US/API Reference/Network management/ModifyDBInstanceNetworkType.md#)|Used to switch the network type of an RDS instance.|


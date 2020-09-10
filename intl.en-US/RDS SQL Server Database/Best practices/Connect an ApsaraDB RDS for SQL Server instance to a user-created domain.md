# Connect an ApsaraDB RDS for SQL Server instance to a user-created domain

This topic describes how to deploy a domain controller server on an Elastic Compute Service \(ECS\) instance and connect an ApsaraDB RDS for SQL Server instance to the target domain.

-   The RDS instance runs one of the following SQL Server versions:
    -   SQL Server 2019 SE \(general-purpose or dedicated instance\)
    -   SQL Server 2017 EE or SE \(general-purpose or dedicated instance\)
    -   SQL Server 2016 EE or SE \(general-purpose or dedicated instance\)
    -   SQL Server 2012 EE or SE \(general-purpose or dedicated instance\)
-   The RDS instance and the ECS instance that hosts your domain controller server reside in the same Virtual Private Cloud \(VPC\).
-   The security group of the ECS instance is configured to allow access from the private IP address of the RDS instance. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
-   The private IP address of the RDS instance is allowed by the firewall of the ECS instance. The firewall is disabled by default. If you have enabled the firewall, you must configure the firewall to allow the private IP address of the RDS instance.
-   The domain account belongs to the Domain Admins group because high permissions are required for a client to add a domain.
-   The domain controller server uses the same IP address as the Domain Name System \(DNS\) server.
-   You have logged on to the console by using an Alibaba Cloud account.

**Note:** This function is available only for specific customers. If you want to use this function, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) or submit an application to your customer manager.

Microsoft Active Directory \(AD\) is a directory service for specific Microsoft products, such as Windows Server Standard, Windows Server Enterprise, and Microsoft SQL Server. A directory is a hierarchical structure that stores information about objects on the same local area network \(LAN\). AD stores information about domain accounts, such as usernames, passwords, and phone numbers. It allows authorized users on the same LAN to access its information.

AD is an important component in the Windows ecosystem. Many large enterprises use domain control to plan and implement centralized access management. Domain control is provided by Windows. It has always been a native management method for the enterprises. If you migrate all your businesses from an on-premises environment to the cloud or use a hybrid cloud architecture, make sure that the cloud supports AD for global management. AD support is a key factor to determine whether you can migrate on-premises SQL Server databases to the cloud.

ApsaraDB RDS for SQL Server enables you to connect an RDS instance to a user-created domain.

## Precautions

**Warning:** After this function is enabled, [SLA](http://terms.aliyun.com/legal-agreement/terms/suit_bu1_ali_cloud/suit_bu1_ali_cloud201910310944_35008.html) is not guaranteed.

## Select a Windows version

You must deploy a domain controller server on an ECS instance that runs Windows Server. The minimum requirement for the instance operating system is Windows Server 2012 R2. We recommend that you use Windows Server 2016 or later and select English. The following sections use Windows Server 2016 as an example to describe how to deploy a domain controller server for an RDS instance.

## Procedure

1.  [Deploy a domain controller server on an ECS instance](#section_v9u_b9r_sri)
2.  [Configure a security group for the ECS instance](#section_w3w_z00_bg4)
3.  [Configure the RDS instance](#section_ds5_cby_zmo)

## Deploy a domain controller server on an ECS instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, find the target ECS instance and click its ID.

5.  Log on to the target ECS instance that runs Windows Server 2016.

6.  Search for and open **Server Manager**.

7.  Click **Add roles and features** and configure parameters on the following pages.

    |Page|Description|
    |----|-----------|
    |**Installation Type**|Retain default settings.|
    |**Server Selection**|Retain default settings.|
    |**Server Roles**|    -   Select **Active Directory Domain Services**. In the dialog box that appears, click **Add Features**.
    -   Select **DNS Server**. In the dialog box that appears, click **Add Features**. Make sure that your computer uses a fixed IP address. Otherwise, the DNS server becomes unavailable if the IP address dynamically changes.
![Server Roles](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3459259951/p113917.png) |
    |**Features**|Retain default settings.|
    |**AD DS**|Retain default settings.|
    |**DNS Server**|Retain default settings.|
    |**Confirmation**|Click **Install**.|

8.  After the installation is complete, click **Close**.

9.  In the left-side navigation pane, click **AD DS**. In the upper-right corner of the page, click **More**.

    ![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113918.png)

10. Click **Promote this server to a domain...** and configure parameters on the following pages.

    ![Promote](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113919.png)

    |Page|Description|
    |----|-----------|
    |**Deployment Configuration**|Select **Add a new forest** to set the domain name.![new forest](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113920.png) |
    |**Domain Controller Options**|Set the password for the Directory Services Restore Mode \(DSRM\) mode.![DSRM password](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113921.png) |
    |**DNS Options**|Deselect **Create DNS delegation**.![Deselect](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113922.png) |
    |**Additional Options**|Retain default settings.|
    |**Paths**|Retain default settings.|
    |**Review Options**|Retain default settings.|
    |**Prerequisites Check**|Click **Install**. **Note:** After the installation is complete, the system restarts. |

11. After the system restarts, search for and open **Server Manager** again.

12. In the left-side navigation pane, click **AD DS**. Right-click the target domain controller server and select **Active Directory Users and Computers** to go to the AD user management module.

    ![AD user management](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113923.png)

13. Choose **testdomain.net** \> **Users** \> **New** \> **User**.

14. Set a username and click **Next**.

    ![Username](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113925.png)

15. Set a password, select Password never expires, and click **Next**. Then, click **Finish**.

    ![Set a password](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113926.png)

16. Double-click the newly created user and add it to the Domain Admins group.

    ![Add the user to the administrator group](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113927.png)

    ![Added successfully](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p113928.png)


## Configure a security group for the ECS instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, find the target ECS instance and click its ID.

5.  In the left-side navigation pane, click **Security Groups**. Click **Add Rules**.

    **Note:** Many ports need to be enabled for a domain controller server. We recommend that you configure a separate security group for the domain controller server instead of configuring the domain controller server in the same security group as other ECS instances.

6.  On the **Inbound** tab, click **Add Security Group Rule** to allow the RDS instance to access the ECS instance over the following ports.

    ![Allow RDS to access ECS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p116505.png)

    |Protocol|Port|Description|
    |--------|----|-----------|
    |TCP|88|The port for the Kerberos authentication protocol.|
    |TCP|135|The port for the Remote Procedure Call \(RPC\) protocol.|
    |TCP/UDP|389|The port for the Lightweight Directory Access Protocol \(LDAP\).|
    |TCP|445|The port for the Common Internet File System \(CIFS\) protocol.|
    |TCP|3268|The port for Global Catalog.|
    |TCP/UDP|53|The port for the DNS service.|
    |TCP|49152~65535|The default dynamic port range for connections. Enter a value in the following format: 49152/65535.|


## Configure the RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target instance and click the instance ID.

4.  In the left-side navigation pane, click **Accounts**.

5.  Click the **AD Domain Services** tab and click **Configure AD Domain Services**.

    ![Configure AD Domain Services](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4459259951/p120531.png)

6.  Set the following parameters and select **I have read and understand the impact of AD Domain Services on the RDS Service Level Agreement.**

    **Warning:** After the AD domain function is enabled, [SLA](http://terms.aliyun.com/legal-agreement/terms/suit_bu1_ali_cloud/suit_bu1_ali_cloud201910310944_35008.html) is not guaranteed.

    ![Add a domain](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5459259951/p120541.png)

    |Parameter|Description|
    |---------|-----------|
    |**Domain Name**|The domain name that you specified when you created an AD on the **Deployment Configuration** page. In this example, enter testdomian.net.|
    |**Directory IP Address**|The IP address of the ECS instance where the domain controller server is deployed. You can obtain the IP address by running ipconfig on the ECS instance or by using the ECS console.![View the private IP address](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5459259951/p120538.png) |
    |**Domain Account**|The username that you specified earlier.|
    |**Domain Password**|The password of the username.|

7.  Click **OK** and wait until the domain is added.


## FAQ

Which RDS account can I use to connect my RDS instance to a domain? How do I control the account permissions?

We recommend that you use an account with the domain administrator permissions. If you do not want to use the domain administrator permissions, you can use the least permissions by performing the following operations. However, if you use the least permissions, you must manually remove your computer from the domain controller server when you exit the domain. Otherwise, an error is reported if you reconnect your RDS instance \(the same original RDS instance\) to this domain.

1.  After you create a user and confirming that the user belongs to the Domain Admins group, choose **Computers** \> **Delegate Control...** to add the newly created user.

    ![Control permissions 1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5459259951/p114804.png)

    ![Control permissions 2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5459259951/p114805.png)

2.  Right-click the newly created user and select **Create a custom task to delegate**. Click **Next**.
3.  Select **Only the following objects in the folder** and the red highlighted items in the following figure. Click **Next**.

    ![Control permissions 3](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5459259951/p114823.png)

4.  Select the items as shown in the following figure. Click **Next** until the procedure is complete.

    ![Control permissions 4](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5459259951/p114824.png)



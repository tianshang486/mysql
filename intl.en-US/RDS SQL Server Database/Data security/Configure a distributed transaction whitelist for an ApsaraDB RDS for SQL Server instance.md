# Configure a distributed transaction whitelist for an ApsaraDB RDS for SQL Server instance

Distributed transaction whitelists allow for distributed transactions between an Elastic Compute Service \(ECS\) instance and an ApsaraDB RDS for SQL Server instance.

For more information about the related best practices, see [Connect Kingdee K/3 WISE to ApsaraDB RDS for SQL Server](/intl.en-US/RDS SQL Server Database/Best practices/Connect Kingdee K/3 WISE to ApsaraDB RDS for SQL Server.md).

## Prerequisites

The RDS instance runs one of the following SQL Server versions on RDS High-Availability Edition: 2012 SE, 2012 EE, 2014 SE, 2016 SE, 2016 EE, and 2017 SE.

## Configure the RDS instance

1.  Log on to the [ApsaraDB for RDS console](https://rdsnext.console.aliyun.com/).
2.  In the top navigation bar, select the region where the target RDS instance resides.
3.  Find the target RDS instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the Whitelist Settings tab, select a whitelist and click **Edit** to the right. In the dialog box that appears, enter the IP address of the ECS instance.

    **Note:**

    -   If the ECS and RDS instances reside in the same VPC, you must enter the private IP address of the ECS instance. You can view the private IP address of the ECS instance on the Instance Details page of the ECS instance in the ECS console.
    -   If the ECS and RDS instances reside in different VPCs, you must enter the public IP address of the ECS instance. In addition, you must apply for a public endpoint for the RDS instance. For more information, see [Apply for a public endpoint for an RDS SQL Server instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for a public endpoint for an RDS SQL Server instance.md).
6.  Click **Add**.
7.  Click the Whitelist for Distributed Transaction tab.
8.  Click **Create Whitelist**.
9.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Group Name**|Enter the name of the whitelist. The name must be 2 to 32 characters in length. It can contain digits, lowercase letters, and underscores \(\_\). It must start with a lowercase letter and end with a lowercase letter or digit.|
    |**Whitelist**|Enter the IP address of the ECS instance and the name of the Windows-based computer where the ECS instance resides. Make sure that you separate the IP address and the computer name with a comma \(,\). Example: 192.168.1.100,k3ecstest. If you want to enter more than one entry, make sure that each entry is in a different line.

**Note:** You can view the computer name by choosing **Control Panel** \> **System and Security** \> **System** on your computer. |

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50883.png)

10. Click **OK**.

## Configure the ECS instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the top navigation bar, select the region where the target ECS instance resides.
4.  Find the target ECS instance and click its instance ID.
5.  In the left-side navigation pane, click **Security Groups**.
6.  Find the target security group and in the Actions column and click **Add Rules**.
7.  On the **Inbound** tab, click **Add Security Group Rule**.
8.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Action**|Select **Allow**.|
    |**Priority**|Retain the default value 1.|
    |**Protocol Type**|Select **Custom TCP**.|
    |**Port Range**|Enter **135**. **Note:** Port 135 is the fixed port for the RPC service. |
    |**Authorization Object**|The two IP addresses of the RDS instance. To obtain these IP addresses, perform the following steps: Log on to the ApsaraDB for RDS console and navigate to the **Whitelist for Distributed Transaction** tab of the **Data Security** page for the RDS instance.![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50892.png) |
    |**Description**|Enter the description of the security group rule. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|

9.  Click **OK**.
10. Add another security group rule. This rule has the same parameter settings as the previous rule except the **Port Range** parameter that is set to **1024/65535**.


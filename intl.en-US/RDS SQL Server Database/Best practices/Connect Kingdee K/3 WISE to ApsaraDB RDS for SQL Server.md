# Connect Kingdee K/3 WISE to ApsaraDB RDS for SQL Server

This topic describes how to connect an Elastic Cloud Service \(ECS\) instance that runs Kingdee K/3 WISE 15.0 or 15.1 to an ApsaraDB RDS for SQL Server instance. After the connection is established, you can run distributed transactions between the RDS instance and the ECS instance.

## Solution

This solution consists of three steps:

1.  Upload a full backup file of the specified Kingdee K/3 WISE set of books to an Object Storage Service \(OSS\) bucket. Then, restore the data from the full backup file to the RDS instance. For more information, see [\#section\_jk1\_kdq\_mdl](#section_jk1_kdq_mdl).
2.  Modify the access settings of the RDS instance, ECS instance, and Windows operating system. This allows you to smoothly run distributed transactions between the RDS instance and the ECS instance. For more information, see [\#section\_jqg\_mfn\_abz](#section_jqg_mfn_abz).
3.  Replace the old accounting data management tool with a new one that is compatible with ApsaraDB RDS for SQL Server. For more information, see [\#section\_qnz\_69u\_5xl](#section_qnz_69u_5xl).

## Before you begin

-   Install Kingdee K/3 WISE on an ECS instance that runs Windows Server 2016.
-   Create an RDS instance. For more information, see [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md).
-   Obtain the full backup data of the Kingdee K/3 WISE set of books.

**Note:**

-   The ECS instance on which Kingdee K/3 WISE is installed must reside in the same region and virtual private cloud \(VPC\) as the RDS instance.For more information, see [Overview of VPCs and VSwitches](https://www.alibabacloud.com/help/zh/doc-detail/100380.htm).
-   The RDS instance must run one of the following SQL Server versions and RDS editions:
    -   SQL Server 2017 on RDS Basic Edition
    -   SQL Server 2012 or 2016 EE on RDS High-availability Edition
    -   SQL Server 2012 or 2016 on RDS Basic Edition

## Restore data to the RDS instance

**Perform the following steps to upload a full backup file of the set of books to an OSS bucket:**

1.  Log on to the [OSS console](https://oss.console.aliyun.com/overview).
2.  In the right-side pane, click **Create Bucket**.
3.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Bucket Name**|Enter the name for the bucket.|
    |**Region**|Select the region where the bucket resides. Make sure that the bucket resides in the same region as the ECS and RDS instances.|
    |**Storage Class**|Select **IA**.|
    |**Zone-redundant Storage**|Select **Disable**.|
    |**Versioning**|Select **Disable**.|
    |**Access Control List \(ACL\)**|Select **Private**.|
    |**Encryption Method**|Select **None**.|
    |**Real-time Log Query**|Select **Disable**.|
    |**Scheduled Backup**|Select **Disable**.|

    **Note:** For more information about the parameters, see[Create a bucket](https://www.alibabacloud.com/help/zh/doc-detail/31885.htm).

4.  Click **OK**.
5.  In the left-side navigation pane, click **Buckets**. On the page that appears, click the bucket that you created.
6.  In the left-side navigation pane of the page that appears, click **Files**. On the page that appears, click **Upload**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50848.png)

7.  Drag the full backup file to upload to the **Upload** section. Alternatively, click **Upload** in the Upload section and select the backup file.

    **Note:** For more information about the parameters, see[Upload an object](https://www.alibabacloud.com/help/zh/doc-detail/31886.htm).

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50849.png)


**Perform the following steps to create a privileged account for the RDS instance:**

1.  Log on to the [ApsaraDB RDS console](https://rdsnext.console.aliyun.com/).
2.  In the top navigation bar, select the region where the RDS instance resides.
3.  Find the RDS instance and click its ID.
4.  In the left-side navigation pane, click **Accounts**.
5.  Click **Create Account**.
6.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Account**|Enter the username of the account. The username must be 2 to 16 characters in length and can contain lowercase letters, digits, and underscores \(\_\). It must start with a lowercase letter and end with a lowercase letter or digit.|
    |**Account Type**|Specify the type of the account. Select **Privileged Account**.|
    |**Password**|Enter the password of the account. The password must meet the following requirements:     -   The password must be 8 to 32 characters in length.
    -   The password must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters.
    -   Special characters include ! @ \# $ % ^ & \* \( \) \_ + - = |
    |**Re-enter Password**|Enter the password of the account again.|
    |**Description**|Enter a description that helps identify the account.|

7.  Click **OK**.

**Perform the following steps to migrate the full backup file from the OSS bucket to the RDS instance:**

1.  Log on to the [ApsaraDB RDS console](https://rdsnext.console.aliyun.com/).
2.  In the top navigation bar, select the region where the RDS instance resides.
3.  Find the RDS instance and click its ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  In the upper-right corner of the page, click **Migrate OSS Backup Data to RDS**.

    **Note:** If this button does not exist, check whether the SQL Server version and edition of the RDS instance meet requirements. For more information, see the ["Before you begin"](#section_dqu_ia9_hgl) section of this topic.

6.  Click **Next** twice to go to the **Import Data** step.
7.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Name**|Enter the name of the destination database on the RDS instance.|
    |**OSS Bucket**|Select the OSS bucket where the full backup file is stored.|
    |**OSS Subfolder Name**|Enter the name of the subfolder where the full backup file is stored.|
    |**OSS File**|Enter the prefix in the name of the full backup file and click the search button. A list of files appears. The list contains the name, size, and update time of each file that matches the query. Select the full backup file that you want to migrate to the RDS instance.|
    |**Cloud Migration Method**|Select **Immediate Access \(Full Backup\)**.|
    |**Consistency Check Mode**|Select **Synchronous DBCC**.|

    **Note:** If you are migrating backup data from OSS to ApsaraDB RDS for the first time, the system prompts you to authorize the OSS access permission to your Alibaba Cloud account. In this case, you only need to click **Authorize** and configure **Confirm Authorization Policy**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50875.png)

8.  Click **OK**.

    **Note:** Wait until the full backup file is imported into the destination database on the RDS instance. You can click Databases in the left-side navigation pane to view the status of the destination database.


## Enable distributed transactions

**Perform the following steps to configure the RDS instance:**

1.  Log on to the [ApsaraDB RDS console](https://rdsnext.console.aliyun.com/).
2.  In the top navigation bar, select the region where the RDS instance resides.
3.  Find the RDS instance and click its ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  Find the specified IP address whitelist and click **Edit** on the right. In the dialog box that appears, enter the IP address of the ECS instance.

    **Note:**

    -   If the ECS and RDS instances belong to the same VPC, enter the private IP address of the ECS instance. You can view the private IP address on the Instance Details page for the ECS instance in the ECS console.
    -   If the ECS and RDS instances reside in different VPCs, enter the public IP address of the ECS instance and apply for a public endpoint for the RDS instance. For more information, see [Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Database connection/Apply for or release a public endpoint on an ApsaraDB RDS for SQL Server instance.md).
6.  Click **OK**.
7.  Click the Whitelist for Distributed Transaction tab.
8.  Click **Create Whitelist**.
9.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Group Name**|Enter the name of the whitelist. The name must be 2 to 32 characters in length and can contain digits, lowercase letters, and underscores \(\_\). It must start with a lowercase letter and end with a lowercase letter or digit.|
    |**Whitelist**|Enter the IP address of the ECS instance and the name of the Windows-based computer where the ECS instance resides. Make sure that you separate the IP address and the computer name with a comma \(,\). Example: 192.168.1.100,k3ecstest. Enter multiple entries in different lines.

**Note:** You can view the computer name by choosing **Control Panel** \> **System and Security** \> **System**. |

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50883.png)

10. Click **OK**.

**Perform the following steps to configure the ECS instance:**

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  In the left-side navigation pane, click Instances. In the top navigation bar, select the region where the ECS instance resides.
3.  Find the ECS instance and click its ID.
4.  In the left-side navigation pane, click **Security Groups**.
5.  Find the security group and in the Actions column click **Add Rules**.
6.  In the upper-right corner of the page, click **Add Security Group Rule.**
7.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Rule Direction**|Select **Inbound**.|
    |**Action**|Select **Allow**.|
    |**Protocol Type**|Select **Custom TCP**.|
    |**Port Range**|Enter **135**. **Note:** Port 135 is the fixed port for the RPC service. |
    |**Priority**|Enter **1**.|
    |**Authorization Type**|Select **IPv4 CIDR Block**.|
    |**Authorization Object**|Enter the two IP addresses of the RDS instance in the **Authorization Objects** field. You can view these IP addresses on the **Whitelist for Distributed Transaction** tab of the **Data Security** page in the ApsaraDB RDS console.![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50892.png) |
    |**Description**|Enter a description that helps identify the rule. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|

8.  Click **OK**.
9.  Add another security group rule. This rule has the same parameter settings as the previous rule except the **Port Range** parameter that is set to **1024/65535**.

**Perform the following steps to configure your Windows operating system:**

1.  Log on to the Windows Server 2016 operating system.
2.  Open the hosts file in the C:\\Windows\\System32\\drivers\\etc\\hosts path.
3.  Enter the two IP addresses of the RDS instance at the end of the hosts file. You can view these IP addresses on the **Whitelist for Distributed Transaction** tab of the **Data Security** page in the ApsaraDB RDS console.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50898.png)

4.  Save the hosts file.
5.  Choose **Control Panel** \> **System and Security** \> **Administrative Tools** and double-click **Component Services**.
6.  Choose **Component Services** \> **Computer** \> **My Computer** \> **Distributed Transaction Coordinator**.
7.  Right-click **Local DTC** and select **Properties**.
8.  Click the Security tab and configure the parameters.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7459259951/p50903.png)

9.  Click **OK**. In the MSDTC Service message, click **Yes**. Then, wait for the MSDTC service to restart.

## Initialize the new accounting data management tool

1.  Download the software package of the accounting data management tool that is used with Kingdee K/3 WISE 15.1 or 15.0.

    -   [Kingdee K/3 WISE 15.1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/128809/cn_zh/1565162995121/K3WISE15.1%20ForRDS.rar)
    -   [Kingdee K/3 WISE 15.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/128809/cn_zh/1565162975502/K3WISE15.0%20ForRDS.rar)
    **Note:** Different Kingdee K/3 WISE versions require different accounting data management tool. Only the account set management tools of Kingdee K/3 WISE 15.0 and 15.1 are provided.

2.  Decompress the package and save it to the following installation directory of Kingdee K/3 WISE: K3ERP\\KDSYSTEM\\KDCOM.
3.  Open Kingdee K/3 WISE.
4.  In the dialog box that appears, configure the identity verification and data server information.

    **Note:** Configure the internal endpoint of the RDS instance for the data server.

5.  Configure the preset connection.
6.  Register the set of books.
7.  Select the specified database.

## Log on to Kingdee K/3 WISE

After all the settings are complete, you can run distributed transactions between the ECS and RDS instances. In addition, you can then log on to and use Kingdee K/3 WISE.


# Clone RDS instances {#reference_pys_54l_12b .reference}

## Description {#section_l21_v32_12b .section}

A new instance with the historical data is cloned based on the backup file of an existing instance or a specified time. The new instance has the same whitelist settings, SQL audit settings, threshold value alarm settings, backup settings, and parameter settings as the existing instance. The data and accounts in the new instance are the same as the historical data in the backup file.

When you create a clone instance, the master instance must meet the following conditions:

-   The instance is running and not locked.
-   The instance does not have an ongoing migration task.
-   To clone an instance by time, log backup must have been enabled.
-   To clone an instance by using a backup set, the master instance must have at least one backup set.

    **Note:** To create a clone instance using a sub-account, ensure that you have authorized the sub-account. For more information, see [Authorization for RDS instances](https://www.alibabacloud.com/help/doc-detail/58932.htm?spm=a2c63.p38356.a3.1.10a75f7dcY4IPE).


## Request parameters {#section_qzx_w32_12b .section}

|Name|Type|Required or not|Description|
|----|----|---------------|-----------|
|Action|String|Yes|Required parameter; value: CloneDBInstance|
|DBInstanceId|String|Yes|Instance ID|
|BackupId|String|No| -   Backup set ID, which is obtained through DescribeBackups, the API for backup list query.
-   Either **BackupId** or **RestoreTime** is required.

 |
|RestoreTime|String|No| -   The arbitrary time specified by user during the backup retention period, for example, 2011-06-11T16:00:00Z.
-   Either **BackupId** or **RestoreTime** is required.

 |
|PayType|String|Yes|Billing method. Value range: -   Postpaid: Pay-As-You-Go
-   Prepaid: Subscription

 |
|Period|String|No| -   This input parameter is required if **PayType** is set to Subscription.
-   The pre-payment methods include:
-   Year: yearly subscription
-   Month: monthly subscription

 |
|UsedTime|String|No|Subscription type. -   This input parameter is required if **PayType** is set to Prepaid.
-   This parameter indicates the duration for purchase, which can be 1, 2, 3, or other numeric values as required.

 |
|DBInstanceClass|String|No| -   Instance type. For more information, see [Instance type list](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#)
-   This parameter is optional. If it is unavailable, the new instance and the master instance are of the same type.

 |
|DBInstanceStorage|String|No| -   Disk space. Unit: GB. By default, the disk space for the new instance is the same as that for the master instance. The parameter value is increased at a step of 5 GB.
-   For RDS instances with exclusive storage space on a physical machine, the parameter value range is \[3000, 3000\].
-   For other instance types, the parameter value range is \[5, 2000\].

 |
|InstanceNetworkType|String|No|Network type. Value range: -   Classic: classic network
-   VPC: VPC
-   By default, the new instance and the master instance are of the same network type.

 |
|VPCId|String|No|VPC ID|
|VSwitch ID|String|No|VSwitich ID|
|PrivateIpAddress|String|No|IP address of a VPC under VSwitchId. If no value is set, the system automatically assigns a VPC IP address.|

## Return parameters {#section_a5x_zlh_12b .section}

|Name|Type|Description|
|----|----|-----------|
|<Common response parameters\>|-|Fore more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|DBInstanceId|-|Instance ID|
|OrderId|-|Order ID|


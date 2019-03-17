# DescribeBackupTasks {#reference_w3d_xvj_n2b .reference}

This API is used to show the backup task list.

## Request parameters {#section_bvb_kwj_n2b .section}

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Action|String|Yes|Required parameter. Value: DescribeBackupTasks|
|DBInstanceId|String|Yes|Instance ID|
|BackupJobId|String|No|Backup task ID.|

## Response parameters {#section_ugq_nwj_n2b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|<Common response parameters\>|String|See [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|Items|List|List of backup tasks.|

**Items**

|Parameter|Type|Description|
|---------|----|-----------|
|BackupStatus|String|Backup task status:-   NoStart
-   Preparing
-   Waiting
-   Uploading
-   Checking
-   Finished

|
|BackupJobId|String|Backup task ID.|


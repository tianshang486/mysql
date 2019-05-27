# RAM authorization {#reference_lnh_1mn_12b .reference}

## Description {#section_l21_v32_12b .section}

Your Alibaba Cloud account has full access to all resources under the account.

You can grant the access and management permissions to sub-accounts \(which are also called RAM users\) by creating an authorization policy. In an authorization policy, an Alibaba Cloud Resource Name \(ARN\) is used as the unique identifier of resources. This topic introduces the format of ARNs.

**Note:** For RDS, the resources are **dbinstance**.

 

## Request parameters {#section_hml_w7d_nxc .section}

|Resource type|ARN format|
|-------------|----------|
|dbinstance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid acs:rds:$regionid:$accountid:dbinstance/

 acs:rds:::dbinstance/

 |

**Parameters**

|Parameter|Description|
|---------|-----------|
| ``` {#codeblock_vxm_uht_13f}
$regionid
```

 |Region ID, which can be replaced with `*`|
| ``` {#codeblock_tk6_o1x_d0n}
$dbinstanceid
```

 |Instance ID, which can be replaced with `*`|
| ``` {#codeblock_4tp_mdf_cu8}
$accountid
```

 |Alibaba Cloud account ID, which can be replaced with `*`|

## RDS API authenication rules {#section_b9c_dvo_ysi .section}

When you use a RAM user account to access RDS through an API, RDS checks whether the RAM user has permissions. The following table lists the authentication rules.

|API|Authenication rule|
|---|------------------|
|CreateDBInstance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DeleteDBInstance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeDBInstances|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|SwitchDBInstanceNetType|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyDBInstanceDescription|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyDBInstanceMaintainTime|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|PurgeDBInstanceLog|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DeleteDatabase|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyDBDescription|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeFilesForSQLServer|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeImportsForSQLServer|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CancelImport|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ResetAccountPassword|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|RevokeAccountPrivilege|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DeleteAccount|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreateBackup|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreateTempDBInstance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyBackupPolicy|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeDBInstancePerformance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeSlowLogRecords|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeBinlogFiles|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeSQLLogRecords|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeOptimizeAdviceOnMissPK|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeOptimizeAdviceOnMissIndex|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeParameters|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreatePrepaidDBInstanceForChannel|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyPrepaidDBInstanceSpec|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreatePostpaidDBInstanceForChannel|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyPostpaidDBInstanceSpec|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeDBInstanceAttribute|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|RestartDBInstance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifySecurityIps|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|UpgradeDBInstanceEngineVersion|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreateDatabase|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeDatabases|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreateUploadPathForSQLServer|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ImportDataBaseBetweenInstances|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|CreateAccount|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|GrantAccountPrivilege|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeAccounts|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyAccountDescription|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeBackups|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeBackupPolicy|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeResourceUsage|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeSlowLogs|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeErrorLogs|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeSQLLogReports|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeOptimizeAdviceOnStorage|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeOptimizeAdviceOnExcessIndex|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|DescribeOptimizeAdviceByDBA|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|
|ModifyeParameter|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid|


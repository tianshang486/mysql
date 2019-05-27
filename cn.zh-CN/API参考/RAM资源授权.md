# RAM资源授权 {#reference_lnh_1mn_12b .reference}

## 描述 {#section_l21_v32_12b .section}

您通过云账号创建的RDS实例，都是该账号自己拥有的资源。默认情况下，账号对自己的资源拥有完整的操作权限。

通过使用阿里云的RAM（Resource Access Management）服务，您可以将您云账号下RDS资源的访问及管理权限授予RAM中的子用户。

目前，可以在RAM中进行授权的资源类型只有dbinstance。在通过RAM进行授权时，资源的描述方式如下：

## 请求参数 {#section_qzx_w32_12b .section}

|资源类型|授权策略中的资源描述方式|
|----|------------|
|dbinstance|acs:rds:$regionid:$accountid:dbinstance/$dbinstanceid acs:rds:$regionid:$accountid:dbinstance/

 acs:rds:::dbinstance/

 |

**参数说明：**

|参数名称|说明|
|----|--|
| ```
$regionid
```

 |地域的ID，可以用`*`代替。|
| ```
$dbinstanceid
```

 |实例的名称，可以用`*`代替。|
| ```
$accountid
```

 |云账号的数字ID，可以用`*`代替。|

## RDS API的鉴权规则 {#section_uwr_fmn_12b .section}

当子用户通过API访问RDS时，RDS后台会向RAM进行权限检查，以确保调用者拥有相应权限。每个API会根据涉及到的资源以及API的语义来确定需要检查哪些资源的权限。每个API的鉴权规则如下表所示：

|API|鉴权规则|
|---|----|
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


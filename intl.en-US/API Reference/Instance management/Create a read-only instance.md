# Create a read-only instance {#reference_ljz_xdf_12b .reference}

## Description {#section_l21_v32_12b .section}

This API is used to create a read-only instance for an RDS instance.

Number of read-only instances：

-   If the memory of the master instance is greater than or equal to 64 GB, the master instance can have up to ten read-only instances.
-   If the memory of the master instance is less than 64 GB, the master instance can have up to five read-only instances.

-   The master instance must be one of the following:
    -   MySQL 5.6
    -   MySQL 5.7 High-Availability Edition based on local SSDs

## Request parameters {#section_qzx_w32_12b .section}

|Name|Type|Required or not|Description|
|----|----|---------------|-----------|
|Action|String|Yes|Required parameter. Value: CreateReadOnlyDBInstance.|
|RegionId|String|Yes|Region ID, which must be the same as the region of the master instance. You can use the API DescribeRegions to view the region ID list.|
|ZoneId|String|Yes|Zone ID. You can use the API DescribeRegions to view the zone ID list.|
|DBInstanceId|String|Yes|ID of the master instance.|
|EngineVersion|String|Yes|Database version, which must be the same as that of the master instance.-   5.6
-   5.7

|
|DBInstanceClass|String|Yes|Instance type. For more information, see [Instance type list](../../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).|
|DBInstanceStorage|Integer|Yes|User-defined storage space. Value range: \[5, 1000\], 5 GB increments. Unit: GB.|
|DBInstanceDescription|String|No| -   Instance description or remarks, no more than 256 bytes. 
-   It cannot begin with http:// or https://. It must start with a Chinese character or an English letter.  It may contain Chinese and English characters/letters, “\_”, “-“, and numbers. The length may be 2-256 characters.

 |
|PayType|String|Yes|Value: Postpaid|
|ClientToken|String|No|Used to guarantee idempotence.|
|InstanceNetworkType|String|No|If no value is specified, a classic instance is created by default.-   VPC: VPC
-   Classic: classic network

|
|VPCId|String|No|VPC ID.|
|VSwitchId|String|No|VSwitch ID.|
|PrivateIpAddress|String|No|IP address of an VPC under VSwitchId. If no value is specified, the system automatically assigns a VPC IP address based on VPCId and VSwitchId.|

## Return parameters {#section_rpk_z32_12b .section}

|Name|Type|Description|
|----|----|-----------|
|<Public return parameters\>|-|For more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|DBInstanceId|String|DB instance ID|
|OrderId|String|Order ID|
|ConnectionString|String|Database connection address|
|Port|String|Port connecting to the database|

## Request example {#section_l4g_pj2_12b .section}

```
https://rds.aliyuncs.com/?Action=CreateReadOnlyDBInstance
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&DBInstanceId=rdsaiiabnaiiabn
&EngineVersion=5.6
&DBInstanceClass=rds.mys2.small
&DBInstanceStorage=10
&PayType=Postpaid
&ClientToken=ETnLKlblzczshOTUbOCziJZNwHlYBQ
&<[Public Request Parameters]>
```

## Return example {#section_xtg_rj2_12b .section}

**XML format**

```
<CreateDBInstanceResponse>
     <OrderId>100789370230206</OrderId>
     <ConnectionString>rdsaiiabnaiiabn.mysql.rds.aliyuncs.com </ConnectionString>
     <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
     <port>3306</port>
     <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId>
</CreateDBInstanceResponse>
```

**JSON format**

```

    "OrderId": "100789370230206", 
    "ConnectionString": "rdsaiiabnaiiabn.mysql.rds.aliyuncs.com", 
    "DBInstanceId": "rdsaiiabnaiiabn", 
    "Port": "3306", 
    "RequestId": "1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
   
```


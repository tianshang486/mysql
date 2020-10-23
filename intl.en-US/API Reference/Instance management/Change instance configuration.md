# Change instance configuration

You can call the ModifyDBInstanceSpec operation to change the instance type or storage capacity of an ApsaraDB RDS instance.

Before you call this operation, make sure that the following requirements are met:

-   The instance must be in the Running state.
-   The instance cannot have ongoing backup tasks.
-   At least one of the DBInstanceClass and DBInstanceStorage parameters must be specified in the request.
-   If you want to decrease the storage capacity, the specified storage capacity must be greater than or equal to 1.1 times the used storage capacity.
-   The instance must be a primary or read-only instance. This operation is not supported for disaster recovery or temporary instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceSpec&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBInstanceSpec|The operation that you want to perform. Set the value to **ModifyDBInstanceSpec**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|PayType|String|Yes|Postpaid|The billing method of the instance. Valid values:

 -   **Postpaid**: pay-as-you-go
-   **Prepaid**: subscription |
|ZoneId|String|No|cn-hangzhou-b|The ID of the zone to which the instance belongs. |
|DBInstanceClass|String|No|rds.mys2.small|The instance type of the instance. For more information, see [Primary instance types](~~26312~~).

 **Note:** You must specify at least one of the **DBInstanceClass** and **DBInstanceStorage** parameters. |
|DBInstanceStorage|Integer|No|20|The storage capacity that you want to specify. Unit: GB. The storage capacity increases at increments of 5 GB. For more information, see [Primary instance types](~~26312~~).

 **Note:** You must specify at least one of the **DBInstanceClass** and **DBInstanceStorage** parameters. |
|EffectiveTime|String|No|MaintainTime|The time when you want the change to take effect. Valid values:

 -   **Immediate**: The change takes effect immediately.
-   **MaintainTime**: The change takes effect during the specified maintenance window. For more information, see [ModifyDBInstanceMaintainTime](~~26249~~).

 Default value: **Immediate**. |
|EngineVersion|String|No|5.6|The database engine version that the instance runs. Valid values:

 -   MySQL: **5.5, 5.6, 5.7, and 8.0**
-   SQLServer: **2008r2, 2012, 2012\_ent\_ha, 2012\_std\_ha, 2012\_web, 2014\_std\_ha, 2016\_ent\_ha, 2016\_std\_ha, 2016\_web, and 2017\_ent**
-   PostgreSQL: **9.4 and 10.0**
-   PPAS: **9.3 and 10.0**
-   MariaDB: **10.3** |
|DBInstanceStorageType|String|No|local\_ssd|The storage type of the instance. Valid values:

 -   **local\_ssd** or **ephemeral\_ssd**: local SSD
-   **cloud\_ssd**: standard SSD
-   **cloud\_essd**: enhanced SSD |
|Direction|String|No|Up|The type of configuration change that you want to perform on the instance. Valid values:

 -   **Up**: upgrades a subscription instance. This value can also specify to upgrade or downgrade a pay-as-you-go instance.
-   **Down**: downgrades a subscription instance.

 Default value: **Up**. |
|SourceBiz|String|No|N/A|This parameter is deprecated. |
|DedicatedHostGroupId|String|No|dhg-7a9xxxxxxxx|The ID of the dedicated cluster to which the instance belongs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3C5CFDEE-F774-4DED-89A2-1D76EC63C575|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBInstanceSpec
&DBInstanceId=rm-uf6wjk5xxxxxxx
&PayType=Postpaid
&DBInstanceClass=rds.mys2.small
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBInstanceSpecResponse>
         <RequestId>3C5CFDEE-F774-4DED-89A2-1D76EC63C575</RequestId>
</ModifyDBInstanceSpecResponse>
```

`JSON` format

```
{
  "RequestId": " 3C5CFDEE-F774-4DED-89A2-1D76EC63C575 "
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


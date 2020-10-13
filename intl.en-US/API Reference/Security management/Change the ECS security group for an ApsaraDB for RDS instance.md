# Change the ECS security group for an ApsaraDB for RDS instance

Changes the ECS security groups to which an ApsaraDB for RDS instance is added.

After an RDS instance is added to an ECS security group, all ECS instances in the security group can access the RDS instance. For more information, see [Configure a whitelist for an RDS instance](~~96118~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifySecurityGroupConfiguration&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySecurityGroupConfiguration|The operation that you want to perform. Set the value to **ModifySecurityGroupConfiguration**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx|The ID of the instance. |
|SecurityGroupId|String|Yes|sg-xxxxxxx|The ID of the ECS security group. Each RDS instance can be added to up to three security groups. Separate the security group IDs with commas \(,\). To delete an ECS security group for the RDS instance, leave this parameter empty. You can call the [DescribeSecurityGroups](~~25556~~) operation to query the ECS security group list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceName|String|rm-uf6wjk5xxxxxx|The ID of the instance. |
|Items|Array of EcsSecurityGroupRelation| |An array that consists of ECS security groups. |
|EcsSecurityGroupRelation| | | |
|NetworkType|String|VPC|The network type of an ECS security group. Valid values:

 -   **Classic**
-   **VPC** |
|RegionId|String|cn-hangzhou|The ID of the region. |
|SecurityGroupId|String|sg-xxxxxxx|The ID of the ECS security group. |
|RequestId|String|8585861B-8F0D-4D17-9460-C42255EB10C0|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/Action=ModifySecurityGroupConfiguration
&DBInstanceId=rm-uf6wjk5xxxxxx
&SecurityGroupId=sg-xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifySecurityGroupConfigurationResponse>
  <Items>
        <EcsSecurityGroupRelation>
              <NetworkType>VPC</NetworkType>
              <SecurityGroupId>sg-1xxxxxxx</SecurityGroupId>
              <RegionId>cn-hangzhou</RegionId>
        </EcsSecurityGroupRelation>
        <EcsSecurityGroupRelation>
              <NetworkType>VPC</NetworkType>
              <SecurityGroupId>sg-2xxxxxxx</SecurityGroupId>
              <RegionId>cn-hangzhou</RegionId>
        </EcsSecurityGroupRelation>
  </Items>
  <RequestId>8585861B-8F0D-4D17-9460-C42255EB10C0</RequestId>
  <DBInstanceName>rm-uf6wjk5xxxxxx</DBInstanceName>
</ModifySecurityGroupConfigurationResponse>
```

`JSON` format

```
{"Items":
	{"EcsSecurityGroupRelation":
		[{"NetworkType":"VPC",
		  "SecurityGroupId":"sg-1xxxxxxx",
		  "RegionId":"cn-hangzhou"},
		 {"NetworkType":"VPC",
		  "SecurityGroupId":"sg-2xxxxxxx",
		  "RegionId":"cn-hangzhou"}]},
 "RequestId":"8585861B-8F0D-4D17-9460-C42255EB10C0",
 "DBInstanceName":"rm-uf6wjk5xxxxxx"}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


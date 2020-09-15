# Modify security groups

Modifies the ECS security groups associated with an ApsaraDB for RDS instance.

After an ECS security group is added to a whitelist of an RDS instance, all of the ECS instances in the ECS security group are granted access to the RDS instance. For more information, see [Configure a whitelist for an RDS MySQL instance](~~96118~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifySecurityGroupConfiguration&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySecurityGroupConfiguration|The operation that you want to perform. Set the value to **ModifySecurityGroupConfiguration**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx|The ID of the RDS instance. |
|SecurityGroupId|String|Yes|sg-xxxxxxx|The ID of the ECS security groups. Each RDS instance can be associated with up to three ECS security groups. You must separate them with commas \(,\). To delete an ECS Security group, leave this parameter empty. You can call the [DescribeSecurityGroups](~~25556~~) operation to query the available ECS security group list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8585861B-8F0D-4D17-9460-C42255EB10C0|The ID of the request. |
|DBInstanceName|String|rm-uf6wjk5xxxxxx|The ID of the RDS instance. |
|Items|Array| |An array that consists of ECS security groups. |
|RegionId|String|cn-hangzhou|The ID of the region to which the ECS security group belongs. |
|SecurityGroupId|String|sg-xxxxxxx|The ID of the ECS security group. |
|NetworkType|String|VPC|The network type of the ECS security group. Valid values:

-   **Classic**
-   **VPC** |

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


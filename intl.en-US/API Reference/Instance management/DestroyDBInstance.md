# DestroyDBInstance {#reference_xsl_xvw_k2b .reference}

This API is used to destroy RDS instances. This API is no longer supported.

**Note:** This API is no longer supported.

Prerequisite: The instance is locked.

## Request parameters {#section_gqn_tww_k2b .section}

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Action|String|Yes|Action to perform. Value: DestroyDBInstance|
|DBInstanceId|String|Yes|Instance ID.|
|AccessKeyId|String|No|AccessKey ID used to access Alibaba Cloud services.|
|ClientToken|String|No|Used to guarantee idempotence.|
|OwnerAccount|String|No|Your AlibabaCloud account used to log in to the RDS console.|

## Response parameters {#section_ffw_dxw_k2b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|RequestId|String|Request ID.|

## Request example {#section_ftl_gxw_k2b .section}

```
https://rds.aliyuncs.com/?Action=DestroyDBInstance
&amp;DBInstanceId=rdsaiiabnaiiabn
&amp;&lt;[Common response parameter]&gt;
```

## Response example {#section_vv5_hxw_k2b .section}

**JSON format**

```
{
"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```


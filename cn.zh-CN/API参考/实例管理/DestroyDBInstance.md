# DestroyDBInstance {#reference_xsl_xvw_k2b .reference}

该接口用于销毁RDS实例，已下线。

## 描述 {#section_pjs_nww_k2b .section}

要求实例状态为锁定中，否则操作将失败。

**说明：** 该API已下线。

## 请求参数 {#section_gqn_tww_k2b .section}

|参数|类型|是否必选|描述|
|--|--|----|--|
|Action|String|是|系统规定参数，取值为：DestroyDBInstance|
|DBInstanceId|String|是|实例的ID。|
|AccessKeyId|String|否|阿里云颁发给用户访问服务所用的密钥ID。|
|ClientToken|String|否|用于保证幂等性。|
|OwnerAccount|String|否|您登录阿里云RDS控制台的主账号。|

## 返回参数 {#section_ffw_dxw_k2b .section}

|参数|类型|描述|
|--|--|--|
|RequestId|String|请求ID。|

## 请求示例 {#section_ftl_gxw_k2b .section}

```
https://rds.aliyuncs.com/?Action=DestroyDBInstance
&amp;DBInstanceId=rdsaiiabnaiiabn
&amp;&lt;[公共请求参数]&gt;
```

## 返回示例 {#section_vv5_hxw_k2b .section}

**JSON 格式**

```
{
"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```


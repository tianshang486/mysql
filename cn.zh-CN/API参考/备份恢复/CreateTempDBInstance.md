# CreateTempDBInstance {#doc_api_Rds_CreateTempDBInstance .reference}

调用CreateTempDBInstance接口创建临时实例。

基于备份集或者7天内的一个时间点创建临时实例。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例为SQL Server 2012/2016基础版或SQL Server 2008 R2版；
-   实例状态为运行中；
-   当前实例中没有正在执行的迁移任务；
-   最近一次创建备份集任务已经完成。

**说明：** 临时实例创建成功后，账号和数据库将继承备份集数据。


## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=CreateTempDBInstance&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateTempDBInstance|系统规定参数，取值：**CreateTempDBInstance**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|BackupId|Integer|否|603524168|备份集ID。

 **说明：** **BackupId**和**RestoreTime**两者至少传入一个。

 |
|RestoreTime|String|否|2011-06-11T16:00:00Z|用户指定备份保留时间内的任意时间点。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** 

-   可以设置为7天之内并且早于当前时间半小时以上的任意时间点，默认时区为UTC；
-   **BackupId**和**RestoreTime**两者至少传入一个。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|TempDBInstanceId|String|sub138xxxxx\_rm-xxxxx|临时实例ID。

 |
|RequestId|String|248DE93F-8647-4B9D-8287-4A4A0FE56AD5|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateTempDBInstance
&DBInstanceId=rm-uf6wjk5xxxxxxx
&BackupId=603524168
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateTempDBInstanceResponse>
       <RequestId>248DE93F-8647-4B9D-8287-4A4A0FE56AD5</RequestId>
  <TempDBInstanceId>sub138xxxxx_juxxxxx</TempDBInstanceId>
</CreateTempDBInstanceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"248DE93F-8647-4B9D-8287-4A4A0FE56AD5",
	"TempDBInstanceId":"sub138xxxxx_juxxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|OperationDenied.TempDBInstanceExists|The operation is not permitted due to temp instance exist.|临时实例已经存在|

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。


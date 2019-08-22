# RestoreTable {#doc_api_Rds_RestoreTable .reference}

调用RestoreTable接口恢复RDS实例的某个数据库或表到原实例上。

RDS for MySQL支持单库和单表的数据恢复，可以通过备份指定恢复误删的数据库或表，快速恢复MySQL的数据。详情请参见[单库单表备份](~~103175~~)。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例版本为RDS for MySQL 5.6高可用版；
-   实例状态为运行中；
-   实例当前没有正在执行的迁移任务；
-   如果需要按时间点恢复，实例必须开启日志备份；
-   实例已开启[单库单表备份](~~103175~~)，并且开启后已[创建新的备份集](~~98818~~)；
-   恢复后的表名在实例中不存在。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=RestoreTable&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RestoreTable|系统规定参数，取值：**RestoreTable**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|BackupId|String|否|9026262|备份集ID。

 您可以通过[DescribeBackups](~~26273~~)接口获取备份集列表。

 **说明：** **BackupId**和**RestoreTime**两者至少传入一个。

 |
|RestoreTime|String|否|2011-06-11T16:00:00Z|备份保留周期内的任意时间点。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** **BackupId**和**RestoreTime**两者至少传入一个。

 |
|TableMeta|String|否|\[\{"type":"db","name":"testdb1","newname":"testdb1\_new","tables":\[\{"type":"table","name":"testdb1table1","newname":"testdb1table1\_new"\}\]\}\]|进行库表恢复时，指定恢复的库表信息。格式：

 ```
[{"type":"db","name":"<数据库1名称>","newname":"<新数据库1名称>","tables":[{"type":"table","name":"<数据库1内的表1名称>","newname":"<新的表1名称>"},{"type":"table","name":"<数据库1内的表2名称>","newname":"<新的表2名称>"}]},{"type":"db","name":"<数据库1名称>","newname":"<新数据库2名称>","tables":[{"type":"table","name":"<数据库2内的表3名称>","newname":"<新的表3名称>"},{"type":"table","name":"<数据库2内的表4名称>","newname":"<新的表4名称>"}]}]
```

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|EA2D4F34-01A7-46EB-A339-D80882135206|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=RestoreTable
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&RestoreTime=2019-08-20T16:00:00Z
&TableMeta=[{"type":"db","name":"dtstestdata","newname":"dtstestdata","tables":[{"type":"table","name":"customer_old","newname":"customer_old123"},{"type":"table","name":"order","newname":"order123"}]}]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RestoreTableResponse>
  <RequestId>EA2D4F34-01A7-46EB-A339-D80882135206</RequestId>
</RestoreTableResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"EA2D4F34-01A7-46EB-A339-D80882135206"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。


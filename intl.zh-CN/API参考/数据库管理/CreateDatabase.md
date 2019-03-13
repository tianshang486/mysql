# CreateDatabase {#doc_api_1063908 .reference}

调用CreateDatabase接口在某个实例下创建数据库。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例中的数据库数量没有超出实例最大数据库数量，可以通过接口[DescribeDBInstanceAttribute](~~26231~~)查询最大数据库数量；
-   实例类型不能为只读实例。

**说明：** 该接口暂不支持PostgreSQL、PPAS和SQL Server 2017集群版，您可以通过SQL做CREATE DATABASE操作。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateDatabase)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDatabase|系统规定参数，取值：**CreateDatabase**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|DBName|String|是|rds\_mysql|数据库名称。

 **说明：** 

-   长度为2~64个字符；
-   以字母开头，以字母或数字结尾；
-   由小写字母、数字、下划线或中划线组成；
-   数据库名称在实例内必须是唯一的；
-   其他非法字符，详见[禁用关键字表](~~26317~~)。

 |
|CharacterSetName|String|是|gbk|字符集，取值：

 -   MySQL/MariaDB类型：**utf8、gbk、latin1、utf8mb4**；
-   SQL Server类型：**Chinese\_PRC\_CI\_AS、Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS、Chinese\_PRC\_BIN**。

 |
|DBDescription|String|否|测试用数据库|实例描述，长度为2~256个字符。以中文、英文字母开头，可以包含可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateDatabase
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&DBName=rds_mysql
&CharacterSetName=gbk
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDatabaseResponse>
  <RequestId>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestId>
</CreateDatabaseResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


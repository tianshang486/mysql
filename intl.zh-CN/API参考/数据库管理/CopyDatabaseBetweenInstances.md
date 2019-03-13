# CopyDatabaseBetweenInstances {#doc_api_1064069 .reference}

调用CopyDatabaseBetweenInstances接口在实例间复制数据库。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   源实例和目标实例同属于一个账户；
-   源实例和目标实例的版本相同；
-   源实例和目标实例在同一地域，可用区可以不同，网络类型需相同；
-   目标实例中没有和源实例同名的数据库；
-   目标实例的可用存储空间 \>源实例中待复制数据库占用的空间。

**说明：** 仅适用于RDS for SQL Server 2012/2016实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CopyDatabaseBetweenInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CopyDatabaseBetweenInstances|系统规定参数，取值为**CopyDatabaseBetweenInstances**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|源实例ID。

 |
|TargetDBInstanceId|String|是|rm-ut5ajk3xxxxxxx|目标实例ID，不能与源实例ID相同。

 |
|DbNames|String|是|testDB1,testDB2|待复制的数据库名列表，用英文逗号（,）隔开。

 |
|BackupId|String|否|1065238746521|源实例备份集ID。按备份集复制数据库时，可以通过查询备份列表接口[DescribeBackups](~~26273~~)获取备份集ID。

 |
|RestoreTime|String|否|2011-06-11T16:00:00Z|按时间点复制数据库，可以选择备份保留周期内的任意时间点。

 |
|SyncUserPrivilege|String|否|NO|是否复制用户和权限：

 -   **YES**：表示复制用户和权限。如果目标实例中有同名的用户，则该用户将叠加源实例的同名用户的权限；
-   **NO**：表示不复制用户和权限。

 默认值：**NO**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|RequestId|String|803D11AF-C370-465B-AB46-CB3A642DC303|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CopyDatabaseBetweenInstances
&DBInstanceId=rm-uf6wjk5xxxxxxx
&TargetDBInstanceId=rm-ut5ajk3xxxxxxx
&DbNames=testDB1,testDB2
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CopyDatabaseBetweenInstancesResponse>
  <RequestId>803D11AF-C370-465B-AB46-CB3A642DC303</RequestId>
</CopyDatabaseBetweenInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"803D11AF-C370-465B-AB46-CB3A642DC303"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|StorageLimitExceeded|Exceeding the allowed Storage of DB instance.|生产磁盘空间限制|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


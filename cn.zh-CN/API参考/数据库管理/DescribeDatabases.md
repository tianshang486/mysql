# DescribeDatabases {#doc_api_1063920 .reference}

调用DescribeDatabases接口查看实例下的数据库信息。

**说明：** 

-   如果请求参数错误，返回数据为空；
-   该接口不支持PostgreSQL、PPAS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDatabases)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDatabases|系统规定参数，取值：**DescribeDatabases**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBName|String|否|testDB01|数据库名称。

 |
|DBStatus|String|否|Creating|数据库状态，取值：

 -   **Creating**：创建中；
-   **Running**：使用中；
-   **Deleting**：删除中。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：30。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Databases| | |数据库信息列表。

 |
|└DBName|String|testDB01|数据库名称。

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxx|数据库所属实例ID。

 |
|└Engine|String|MySQL|数据库实例类型。

 |
|└DBStatus|String|Creating|数据库状态，取值：

 -   **Creating**：创建中；
-   **Running**：使用中；
-   **Deleting**：删除中。

 |
|└CharacterSetName|String|utf8|字符集，取值：

 -   MySQL/MariaDB实例：**utf8、gbk、latin1、utf8mb4**；
-   SQL Server实例：**Chinese\_PRC\_CI\_AS、Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS、Chinese\_PRC\_BIN**。

 |
|└DBDescription|String|测试数据库|数据库描述。

 |
|└Accounts| | |拥有数据库相关权限的账号信息。

 |
|└Account|String|test|账号名称。

 |
|└AccountPrivilege|String|DMLOnly|账号对该数据库拥有的权限，取值：

 -   **ReadWrite**：读写权限；
-   **ReadOnly**：只读权限；
-   **DDLOnly**：仅DDL权限；
-   **DMLOnly**：只DML权限。

 |
|└AccountPrivilegeDetail|String|SELECT|账号对该数据库具有的权限。

 |
|RequestId|String|2603CA96-B17D-4903-BC04-61A2C829CD94|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDatabases
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDatabasesResponse>
  <RequestId>2603CA96-B17D-4903-BC04-61A2C829CD94</RequestId>
  <Databases>
    <Database>
      <Engine>MySQL</Engine>
      <CharacterSetName>utf8</CharacterSetName>
      <DBStatus>Creating</DBStatus>
      <DBDescription/>
      <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
      <Accounts/>
      <DBName>testdb</DBName>
    </Database>
    <Database>
      <Engine>MySQL</Engine>
      <CharacterSetName>gbk</CharacterSetName>
      <DBStatus>Creating</DBStatus>
      <DBDescription/>
      <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
      <Accounts/>
      <DBName>testdb2</DBName>
    </Database>
  </Databases>
</DescribeDatabasesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Databases":{
		"Database":[
			{
				"Accounts":{
					" AccountPrivilegeInfo":[]
				},
				"DBStatus":"Creating",
				"DBInstanceId":"rdsaiiabnaiiabn",
				"DBDescription":"",
				"DBName":"testdb",
				"CharacterSetName":"utf8",
				"Engine":"MySQL"
			},
			{
				"Accounts":{
					" AccountPrivilegeInfo":[]
				},
				"DBStatus":"Creating",
				"DBInstanceId":"rdsaiiabnaiiabn",
				"DBDescription":"",
				"DBName":"testdb2",
				"CharacterSetName":"gbk",
				"Engine":"MySQL"
			}
		]
	},
	"RequestId":"2603CA96-B17D-4903-BC04-61A2C829CD94"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


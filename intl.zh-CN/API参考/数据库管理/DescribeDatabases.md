# DescribeDatabases {#doc_api_Rds_DescribeDatabases .reference}

调用DescribeDatabases接口查看实例下的数据库信息。

**说明：** 如果请求参数错误，返回数据为空。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeDatabases&type=RPC&version=2014-08-15)

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

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Databases| | |数据库信息列表。

 |
|DBName|String|testDB01|数据库名称。

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|数据库所属实例ID。

 |
|Engine|String|MySQL|数据库实例类型。

 |
|DBStatus|String|Creating|数据库状态，取值：

 -   **Creating**：创建中；
-   **Running**：使用中；
-   **Deleting**：删除中。

 |
|CharacterSetName|String|utf8|字符集。

 |
|DBDescription|String|测试数据库|数据库描述。

 |
|Accounts| | |拥有数据库相关权限的账号信息。

 |
|Account|String|test|账号名称。

 |
|AccountPrivilege|String|DMLOnly|账号对该数据库拥有的权限。

 |
|AccountPrivilegeDetail|String|SELECT|账号对该数据库具有的权限。

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
			      <DBDescription></DBDescription>
			      <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
			      <Accounts></Accounts>
			      <DBName>testdb</DBName>
		    </Database>
		    <Database>
			      <Engine>MySQL</Engine>
			      <CharacterSetName>gbk</CharacterSetName>
			      <DBStatus>Creating</DBStatus>
			      <DBDescription></DBDescription>
			      <DBInstanceId>rdsaiiabnaiiabn</DBInstanceId>
			      <Accounts></Accounts>
			      <DBName>testdb2</DBName>
		    </Database>
	  </Databases></DescribeDatabasesResponse>
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。


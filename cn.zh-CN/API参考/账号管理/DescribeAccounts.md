# DescribeAccounts {#doc_api_1105966 .reference}

调用DescribeAccounts接口查看实例的帐号信息。

**说明：** 该接口暂不支持SQL Server 2017集群版、PostgreSQL、PPAS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeAccounts)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAccounts|系统规定参数，取值：**DescribeAccounts**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|AccountName|String|否|test1|数据库账号名称。

 |
|PageSize|Integer|否|30|每页记录数，取值：

 -   **30**；
-   **50**；
-   **100**。

 默认值：**30**。

 |
|PageNumber|Integer|否|1|页码，取值：大于0且不超过Integer的最大值。

 默认值：**1**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Accounts| | |账号信息列表。

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxx|账号所属实例ID。

 |
|└AccountName|String|test1|数据库账号名称。

 |
|└AccountStatus|String|Available|账号状态：

 -   **Unavailable**：不可用；
-   **Available**：可用。

 |
|└AccountDescription|String|测试数据库账号|账号描述。

 |
|└DatabasePrivileges| | |账号拥有的数据库权限列表。

 |
|└DBName|String|test1|数据库名称。

 |
|└AccountPrivilege|String|ReadWrite|账号的权限，取值：

 -   **ReadWrite**：读写；
-   **ReadOnly**：只读；
-   **DDLOnly**：仅DDL；
-   **DMLOnly**：只DML；
-   **Custom**：自定义，您可以通过命令修改。

 |
|└AccountPrivilegeDetail|String|SELECT,INSERT|账号具体的权限。

 |
|└AccountType|String|Normal|账号类型，取值：

 -   **Normal**：普通账号；
-   **Super**：高权限账号。

 |
|└PrivExceeded|String|0|授权是否超过限制，取值：

 -   **1**：是；
-   **0**：否。

 |
|RequestId|String|A2E94301-D07F-4457-9B49-6AA2BB388C85|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeAccounts
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAccountsResponse>
  <Accounts>
    <DBInstanceAccount>
      <DatabasePrivileges>
        <DatabasePrivilege>
          <AccountPrivilege>ReadWrite</AccountPrivilege>
          <AccountPrivilegeDetail>SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER</AccountPrivilegeDetail>
          <DBName>testdb</DBName>
        </DatabasePrivilege>
      </DatabasePrivileges>
      <AccountStatus>Available</AccountStatus>
      <AccountDescription/>
      <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
      <AccountName>testacc02</AccountName>
      <PrivExceeded>0</PrivExceeded>
      <AccountType>Normal</AccountType>
    </DBInstanceAccount>
  </Accounts>
  <RequestId>A2E94301-D07F-4457-9B49-6AA2BB388C85</RequestId>
</DescribeAccountsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Accounts":{
		"DBInstanceAccount":[
			{
				"AccountStatus":"Available",
				"DatabasePrivileges":{
					"DatabasePrivilege":[
						{
							"AccountPrivilege":"ReadWrite",
							"AccountPrivilegeDetail":"SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,INDEX,ALTER,CREATE TEMPORARY TABLES,LOCK TABLES,CREATE VIEW,SHOW VIEW,CREATE ROUTINE,ALTER ROUTINE,EXECUTE,EVENT,TRIGGER",
							"DBName":"testdb"
						}
					]
				},
				"AccountDescription":"",
				"DBInstanceId":"rm-uf6wjk5xxxxxxx",
				"AccountName":"testacc02",
				"PrivExceeded":"0",
				"AccountType":"Normal"
			}
		]
	},
	"RequestId":"A2E94301-D07F-4457-9B49-6AA2BB388C85"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


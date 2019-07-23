# ModifyDTCSecurityIpHostsForSQLServer {#doc_api_Rds_ModifyDTCSecurityIpHostsForSQLServer .reference}

调用ModifyDTCSecurityIpHostsForSQLServer接口设置分布式事务白名单。

分布式事务白名单可以让ECS实例和RDS实例之间支持分布式事务。详情请参见[设置分布式事务白名单](~~124321~~)。

仅适用于如下版本实例：

-   SQL Server 2012/2016企业版高可用版
-   SQL Server 2012/2016标准版

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ModifyDTCSecurityIpHostsForSQLServer&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDTCSecurityIpHostsForSQLServer|系统规定参数，取值：**ModifyDTCSecurityIpHostsForSQLServer**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|RDS实例ID。

 |
|RegionId|String|是|cn-hangzhou|RDS实例的地域ID，可以通过接口[DescribeRegions](~~26243~~)查看。

 |
|SecurityIpHosts|String|是|192.168.1.100,k3ecstest|ECS实例的IP地址和Windows系统的计算机名。格式：ip,hostname。多个实例之间以英文分号（;）隔开。

 **说明：** 计算机名查看方式请参见[设置分布式事务白名单](~~124321~~)。

 |
|WhiteListGroupName|String|是|test1|白名单分组名称。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|RDS实例ID。

 |
|DTCSetResult|String|Success|设置白名单的结果，取值：

 -   **Success**：设置成功；
-   **Fail**：设置失败。

 |
|RequestId|String|671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3|请求ID。

 |
|TaskId|String|178968983|设置任务ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDTCSecurityIpHostsForSQLServer
&DBInstanceId=rm-uf6wjk5xxxxxxx
&RegionId=cn-hangzhou
&SecurityIpHosts=192.168.1.100,k3ecstest
&WhiteListGroupName=test1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDTCSecurityIpHostsForSQLServerResponse>
  <RequestId>671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3</RequestId>
	  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
	  <DTCSetResult>Success</DTCSetResult>
	  <TaskId>178968983</TaskId>
</ModifyDTCSecurityIpHostsForSQLServerResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"RequestId":"671B6D32-B907-4EFF-A3B7-94D2EAD5E3A3",
	"DTCSetResult":"Success",
	"TaskId":178968983
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。


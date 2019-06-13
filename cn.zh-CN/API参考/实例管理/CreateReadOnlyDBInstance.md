# CreateReadOnlyDBInstance {#doc_api_Rds_CreateReadOnlyDBInstance .reference}

调用CreateReadOnlyDBInstance接口为某个实例创建一个只读实例。

 **调用该接口创建只读实例时，请注意：** 

-   主实例的版本必须为以下其中一种：
    -   MySQL 5.6
    -   MySQL 5.7/8.0高可用版（本地SSD盘）
    -   SQL Server 2017集群版
-   对于MySQL类型实例：
    -   如果主实例内存≥64GB，最多允许创建10个只读实例。
    -   如果主实例内存＜64GB，最多允许创建5个只读实例。
-   对于SQL Server类型实例，最多允许创建7个只读实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateReadOnlyDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateReadOnlyDBInstance|系统规定参数，取值：**CreateReadOnlyDBInstance**。

 |
|RegionId|String|是|cn-hangzhou|地域ID。只读实例的地域必须和主实例相同。可以通过接口[DescribeRegions](~~26243~~)查看地域列表。

 |
|ZoneId|String|是|cn-hangzhou-b|可用区ID。可以通过接口[DescribeRegions](~~26243~~)查看可用区列表。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|主实例ID。

 |
|DBInstanceClass|String|是|rds.mys2.small|实例规格，详见[实例规格表](~~26312~~)。建议只读实例规格不小于主实例规格，否则易导致只读实例延迟高、负载高等现象。

 |
|DBInstanceStorage|Integer|是|20|存储空间，取值：**5-3000**，每5GB进行递增，单位：GB。

 **说明：** 不同版本实例，支持的取值范围不同，请以控制台创建只读实例页面为准。

 |
|EngineVersion|String|是|5.6|数据库版本号。必须与主实例相同。取值：

 -   **5.6**
-   **5.7**
-   **8.0**
-   **2017\_ent**

 |
|PayType|String|是|Postpaid|付费类型，仅支持按量付费，取值：**Postpaid**。

 |
|DBInstanceDescription|String|否|测试只读实例|实例描述，长度为2~256个字符。以中文、英文字母开头，可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|InstanceNetworkType|String|否|Classic|实例的网络类型，取值：

 -   **VPC**：VPC网络；
-   **Classic**：经典网络。

 默认创建经典网络实例。

 |
|VPCId|String|否|vpc-uf6f7l4fg90xxxxxxxxxx|VPC ID。

 |
|VSwitchId|String|否|vsw-uf6adz52c2pxxxxxxxxxx|交换机ID。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|PrivateIpAddress|String|否|172.16.201.69|设置只读实例的内网IP，需要在指定交换机的IP地址范围内。系统默认通过**VPCId**和**VSwitchId**自动分配。

 |
|ResourceGroupId|String|否|rg-acfmyxxxxxxxxxx|资源组ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rr-uf6wjk5xxxxxxx|创建的只读实例ID。

 |
|OrderId|String|10078937xxxxx|订单ID。

 |
|ConnectionString|String|rr-xxxxx.mysql.rds.aliyuncs.com|创建的只读实例内网数据库连接地址。

 |
|Port|String|3306|创建的只读实例内网数据库连接端口。

 |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateReadOnlyDBInstance
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&DBInstanceId=rm-uf6wjk5xxxxxxx
&DBInstanceClass=rds.mys2.small
&DBInstanceStorage=20
&EngineVersion=5.6
&PayType=Postpaid
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateReadOnlyDBInstanceResponse>
  <OrderId>10078937xxxxx</OrderId>
  <ConnectionString>rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com </ConnectionString>
  <DBInstanceId>rm-uf6wjk5xxxxxxx</DBInstanceId>
  <port>3306</port>
  <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId>
</CreateReadOnlyDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Port":"3306",
	"ConnectionString":"rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com",
	"RequestId":"1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC",
	"DBInstanceId":"rm-uf6wjk5xxxxxxx",
	"OrderId":"10078937xxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidEngineVersion.Malformed|The specified parameter "EngineVersion" is not valid.|指定EngineVersion参数无效。|
|400|InvalidSecurityIPList.Malformed|The specified parameter "SecurityIPList" is not valid.|指定的SecurityIPList参数无效。|
|400|InvalidSecurityIPList.Duplicate|The Security IP address is not in the available range or occupied.|指定的安全IP地址已被占用或不在有效区间内。|
|400|InvalidParameter|The specified parameter "dbInstanceId" is not valid.|指定dbInstanceId参数无效。|
|403|OperationDenied.PrimaryDBInstanceStatus|The operation is not permitted due to status of primary instance.|主实例状态不支持，实例处于运行态，才能做此操作。|
|400|OperationDenied|VPC IP is in use, please check.|该Ip已经被使用，请您更换IP再重试。|
|404|IncorrectDBInstanceConnType|Current DB instance conn type does not support this operation.|当前DB实例连接类型不支持此操作。|
|400|InvalidZoneId.NotSupported|The Specified vpc Zone not supported.|当前可用区不支持生产 VPC 实例，请您更换可用区再试。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


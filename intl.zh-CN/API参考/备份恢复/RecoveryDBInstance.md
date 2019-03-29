# RecoveryDBInstance {#doc_api_1085943 .reference}

调用RecoveryDBInstance接口恢复数据库，已下线。

**说明：** 该API已下线。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=RecoveryDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RecoveryDBInstance|系统规定参数，取值为：**RecoveryDBInstance**。

 |
|DbNames|String|是|"sourceDbName1":"targetDbName1"|数据库名，若指定多个数据库，按如下格式：\{"原库名1":"新库名1","原库名2":"新库名2"\}

 **说明：** 恢复到已有实例该参数必须传入。

 |
|TargetDBInstanceId|String|否|rm-uf6wjk5xxxxxxx|目标实例ID。

 |
|DBInstanceClass|String|否|rds.mysql.s2.large|新实例规格。

 |
|DBInstanceStorage|Integer|否|5|新实例存储容量。

 |
|PayType|String|否|Postpaid|新实例付费类型：

 -   Postpaid：后付费，按量付费；
-   Prepaid：预付费，包年包月。

 |
|InstanceNetworkType|String|否|VPC|新实例网络类型：

 -   Classic：经典网络；
-   VPC：专有网络，VPC网络。

 默认与主实例网络类型一致。

 |
|DBInstanceId|String|否|rm-xxxxxxxx1|原实例ID。

 -   按备份集恢复（即指定BackupId参数）时，本参数不是必须。
-   按时间点恢复（即指定RestoreTime参数）时，本参数为必须。

 |
|BackupId|String|否|293044600|备份集ID，可通过查询备份列表接口[DescribeBackups](~~26273~~)获取。

 指定此参数时，**DBInstanceId**参数为可选。

 **BackupId**和**RestoreTime**两者至少传入一个。

 |
|RestoreTime|String|否|2011-06-11T16:00:00Z|备份保留周期内的任意时间点，例如2011-06-11T16:00:00Z

 指定此参数时，**DBInstanceId**参数为必须。

 **BackupId**和**RestoreTime**两者至少传入一个。

 |
|VPCId|String|否|vpc-xxxxxxxxxxx|VPCId。

 |
|VSwitchId|String|否|vsw-xxxxxxxxxxx|VSwitch Id，多个值用英文逗号“,”隔开。

 |
|PrivateIpAddress|String|否|vpc-xxxxxxxxxxx|设置实例的内网IP，需要在指定交换机的IP地址范围内。系统默认通过**VPCId**和**VSwitchId**自动分配。

 |
|UsedTime|String|否|Prepaid|包年包月类型：

 若付费类型为Prepaid，则该入参必须传入；

 指定购买时长，可按需传入1、2、3等数值。

 |
|Period|String|否|Prepaid|指定预付费实例为包年或者包月类型：

 -   Year：包年；
-   Month：包月。

 **说明：** 若付费类型为Prepaid，则该入参必须传入。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-xxxxxxx|实例名。

 |
|OrderId|String|543254874|订单ID。

 |
|RequestId|String|EFB6083A-7699-489B-8278-C0CB4793A96E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=RecoveryDBInstance
&TargetDBInstanceId=rm-uf6wjk5xxxxxxx
&DbNames="sourceDbName1":"targetDbName1"
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RecoveryDBInstanceResponse>
  <RequestId>EFB6083A-7699-489B-8278-C0CB4793A96E</RequestId>
</RecoveryDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"EFB6083A-7699-489B-8278-C0CB4793A96E"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


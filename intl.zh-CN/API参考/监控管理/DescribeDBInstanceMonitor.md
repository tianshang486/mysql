# DescribeDBInstanceMonitor {#doc_api_Rds_DescribeDBInstanceMonitor .reference}

调用DescribeDBInstanceMonitor接口查询监控频率。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceMonitor&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceMonitor|系统规定参数，取值：**DescribeDBInstanceMonitor**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Period|String|60|监控的采集数据间隔，单位：秒。

 |
|RequestId|String|30829FD4-1A84-4C2A-A625-2EADECB95CA3|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceMonitor
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceMonitorResponse>
	  <period>60</period>
	  <requestId>30829FD4-1A84-4C2A-A625-2EADECB95CA3</requestId></DescribeDBInstanceMonitorResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"30829FD4-1A84-4C2A-A625-2EADECB95CA3",
	"period":"60"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Rds)查看更多错误码。


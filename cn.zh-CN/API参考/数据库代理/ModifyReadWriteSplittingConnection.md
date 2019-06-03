# ModifyReadWriteSplittingConnection {#doc_api_Rds_ModifyReadWriteSplittingConnection .reference}

调用ModifyReadWriteSplittingConnection接口修改读写分离链路的延迟阈值和各个实例的读权重。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例中没有正在执行的迁移任务；
-   实例为如下版本：
    -   MySQL 5.7高可用版（本地SSD盘）
    -   MySQL 5.6
    -   SQL Server 2017集群版

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyReadWriteSplittingConnection)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyReadWriteSplittingConnection|系统规定参数，取值：**ModifyReadWriteSplittingConnection**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|主实例ID。

 |
|ConnectionStringPrefix|String|否|rm-m5xxxxxxxx.mysql.rds.aliyuncs.com|读写分离地址前缀名，不可重复，由小写字母和中划线组成，需以字母开头，长度不超过30个字符。

 **说明：** 默认以“实例名+rw”字符串组成前缀。

 |
|MaxDelayTime|String|否|12|延迟阈值，单位为秒。当只读实例延迟时间超过该阈值时，读取流量不发往该实例。不传该参数则保持原值。

 **说明：** 

-   参数**MaxDelayTime**不适用于SQL Server 2017集群版实例；
-   至少传入**MaxDelayTime**或**DistributionType**中的一个。

 |
|DistributionType|String|否|Standard|读权重分配模式，取值：

 -   **Standard**：按规格权重自动分配；
-   **Custom**：自定义分配权重。

 **说明：** 至少传入**MaxDelayTime**或**DistributionType**中的一个。

 |
|Weight|String|否|\{“Instanceid1“:”100”,”Instanceid2”:”200”\}|读权重分配，即传入主实例和只读实例的读请求权重。以100递增，最大值为10000，格式：\{“Instanceid1“:”Weight”,”Instanceid2”:”Weight”...\}。

 **说明：** 

-   当**DistributionType**为**Custom**时，必须传入该参数；
-   当**DisrtibutionType**为**Standard**时，传入该参数无效。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyReadWriteSplittingConnection
&DistributionType=Standard
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyReadWriteSplittingConnectionResponse>
  <RequestID>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestID>
</ModifyReadWriteSplittingConnectionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestID":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


# AllocateReadWriteSplittingConnection {#doc_api_Rds_AllocateReadWriteSplittingConnection .reference}

调用AllocateReadWriteSplittingConnection接口申请读写分离地址。

对拥有只读实例的主实例，可以申请[读写分离访问地址](~~51073~~)。申请该地址后，不影响原主实例、只读实例的已有访问地址，以及正常的内外网申请。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例拥有只读实例；
-   实例没有正在执行的迁移任务；
-   实例为如下版本：
    -   MySQL 5.7高可用版（本地SSD盘）
    -   MySQL 5.6
    -   SQL Server 2017集群版

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=AllocateReadWriteSplittingConnection)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AllocateReadWriteSplittingConnection|系统规定参数，取值：**AllocateReadWriteSplittingConnection**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|主实例ID。

 |
|ConnectionStringPrefix|String|否|rr-m5exxxxx-rw.mysql.rds.aliyuncs.com|读写分离地址前缀名，不可重复，由小写字母和中划线组成，需以字母开头，长度不超过30个字符。

 **说明：** 默认以“实例名+rw”字符串组成前缀。

 |
|Port|String|否|3306|读写分离端口，取值：

 -   MySQL：范围为3001~3999，默认为3306；
-   SQL Server：范围为1000~5999，默认为1433。

 |
|MaxDelayTime|String|否|30|延迟阈值，范围是0~7200，单位：秒，默认为30。

 **说明：** 当只读实例延迟超过该阈值时，读取流量不发往该实例。

 |
|NetType|String|否|Intranet|读写分离连接串的网络类型，取值：

 -   **Internet**：外网；
-   **Intranet**：内网。

 默认为内网，且内网类型与主实例保持一致。

 |
|DistributionType|String|否|Standard|读权重分配模式，取值：

 -   **Standard**：按规格权重自动分配；
-   **Custom**：自定义分配权重。

 |
|Weight|String|否|\{“Instanceid1“:”100”,”Instanceid2”:”200”\}|读权重分配，即传入主实例和只读实例的读请求比例。以100进行递增，最大值为10000，格式：\{“Instanceid1“:”Weight”,”Instanceid2”:”Weight”...\}。

 **说明：** 

-   当DistributionType为Custom时，必须传入该参数；
-   当DisrtibutionType为Standard时，传入该参数无效。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4C467B38-3910-447D-87BC-AC049166F216|请求ID 。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=AllocateReadWriteSplittingConnection
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AllocateReadWriteSplittingConnectionResponse>
  <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
</AllocateReadWriteSplittingConnectionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"4C467B38-3910-447D-87BC-AC049166F216"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


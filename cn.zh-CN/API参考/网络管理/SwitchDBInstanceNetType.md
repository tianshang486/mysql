# SwitchDBInstanceNetType {#doc_api_Rds_SwitchDBInstanceNetType .reference}

调用SwitchDBInstanceNetType接口切换内外网地址。

该接口用于内外网切换，即原来是内网，则会切换到外网，反之亦然。切换后连接地址会发生变化，需要您修改代码中的连接地址并重启应用。

必须满足以下条件，否则将修改失败：

-   实例状态为运行中；
-   24小时内切换次数低于20次；
-   实例的网络类型为经典网络；
-   实例的[设置访问模式](~~26193~~)和[实例规格表](~~26312~~)对连接地址的选择有如下限制：
    -   实例系列为**单机基础版**，实例版本为**MySQL 5.7、SQL Server 2016 web 基础系列、2012 web 基础系列、2012 企业版 基础系列、PostgreSQL 10.0**，访问模式为**标准模式**，连接地址可切换为**内网地址、外网地址、内网地址和外网地址**；
    -   实例系列为**双机高可用版**，实例版本为**MySQL 5.5/5.6/5.7、SQL Server 2008 R2、2016标准版 高可用系列、2012标准版 高可用系列、2016企业版 高可用系列、2012企业版 高可用系列、PostgreSQL 9.4、PPAS 9.3、10.0**，访问模式为**标准模式**，连接地址可切换为**内网地址、外网地址**；
    -   实例系列为**双机高可用版**，实例版本为**MySQL 5.5/5.6/5.7、SQL Server 2008 R2、2016标准版 高可用系列、2012标准版 高可用系列、2016企业版 高可用系列、2012企业版 高可用系列、PostgreSQL 9.4、PPAS 9.3、10.0**，访问模式为**高安全模式**，连接地址可切换为**内网地址、外网地址、内网地址和外网地址**；
    -   实例系列为**金融版**，实例版本为**MySQL 5.6**，访问模式为**标准模式**，连接地址可切换为**内网地址、外网地址**；
    -   实例系列为**金融版**，实例版本为**MySQL 5.6**，访问模式为**高安全模式**，连接地址可切换为**内网地址、外网地址、内网地址和外网地址**。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=SwitchDBInstanceNetType)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SwitchDBInstanceNetType|系统规定参数，取值：**SwitchDBInstanceNetType**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|实例ID。

 |
|ConnectionStringPrefix|String|是|rm-xxxxxx|自定义连接地址的前辍。由字母，数字组成，小写字母开头，8~64个字符。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|Port|String|否|3306|端口号，取值：**3001~3999**。

 |
|ConnectionStringType|String|否|Normal|查询连接地址类型，取值：

 -   **Normal**：查询普通连接；
-   **ReadWriteSplitting**：查询读写分离连接；

 默认返回所有连接。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65BDA532-28AF-4122-AA39-B382721EEE64|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=SwitchDBInstanceNetType
&DBInstanceId=rm-uf6wjk5xxxxxxx
&ConnectionStringPrefix=rm-xxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SwitchDBInstanceNetTypeResponse>
  <RequestId> 65BDA532-28AF-4122-AA39-B382721EEE64</RequestId>
</SwitchDBInstanceNetTypeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 65BDA532-28AF-4122-AA39-B382721EEE64"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


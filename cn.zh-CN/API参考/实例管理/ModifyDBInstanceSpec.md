# ModifyDBInstanceSpec {#doc_api_Rds_ModifyDBInstanceSpec .reference}

调用ModifyDBInstanceSpec接口变更RDS实例（包括常规实例和只读实例，不包括灾备实例和临时实例）的规格或存储空间。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   实例状态为运行中；
-   实例没有正在执行的备份任务；
-   请求参数中必须至少指定实例规格（DBInstanceClass）和存储空间（DBInstanceStorage）其中一个参数；
-   若降低磁盘空间配置，输入的磁盘空间不能小于实际使用空间大小的1.1倍；
-   当前只支持对常规实例和只读实例变更配置，不支持灾备实例和临时实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=ModifyDBInstanceSpec)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDBInstanceSpec|系统规定参数，取值：**ModifyDBInstanceSpec**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|待变更配置的实例ID。

 |
|PayType|String|是|Postpaid|实例当前的付费类型，取值：

 -   **Postpaid**：按量付费；
-   **Prepaid**：预付费。

 |
|DBInstanceClass|String|否|rds.mys2.small|实例规格，详见[实例规格表](~~26312~~)。

 **说明：** 至少指定实例规格**DBInstanceClass**和存储空间**DBInstanceStorage**其中一个参数。

 |
|DBInstanceStorage|Integer|否|20|自定义存储空间，单位：GB。每5GB进行递增，详情请参见[实例规格表](~~26312~~)。

 **说明：** 至少指定实例规格**DBInstanceClass**和存储空间**DBInstanceStorage**其中一个参数。

 |
|EffectiveTime|String|否|MaintainTime|生效时间，取值：

 -   **Immediate**：立即生效；
-   **MaintainTime**：在可运维时间段内生效，请参见[ModifyDBInstanceMaintainTime](~~26249~~)。

 默认值：**Immediate**。

 |
|EngineVersion|String|否|5.6|数据库版本号，取值：

 -   MySQL：**5.5/5.6/5.7/8.0**；
-   SQLServer：**2008r2/2012/2012\_ent\_ha/2012\_std\_ha/2012\_web/2016\_ent\_ha/2016\_std\_ha/2016\_web/2017\_ent**；
-   PostgreSQL：**9.4/10.0**；
-   PPAS：**9.3/10.0**；
-   MariaDB：**10.3**。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|3C5CFDEE-F774-4DED-89A2-1D76EC63C575|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ModifyDBInstanceSpec
&DBInstanceId=rm-uf6wjk5xxxxxxx
&PayType=Postpaid
&DBInstanceClass=rds.mys2.small
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDBInstanceSpecResponse>
  <RequestId>3C5CFDEE-F774-4DED-89A2-1D76EC63C575</RequestId>
</ModifyDBInstanceSpecResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":" 3C5CFDEE-F774-4DED-89A2-1D76EC63C575 "
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


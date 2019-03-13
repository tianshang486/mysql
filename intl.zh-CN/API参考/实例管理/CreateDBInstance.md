# CreateDBInstance {#doc_api_1063872 .reference}

调用CreateDBInstance接口创建一个RDS实例。

关于RDS实例的规格，请参见[实例规格表](~~26312~~)。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=CreateDBInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDBInstance|系统规定参数，取值：**CreateDBInstance**。

 |
|RegionId|String|是|cn-hangzhou|地域ID，长度不超过50个字符，可以通过接口[DescribeRegions](~~26243~~)查看可用的地域ID。

 |
|Engine|String|是|MySQL|数据库类型，取值：

 -   **MySQL**；
-   **SQLServer**；
-   **PostgreSQL**；
-   **PPAS**；
-   **MariaDB**。

 |
|EngineVersion|String|是|5.6|数据库版本，取值：

 -   MySQL：**5.5/5.6/5.7**；
-   SQLServer：**2008r2/2012/2012\_ent\_ha/2012\_std\_ha/2012\_web/2016\_ent\_ha/2016\_std\_ha/2016\_web/2017\_ent**；
-   PostgreSQL：**9.4/10.0**；
-   PPAS：**9.3/10.0**；
-   MariaDB：**10.3**。

 |
|DBInstanceClass|String|是|rds.mys2.small|实例规格，详见[实例规格表](~~26312~~)。

 |
|DBInstanceStorage|Integer|是|20|实例存储空间，取值：

 -   MySQL/PostgreSQL/PPAS 双机高可用版： **5~2000**；
-   MySQL 5.7 云盘版/MariaDB：**20~1000**；
-   SQL Server 2008R2：**10~2000**；
-   SQL Server 2012/2016/2017：**20~3000**。

 每5G进行递增，单位：GB。详见[实例规格表](~~26312~~)。

 |
|DBInstanceNetType|String|是|Internet|实例的网络连接类型，取值：

 -   **Internet**：公网连接；
-   **Intranet**：内网连接。

 |
|SecurityIPList|String|是|10.23.12.27/25|该实例的[IP白名单](~~43185~~)，多个IP地址请以英文逗号（,）隔开，不可重复，最多1000个。支持如下两种格式：

 -   IP地址形式，例如：10.23.12.24。
-   CIDR形式，例如：10.23.12.24/24（无类域间路由，24表示了地址中前缀的长度，范围为1~32）。

 |
|PayType|String|是|Postpaid|实例的付费类型，取值：

 -   **Postpaid**：后付费（按量付费）；
-   **Prepaid**：预付费（包年包月）。

 |
|SystemDBCharset|String|否|GBK|字符集，取值：

 -   MySQL/MariaDB实例：**utf8、gbk、latin1、utf8mb4**；
-   SQL Server实例：**Chinese\_PRC\_CI\_AS、Chinese\_PRC\_CS\_AS、SQL\_Latin1\_General\_CP1\_CI\_AS、SQL\_Latin1\_General\_CP1\_CS\_AS、Chinese\_PRC\_BIN**。

 |
|DBInstanceDescription|String|否|测试数据库|实例名称，长度为2~256个字符。以中文、英文字母开头，可以包含可以包含数字、中文、英文、下划线（\_）、短横线（-）。

 **说明：** 不能以 http:// 和 https:// 开头。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|ZoneId|String|否|cn-hangzhou-b|可用区ID。

 **说明：** 如果数据库类型为MariaDB，该参数必填。

 |
|InstanceNetworkType|String|否|Classic|实例的网络类型，取值：

 -   **VPC**：VPC网络；
-   **Classic**：经典网络。

 默认创建经典网络类型的实例。

 **说明：** 

 

-   SQL Server2017集群版只支持VPC网络；

-   如果数据库类型为MariaDB，该参数必填。

 |
|ConnectionMode|String|否|Standard|实例的访问模式，取值：

 -   **Standard**：标准访问模式；
-   **Safe**：数据库代理模式。

 默认为RDS系统分配。

 **说明：** SQL Server 2012/2016/2017只支持标准访问模式。

 |
|VPCId|String|否|vpc-xxxxxxxxxxxx|VPC ID， 多个值用英文逗号（,）隔开。

 **说明：** 如果数据库类型为MariaDB，该参数必填。

 |
|VSwitchId|String|否|vsw-xxxxxxxxxxx|VSwitch ID，多个值用英文逗号（,）隔开。

 **说明：** 如果数据库类型为MariaDB，该参数必填。

 |
|PrivateIpAddress|String|否|172.16.201.69|设置实例的内网IP，需要在指定交换机的IP地址范围内。系统默认通过**VPCId**和**VSwitchId**自动分配。

 |
|UsedTime|String|否|2|指定购买时长，取值：

 -   当参数**Period**为**Year**时，UsedTime取值为**1~9**；
-   当参数**Period**为**Month**时，UsedTime取值为**1~3**。

 **说明：** 若付费类型为**Prepaid**则该参数必须传入。

 |
|Period|String|否|Year|指定预付费实例为包年或者包月类型，取值：

 -   **Year**：包年；
-   **Month**：包月。

 **说明：** 若付费类型为**Prepaid**则该参数必须传入。

 |
|DBInstanceStorageType|String|否|cloud\_ssd|实例存储类型，取值：

 -   **local\_ssd**：本地SSD盘（推荐）；
-   **cloud\_ssd**：SSD云盘。

 |
|BusinessInfo|String|否|121436975448952|业务扩展参数。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|OrderId|String|100789370230206|订单ID。

 |
|ConnectionString|String|rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com|数据库内网连接地址。

 |
|Port|String|3306|数据库内网连接端口。

 |
|RequestId|String|1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=CreateDBInstance
&RegionId=cn-hangzhou
&Engine=MySQL
&EngineVersion=5.6
&DBInstanceClass=rds.mys2.small
&DBInstanceStorage=20
&DBInstanceNetType=Internet
&SecurityIPList=10.23.12.27/25
&PayType=Postpaid
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDBInstanceResponse>
  <OrderId>100789370230206</OrderId>
  <ConnectionString>rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com</ConnectionString>
  <DBInstanceId>rm-uf6wjk5xxxxxxxxxx</DBInstanceId>
  <Port>3306</Port>
  <RequestId>1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC</RequestId>
</CreateDBInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Port":"3306",
	"ConnectionString":"rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com",
	"RequestId":"1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC",
	"DBInstanceId":"rm-uf6wjk5xxxxxxxxxx",
	"OrderId":"100789370230206"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidZoneId.NotSupported|The Specified vpc Zone not supported.|当前可用区不支持生产 VPC 实例，请您更换可用区再试。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


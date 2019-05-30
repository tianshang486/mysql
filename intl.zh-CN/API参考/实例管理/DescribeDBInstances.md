# DescribeDBInstances {#doc_api_Rds_DescribeDBInstances .reference}

调用DescribeDBInstances接口查看RDS实例列表或被RAM授权的实例列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstances|系统规定参数，取值：**DescribeDBInstances**。

 |
|RegionId|String|是|cn-hangzhou|地域ID，可以通过接口[DescribeRegions](~~26243~~)查看。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|Engine|String|否|MySQL|数据库类型，取值：

 -   **MySQL**；
-   **SQLServer**；
-   **PostgreSQL**；
-   **PPAS**；
-   **MariaDB**。

 默认返回所有数据库类型。

 |
|ZoneId|String|否|cn-hangzhou-a|可用区ID。

 |
|DBInstanceStatus|String|否|Running|实例状态，详情请参见[实例状态表](~~26315~~)。

 |
|Expired|String|否|True|实例的过期状态，取值：

 -   **True**：已过期。
-   **False**：未过期。

 |
|SearchKey|String|否|rm-uf6w|可基于实例ID或者实例备注模糊搜索。

 |
|DBInstanceId|String|否|rm-uf6wjk5xxxxxxx|实例ID。

 |
|DBInstanceType|String|否|Primary|实例类型，取值：

 -   **Primary**：主实例；
-   **Readonly**：只读实例；
-   **Guard**：灾备实例；
-   **Temp**：临时实例。

 默认返回所有实例类型。

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
|InstanceNetworkType|String|否|Classic|实例的网络类型，取值：

 -   **VPC**：专有网络下的实例；
-   **Classic**：经典网络下的实例。

 默认返回所有网络类型下的实例。

 |
|VpcId|String|否|vpc-uf6f7l4fg90xxxxxxxxxx|VPC ID。

 |
|VSwitchId|String|否|vsw-uf6adz52c2pxxxxxxxxxx|交换机ID。

 |
|DBInstanceClass|String|否|rds.mys2.small|实例规格，详见[实例规格表](~~26312~~)。

 |
|EngineVersion|String|否|5.7|数据库版本。

 |
|PayType|String|否|Postpaid|付费类型，取值：

 -   **Postpaid**：按量付费；
-   **Prepaid**：包年包月。

 |
|ConnectionMode|String|否|Standard|实例的访问模式，取值：

 -   **Standard**：标准访问模式；
-   **Safe**：数据库代理模式。

 默认返回所有访问模式下的实例。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|proxyId|String|否|API|代理模式ID。

 |
|ResourceGroupId|String|否|rg-acfmyxxxxx|资源组ID。

 |
|Tags|String|否|\{“key1”:”value1”\}|查询绑定有该标签的实例，包括TagKey和TagValue。单次最多支持传入5组值，格式：\{"key1":"value1","key2":"value2"...\}。

 |
|Tag.1.key|String|否|Tagkey1|当前第一组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.2.key|String|否|Tagkey2|当前第二组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.3.key|String|否|Tagkey3|当前第三组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.4.key|String|否|Tagkey4|当前第四组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.5.key|String|否|Tagkey5|当前第五组key。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.1.value|String|否|Tagvalue1|当前第一组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.2.value|String|否|Tagvalue2|当前第二组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.3.value|String|否|Tagvalue3|当前第三组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.4.value|String|否|Tagvalue4|当前第四组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |
|Tag.5.value|String|否|Tagvalue5|当前第五组value。需要绑定的Tag，包括TagKey和TagValue，单次最多支持传入5组值。TagKey不能为空，TagValue可以为空。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageRecordCount|Integer|10|当前页实例个数。

 |
|TotalRecordCount|Integer|100|总记录数。

 |
|PageNumber|Integer|1|页码。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |
|Items| | |由实例信息组成的数组。

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|└DBInstanceDescription|String|测试数据库|实例描述。

 |
|└PayType|String|Postpaid|实例的付费类型，取值：

 -   **Postpaid**：按量付费；
-   **Prepaid**：包年包月。

 |
|└DBInstanceType|String|Primary|实例类型，取值：

 -   **Primary**：主实例；
-   **ReadOnly**：只读实例；
-   **Guard**：灾备实例；
-   **Temp**：临时实例。

 |
|└InstanceNetworkType|String|Classic|实例的网络类型，取值：

 -   **Classic**：经典网络；
-   **VPC**：VPC网络。

 |
|└ConnectionMode|String|Performance|实例的访问模式，取值：

 -   **Standard**：标准访问模式；
-   **Safe**：数据库代理模式。

 |
|└RegionId|String|cn-hangzhou|地域ID。

 |
|└ExpireTime|String|2019-02-27T16:00:00Z|到期时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 **说明：** 按量付费实例无到期时间。

 |
|└DBInstanceStatus|String|Running|实例状态，详情请参见[实例状态表](~~26315~~)。

 |
|└Engine|String|MySQL|数据库类型。

 |
|└DBInstanceNetType|String|Internet|实例的网络连接类型，取值：

 -   **Internet**：外网连接；
-   **Intranet**：内网连接。

 |
|└LockMode|String|Unlock|实例的锁定状态。取值：

 -   **Unlock**：正常；
-   **ManualLock**：手动触发锁定；
-   **LockByExpiration**：实例过期自动锁定；
-   **LockByRestoration**：实例回滚前自动锁定；
-   **LockByDiskQuota**：实例空间满自动锁定；
-   **Released**：实例已释放。此时实例无法进行解锁，只能使用备份数据重新创建新实例，重建时间较长，请耐心等待。

 |
|└LockReason|String|instance\_expired|实例被锁定的原因。

 |
|└MasterInstanceId|String|rm-uf6wjk5xxxxxxxxxx|主实例的ID，如果没有返回此参数（即为null）则表示该实例是主实例。

 |
|└GuardDBInstanceId|String|rm-uf64zsuxxxxxxxxxx|主实例如果有灾备实例，该参数即为灾备实例的ID。

 |
|└TempDBInstanceId|String|rm-uf64zsuxxxxxxxxxx|主实例如果有临时实例，该参数即为临时实例的ID。

 |
|└Category|String|Basic|实例系列：

 -   **Basic**：基础版；
-   **HighAvailability**：高可用版；
-   **Finance**：金融版（仅支持中国站）。

 |
|└CreateTime|String|2018-11-05T11:26:02Z|创建时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└DBInstanceClass|String|rds.mys2.small|实例规格，详见[实例规格表](~~26312~~)。

 |
|└DBInstanceStorageType|String|ModuleList.4.ModuleCode|实例储存类型。

 |
|└DestroyTime|String|2018-11-05T11:26:02Z|销毁时间。格式：*yyyy-MM-dd*T*HH:mm:ss*Z（UTC时间）。

 |
|└EngineVersion|String|5.7|数据库版本。

 |
|└MutriORsignle|Boolean|true|是否是多可用区，取值：**true | false**

 |
|└ReadOnlyDBInstanceIds| | |主实例下如果有只读实例，该参数为只读实例的ID列表。

 |
|└DBInstanceId|String|rr-uf6wjk5xxxxxxx|只读实例ID。

 |
|└ResourceGroupId|String|rg-acfmyxxxxxxx|资源组ID。

 |
|└VSwitchId|String|vsw-uf6adz52c2pxxxxxxx|交换机ID。

 |
|└VpcCloudInstanceId|String|rm-uf6wjk5xxxxxxx|专有网络实例ID。

 |
|└VpcId|String|vpc-uf6f7l4fg90xxxxxxx|VPC ID。

 |
|└ZoneId|String|cn-hangzhou-a|可用区ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstances
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstancesResponse>
  <Items>
    <DBInstance>
      <LockMode>Unlock</LockMode>
      <DBInstanceNetType>Intranet</DBInstanceNetType>
      <DBInstanceClass>ppas.x4.xlarge.2</DBInstanceClass>
      <ResourceGroupId>rg-acfnt75uxxxxx</ResourceGroupId>
      <DBInstanceId>rm-dj120j44xxxxx</DBInstanceId>
      <VpcCloudInstanceId/>
      <ZoneId>cn-beijing-MAZ3(c,e)</ZoneId>
      <ReadOnlyDBInstanceIds/>
      <ConnectionMode>Standard</ConnectionMode>
      <InstanceNetworkType>Classic</InstanceNetworkType>
      <Engine>PPAS</Engine>
      <MutriORsignle>true</MutriORsignle>
      <InsId>1</InsId>
      <ExpireTime/>
      <CreateTime>2019-03-20T02:18:02Z</CreateTime>
      <DBInstanceType>Primary</DBInstanceType>
      <RegionId>cn-beijing</RegionId>
      <EngineVersion>10.0</EngineVersion>
      <LockReason/>
      <DBInstanceStatus>Running</DBInstanceStatus>
      <PayType>Postpaid</PayType>
    </DBInstance>
  </Items>
  <TotalRecordCount>1</TotalRecordCount>
  <PageNumber>1</PageNumber>
  <RequestId>0C2B0363-2707-4300-9900-0A65846CE48E</RequestId>
  <PageRecordCount>1</PageRecordCount>
</DescribeDBInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"DBInstance":[
			{
				"LockMode":"Unlock",
				"DBInstanceNetType":"Intranet",
				"DBInstanceClass":"ppas.x4.xlarge.2",
				"ResourceGroupId":"rg-acfnt75uxxxxx",
				"DBInstanceId":"rm-dj120j44xxxxx",
				"VpcCloudInstanceId":"",
				"ZoneId":"cn-beijing-MAZ3(c,e)",
				"ReadOnlyDBInstanceIds":{
					"ReadOnlyDBInstanceId":[]
				},
				"ConnectionMode":"Standard",
				"InstanceNetworkType":"Classic",
				"Engine":"PPAS",
				"MutriORsignle":true,
				"InsId":1,
				"ExpireTime":"",
				"RegionId":"cn-beijing",
				"DBInstanceType":"Primary",
				"CreateTime":"2019-03-20T02:18:02Z",
				"LockReason":"",
				"EngineVersion":"10.0",
				"DBInstanceStatus":"Running",
				"PayType":"Postpaid"
			}
		]
	},
	"PageNumber":1,
	"TotalRecordCount":1,
	"RequestId":"0C2B0363-2707-4300-9900-0A65846CE48E",
	"PageRecordCount":1
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDBInstanceType.ValueNotSupport|The specified parameter"DBInstanceType" is not valid.|参数DBInstanceType无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


# DescribeDBInstanceAttribute {#doc_api_1101599 .reference}

调用DescribeDBInstanceAttribute接口查看RDS实例的详细信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDBInstanceAttribute|系统规定参数，取值：**DescribeDBInstanceAttribute**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxxxxx|实例ID。可以一次输入最多30个，以英文逗号（,）分隔。

 |
|Expired|String|否|False|实例过期状态，取值：

 -   **True**：已过期；
-   **False**：未过期。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Items| | |DBInstanceAttribute的参数。

 |
|└DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|└PayType|String|Postpaid|实例付费方式，取值：

 -   **Postpaid**：按量付费；
-   **Prepaid**：包年包月。

 |
|└DBInstanceType|String|Primary|实例类型，取值：

 -   **Primary**：主实例；
-   **Readonly**：只读实例；
-   **Guard**：灾备实例；
-   **Temp**：临时实例。

 |
|└Category|String|Basic|实例系列，取值：

 -   **Basic**：基础版；
-   **HighAvailability**：高可用版；
-   **Finance**：金融版（仅支持中国站）。

 |
|└InstanceNetworkType|String|Classic|实例的网络类型，取值：

 -   **Classic**：经典网络；
-   **VPC**：专有网络。

 |
|└RegionId|String|cn-hangzhou|地域ID。

 |
|└ZoneId|String|cn-hangzhou-a|可用区ID。

 |
|└ConnectionString|String|rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com|内网连接地址。

 |
|└Port|String|3306|内网连接端口。

 |
|└Engine|String|MySQL|数据库类型。

 |
|└EngineVersion|String|5.5|数据库版本。

 |
|└DBInstanceClassType|String|s|实例规格族，取值：

 -   **s**：共享型；
-   **x**：通用型；
-   **d**：独享套餐；
-   **h**：独占物理机。

 |
|└DBInstanceClass|String|rds.mys2.small|实例规格。

 |
|└DBInstanceMemory|Long|4096|实例内存，单位：M。

 |
|└DBInstanceStorage|Integer|10|实例存储空间，单位：GB。

 |
|└DBInstanceNetType|String|Internet|实例的网络连接类型，取值：

 -   **Internet**：外网；
-   **Intranet**：内网。

 |
|└DBInstanceStatus|String|Running|实例状态，详情请参见[实例状态表](~~26315~~)。

 |
|└DBInstanceDescription|String|测试数据库|实例备注。

 |
|└LockMode|String|Unlock|实例锁定模式：

 -   **Unlock**：正常；
-   **ManualLock**：手动触发锁定；
-   **LockByExpiration**：实例过期自动锁定；
-   **LockByRestoration**：实例回滚前的自动锁定；
-   **LockByDiskQuota**：实例空间满自动锁定。

 |
|└LockReason|String|instance\_expired|锁定原因。

 |
|└DBMaxQuantity|Integer|200|一个实例下可创建最大数据库数量。

 |
|└AccountMaxQuantity|Integer|50|可创建账号的最大数量。

 |
|└CreationTime|String|2011-05-30T12:11:04Z|创建时间。

 |
|└ExpireTime|String|2019-03-27T16:00:00Z|到期时间。

 **说明：** 按量付费实例无到期时间。

 |
|└MaintainTime|String|00:00Z-02:00Z|实例可维护时间段。

 |
|└AvailabilityValue|String|100.0%|实例可用性状态，单位：百分比。

 |
|└MaxIOPS|Integer|150|最大每秒IO请求次数。

 |
|└MaxConnections|Integer|60|最大并发连接数。

 |
|└MasterInstanceId|String|rm-uf6wjk5xxxxxxxxxx|主实例的ID，如果没有返回此参数（即为null）则表示该实例是主实例。

 |
|└IncrementSourceDBInstanceId|String|rm-uf6wjk5xxxxxxxxxx|增量数据来源的实例ID，如灾备实例的增量数据来源是主实例。只读实例的增量数据来源是主实例，如果没有返回此参数（即为null）则表示该实例是主实例。

 |
|└GuardDBInstanceId|String|rm-uf64zsuxxxxxxxxxx|该实例如果挂载着灾备实例，即为灾备实例的ID。

 |
|└TempDBInstanceId|String|rm-uf64zsuxxxxxxxxxx|该实例如果挂载着临时实例，即为临时实例ID。

 |
|└ReadOnlyDBInstanceIds| | |主实例下挂载的只读实例ID列表。

 |
|└DBInstanceId|String|rm-bpxxxxxxxxx|只读实例ID。

 |
|└AdvancedFeatures|String|LinkedServer|目前只针对SQL Server，获取高级特性值，多个值之间用英文逗号（,）隔开，现返回值如下：

 -   **LinkedServer**：链接服务器；
-   **DistributeTransaction**：分布式事务。

 |
|└Collation|String|Chinese\_PRC\_CI\_AS|系统字符集排序规则。

 |
|└ConnectionMode|String|Standard|实例的访问模式，取值：

 -   **Standard**：标准访问模式；
-   **Safe**：数据库代理模式。

 |
|└CurrentKernelVersion|String|rds\_20181010|当前内核版本。

 |
|└DBInstanceStorageType|String|local\_ssd|实例储存类型，取值：

 -   **local\_ssd**：本地SSD盘；
-   **cloud\_ssd**：SSD云盘。

 |
|└DispenseMode|String|ClassicDispenseMode|分配模式。

 |
|└Extra| | |扩展信息。

 |
|└DBInstanceId| |rm-uf6wjk5xxxxxxxxxx|实例ID。

 |
|└ResourceGroupId|String|rg-acfmyxxxxxxxxxx|资源组ID。

 |
|└SecurityIPMode|String|normal|白名单模式。

 |
|└SlaveZones| | |组成SlaveZones的参数。

 |
|└ZoneId|String|cn-hangzhou-a|可用区。

 |
|└TimeZone|String|Central Standard Time|时区。

 |
|└VSwitchId|String|vsw-xxxxxx|交换机ID。

 |
|└VpcCloudInstanceId|String|vpc-23rsxdfxxxxxxx|专有网络实例ID。

 |
|└VpcId|String|vpc-xxxxxxxxx|VPC ID。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceAttribute
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDBInstanceAttributeResponse>
  <Items>
    <DBInstanceAttribute>
      <Extra>
        <DBInstanceId/>
      </Extra>
      <ConnectionString>rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com</ConnectionString>
      <AccountMaxQuantity>99999</AccountMaxQuantity>
      <CurrentKernelVersion>rds_20170714</CurrentKernelVersion>
      <DBInstanceCPU>2</DBInstanceCPU>
      <IPType>IPv4</IPType>
      <ZoneId>cn-hangzhou-f</ZoneId>
      <ReadOnlyDBInstanceIds/>
      <ConnectionMode>Standard</ConnectionMode>
      <VSwitchId>vsw-bp1w9oueixxxxx</VSwitchId>
      <VpcId>vpc-bp1opxu1zkhxxxxx</VpcId>
      <Engine>MySQL</Engine>
      <MaintainTime>18:00Z-22:00Z</MaintainTime>
      <MaxConnections>4000</MaxConnections>
      <DBInstanceType>Primary</DBInstanceType>
      <DBInstanceMemory>4096</DBInstanceMemory>
      <EngineVersion>5.7</EngineVersion>
      <DBInstanceStorageType>cloud_ssd</DBInstanceStorageType>
      <DBInstanceStatus>Running</DBInstanceStatus>
      <SecurityIPMode>normal</SecurityIPMode>
      <PayType>Prepaid</PayType>
      <SupportUpgradeAccountType>No</SupportUpgradeAccountType>
      <AccountType>Mix</AccountType>
      <LockMode>Unlock</LockMode>
      <DBInstanceNetType>Intranet</DBInstanceNetType>
      <MaxIOPS>600</MaxIOPS>
      <DBInstanceClass>mysql.n2.medium.1</DBInstanceClass>
      <DBMaxQuantity>99999</DBMaxQuantity>
      <ResourceGroupId>rg-acfmyxxxxx</ResourceGroupId>
      <DBInstanceId>rm-bp176xxxxx</DBInstanceId>
      <VpcCloudInstanceId>rm-bp176gz7xxxxx</VpcCloudInstanceId>
      <DBInstanceClassType>x</DBInstanceClassType>
      <LatestKernelVersion/>
      <InstanceNetworkType>VPC</InstanceNetworkType>
      <DBInstanceStorage>20</DBInstanceStorage>
      <SupportCreateSuperAccount>No</SupportCreateSuperAccount>
      <CreationTime>2018-11-28T01:32:08Z</CreationTime>
      <Category>Basic</Category>
      <Port>3306</Port>
      <InsId>1</InsId>
      <ExpireTime>2018-12-28T16:00:00Z</ExpireTime>
      <RegionId>cn-hangzhou</RegionId>
      <AvailabilityValue>100.0%</AvailabilityValue>
      <SecurityIPList>1.1.1.1</SecurityIPList>
    </DBInstanceAttribute>
  </Items>
  <RequestId>CFE76192-2F85-4D18-975E-465B77C129C4</RequestId>
</DescribeDBInstanceAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Items":{
		"DBInstanceAttribute":[
			{
				"AccountMaxQuantity":99999,
				"ConnectionString":"rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com",
				"Extra":{
					"DBInstanceId":{
						"DBInstanceId":[]
					}
				},
				"CurrentKernelVersion":"rds_20170714",
				"DBInstanceCPU":"2",
				"IPType":"IPv4",
				"ZoneId":"cn-hangzhou-f",
				"ConnectionMode":"Standard",
				"ReadOnlyDBInstanceIds":{
					"ReadOnlyDBInstanceId":[]
				},
				"VSwitchId":"vsw-bp1w9oueixxxxx",
				"Engine":"MySQL",
				"VpcId":"vpc-bp1opxu1zkhxxxxx",
				"MaintainTime":"18:00Z-22:00Z",
				"MaxConnections":4000,
				"DBInstanceType":"Primary",
				"DBInstanceMemory":4096,
				"EngineVersion":"5.7",
				"DBInstanceStorageType":"cloud_ssd",
				"DBInstanceStatus":"Running",
				"SecurityIPMode":"normal",
				"PayType":"Prepaid",
				"SupportUpgradeAccountType":"No",
				"AccountType":"Mix",
				"LockMode":"Unlock",
				"MaxIOPS":600,
				"DBInstanceNetType":"Intranet",
				"DBInstanceClass":"mysql.n2.medium.1",
				"DBMaxQuantity":99999,
				"DBInstanceId":"rm-bp176xxxxx",
				"ResourceGroupId":"rg-acfmyxxxxx",
				"VpcCloudInstanceId":"rm-bp176gz7xxxxx",
				"DBInstanceClassType":"x",
				"LatestKernelVersion":"",
				"InstanceNetworkType":"VPC",
				"DBInstanceStorage":20,
				"SupportCreateSuperAccount":"No",
				"CreationTime":"2018-11-28T01:32:08Z",
				"Port":"3306",
				"Category":"Basic",
				"InsId":1,
				"ExpireTime":"2018-12-28T16:00:00Z",
				"AvailabilityValue":"100.0%",
				"RegionId":"cn-hangzhou",
				"SecurityIPList":"1.1.1.1"
			}
		]
	},
	"RequestId":"CFE76192-2F85-4D18-975E-465B77C129C4"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)


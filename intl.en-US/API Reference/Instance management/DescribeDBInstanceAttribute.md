# DescribeDBInstanceAttribute {#doc_api_1101599 .reference}

You can call this operation to view the details of an RDS instance.

## Debugging {#apiExplorer .section}

You can use [OpenAPI Explorer](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceAttribute) to perform debugging.

API Explorer provides various functions to simplify API usage. For example, you can search APIs, call APIs, and generate SDK sample code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceAttribute| The operation that you want to perform. Set this parameter to DescribeDBInstanceAttribute.

 |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx| The ID of the instance. You can enter up to 30 instance IDs at a time. Separate multiple instance IDs with commas \(,\).

 |
|Expired|String|No|False| Indicates whether the instance has expired. Valid values:

 -   True
-   False

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Items|N/A|N/A| A list of instances.

 |
|DBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of an instance.

 |
|PayType|String|Postpaid| The billing method of the instance. Valid values:

 -   Postpaid: Pay-As-You-Go.
-   Prepaid: Subscription.

 |
|DBInstanceType|String|Primary| The role of the instance. Valid values:

 -   Primary: master instance.
-   Readonly: read-only instance.
-   Guard: disaster recovery instance.
-   Temp: temporary instance.

 |
|Category|String|Basic| The edition \(series\) of the instance. Valid values:

 -   Basic
-   HighAvailability
-   AlwaysOn

 |
|InstanceNetworkType|String|Classic| The intranet type of the instance. Valid values:

 -   Classic
-   VPC

 |
|RegionId|String|cn-hangzhou| The ID of the region.

 |
|ZoneId|String|cn-hangzhou-a| The ID of the zone.

 |
|ConnectionString|String|rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com| The private IP address of the instance.

 |
|Port|String|3306| The private port of the instance.

 |
|Engine|String|MySQL| The type of the database engine.

 |
|EngineVersion|String|5.5| The version of the database engine.

 |
|DBInstanceClassType|String|s| The type family of the instance. Valid values:

 -   s: shared instance.
-   x: common instance.
-   d: dedicated instance.
-   h: dedicated-host instance.

 |
|DBInstanceClass|String|rds.mys2.small| The instance type \(specifications\). For more information, see [Instance type list](../../../../intl.en-US/Product Introduction/Instance types/Instance type list.md#).

 |
|DBInstanceMemory|Long|4096| The memory of the instance. Unit: MB.

 |
|DBInstanceStorage|Integer|10| The storage capacity of the instance. Unit: GB.

 |
|DBInstanceNetType|String|Internet| The network type of the instance. Valid values:

 -   Internet
-   Intranet

 |
|DBInstanceStatus|String|Running| The status of the instance. For more information, see [Instance status table](intl.en-US/API Reference/Appendix/Instance status table.md#).

 |
|DBInstanceDescription|String|Test database| The description of the instance.

 |
|LockMode|String|Unlock| The lock mode of the instance. Valid values:

 -   Unlock: The instance is not locked, indicating the instance is operating normally.
-   ManualLock: The instance is locked manually.
-   LockByExpiration: The instance is locked automatically after the instance expires.
-   LockByRestoration: The instance is locked automatically during the instance rollback.
-   LockByDiskQuota: The instance is locked automatically due to full disk space.

 |
|LockReason|String|instance\_expired| The reason why the instance is locked.

 |
|DBMaxQuantity|Integer|200| The maximum number of databases that can be created in an instance.

 |
|AccountMaxQuantity|Integer|50| The maximum number of accounts that can be created in an instance.

 |
|CreationTime|String|2011-05-30T12:11:04Z| The time when the instance is created. Format: yyyy-MM-ddTHH:mm:ssZ \(UTC time\).

 |
|ExpireTime|String|2019-03-27T16:00:00Z| The expiration time. Format: yyyy-MM-ddTHH:mm:ssZ \(UTC time\).

 **Note:** Pay-As-You-Go instances never expire.

 |
|MaintainTime|String|00:00Z-02:00Z| The maintenance period of the instance. The value is UTC time. The value plus 8 hours is the maintenance period displayed on the web console.

 |
|AvailabilityValue|String|100.0%| The availability of the instance. Unit: %.

 |
|MaxIOPS|Integer|150| The maximum number of I/O requests per second.

 |
|MaxConnections|Integer|60| The maximum number of concurrent connections.

 |
|MasterInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of the master instance of the current instance. If this parameter is not returned \(null\), the current instance itself is a master instance.

 |
|IncrementSourceDBInstanceId|String|rm-uf6wjk5xxxxxxxxxx| The ID of the incremental data source. The incremental data source of a disaster recovery instance or read-only instance is the master instance. If this parameter is not returned \(null\), the current instance itself is a master instance.

 |
|GuardDBInstanceId|String|rm-uf64zsuxxxxxxxxxx| The ID of the disaster recovery instance \(if any\) attached to the current instance.

 |
|TempDBInstanceId|String|rm-uf64zsuxxxxxxxxxx| The ID of the temporary instance \(if any\) attached to the current instance.

 |
|ReadOnlyDBInstanceIds|N/A|N/A| The IDs of read-only instances attached to the master instance.

 |
|DBInstanceId|String|rm-bpxxxxxxxxx| The ID of a read-only instance.

 |
|AdvancedFeatures|String|LinkedServer| This parameter is only applicable to SQL Server instances and indicates advanced features. Valid values:

 -   LinkedServer
-   DistributeTransaction

 |
|AutoUpgradeMinorVersion|String|Auto| The method of upgrading an instance to a minor version. Valid values:

 -   Auto: The system automatically upgrades an instance to a minor version.
-   Manual: The system prompts you to upgrade an instance to a minor version only when the version is deprecated.

 |
|Collation|String|Chinese\_PRC\_CI\_AS| The sorting rule of character sets.

 |
|ConnectionMode|String|Standard| The access mode of the instance. Valid values:

 -   Standard: standard mode.
-   Safe: database proxy mode.

 |
|CurrentKernelVersion|String|rds\_20181010| The current kernel version.

 |
|DBInstanceStorageType|String|local\_ssd| The storage type of the instance. Valid values:

 -   local\_ssd: local SSD.
-   cloud\_ssd: cloud SSD.

 |
|DispenseMode|String|ClassicDispenseMode| The allocation mode.

 |
|Extra|N/A|N/A| The extended information about the instance.

 |
|DBInstanceId|N/A|rm-uf6wjk5xxxxxxxxxx| The ID of the instance.

 |
|MasterZone|String|5454284|The ID of the master zone.|
|ReadonlyInstanceSQLDelayedTime|String|30|After the latency of ReadonlyInstanceSQLDelayedTime, read-only instances synchronize data from the master instance. Unit: second.|
|ResourceGroupId|String|rg-acfmyxxxxxxxxxx| The ID of the resource group.

 |
|SecurityIPMode|String|normal| The IP whitelist mode.

 |
|SlaveZones|N/A|N/A| The information about SlaveZones.

 |
|ZoneId|String|cn-hangzhou-a| The ID of the zone.

 |
|TimeZone|String|Central Standard Time| The time zone.

 |
|VSwitchId|String|vsw-xxxxxx| The ID of the VSwitch.

 |
|VpcCloudInstanceId|String|vpc-23rsxdfxxxxxxx| The ID of the VPC instance.

 |
|VpcId|String|vpc-xxxxxxxxx| The ID of the VPC.

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}
http(s)://rds.aliyuncs.com/?Action=DescribeDBInstanceAttribute
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&<Common request parameters>
```

Normal response examples

`XML` format

``` {#codeblock_y8n_vy0_04z}
<DescribeDBInstanceAttributeResponse>
		  <Items>
		    <DBInstanceAttribute>
			      <Extra>
				        <DBInstanceId></DBInstanceId>
			      </Extra>
			      <ConnectionString>rm-uf6wjk5xxxxxxxxxx.mysql.rds.aliyuncs.com</ConnectionString>
			      <AccountMaxQuantity>99999</AccountMaxQuantity>
			      <CurrentKernelVersion>rds_20170714</CurrentKernelVersion>
			      <DBInstanceCPU>2</DBInstanceCPU>
			      <ZoneId>cn-hangzhou-f</ZoneId>
			      <ReadOnlyDBInstanceIds></ReadOnlyDBInstanceIds>
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
			      <LatestKernelVersion></LatestKernelVersion>
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

`JSON` format

``` {#codeblock_qxp_32m_s8d}
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
				"DBInstanceNetType":"Intranet",
				"MaxIOPS":600,
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

## Error codes {#section_pfv_06h_uxz .section}

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


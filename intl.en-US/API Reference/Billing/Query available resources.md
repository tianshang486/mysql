# Query available resources

You can call the DescribeAvailableResource operation to query the resources that are available in a region.

**Note:** You can call this operation up to 20 times within 1 minute.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeAvailableResource&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableResource|The operation that you want to perform. Set the value to **DescribeAvailableResource**. |
|InstanceChargeType|String|Yes|Postpaid|The billing method to query. Valid values:

-   **Prepaid**: subscription
-   **Postpaid**: pay-as-you-go |
|RegionId|String|No|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~26243~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-b|The ID of the zone to query. If the region contains more than one zone, separate the IDs of the zones with colons \(:\). |
|Engine|String|No|MySQL|The database engine to query. Valid values:

-   **MySQL**
-   **SQLServer**
-   **PostgreSQL**
-   **PPAS**
-   **MariaDB** |
|EngineVersion|String|No|5.7|The database engine version to query. Valid values:

-   MySQL: **5.5, 5.6, 5.7, and 8.0**
-   SQL Server: **2008r2, 2012, 2012\_ent\_ha, 2012\_std\_ha, 2012\_web, 2014\_std\_ha, 2016\_ent\_ha, 2016\_std\_ha, 2016\_web, and 2017\_ent**
-   PostgreSQL: **9.4 and 10.0**
-   PPAS: **9.3 and 10.0**
-   MariaDB: **10.3** |
|DBInstanceClass|String|No|rds.mysql.s1.small|The instance type to query. For more information, see [Primary instance types](~~26312~~). |
|OrderType|String|No|BUY|The type of purchase order to query. Set the value to **BUY**. |
|DBInstanceStorageType|String|No|local\_ssd|The storage type to query. Valid values:

-   **local\_ssd or ephemeral\_ssd**: local SSD
-   **cloud\_ssd**: standard SSD
-   **cloud\_essd**: enhanced SSD |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AvailableZones|Array| |An array that consists of the zones in which resources are available. |
|AvailableZone| | | |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Status|String|Enable|Indicates whether the resources in the region can be purchased. Valid values:

-   **Enable**: The resources in the region can be purchased.
-   **Disable**: The resources in the region cannot be purchased. |
|SupportedEngines|Array| |An array that consists of available database engines. |
|SupportedEngine| | | |
|Engine|String|MySQL|The database engine that is available. |
|SupportedEngineVersions|Array| |An array that consists of available database engine versions. |
|SupportedEngineVersion| | | |
|SupportedCategorys|Array| |An array that consists of available RDS editions. |
|SupportedCategory| | | |
|Category|String|HighAvailability|The RDS edition that is available. |
|SupportedStorageTypes|Array| |An array that consists of available storage types. |
|SupportedStorageType| | | |
|AvailableResources|Array| |An array that consists of available resources. |
|AvailableResource| | | |
|DBInstanceClass|String|rds.mysql.s1.small|The instance type that is available. |
|DBInstanceStorageRange|Struct| |An array that consists of available storage capacity ranges. |
|Max|Integer|2000|The maximum storage capacity that is available. Unit: GB. |
|Min|Integer|5|The minimum storage capacity that is available. Unit: GB. |
|Step|Integer|5|The incremental step of storage capacity. Unit: GB. |
|StorageRange|String|"\{\\"values\\":\[\{\\"max\\":2000,\\"min\\":5,\\"step\\":5\}\]\}"|The storage capacity range that is available. The range includes the maximum storage capacity, minimum storage capacity, and incremental step. |
|StorageType|String|local\_ssd|The storage type that is available. |
|Version|String|5.7|The database engine version that is available. |
|ZoneId|String|cn-hangzhou-b|The ID of the zone. |
|RequestId|String|A32E046E-2643-4B65-828D-23FEED4853A3|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeAvailableResource
&InstanceChargeType=Postpaid
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAvailableResourceResponse>
  <RequestId>A32E046E-2643-4B65-828D-23FEED4853A3</RequestId>
      <AvailableZones>
            <AvailableZone>
                  <Status>Enable</Status>
                  <RegionId>cn-hangzhou</RegionId>
                  <ZoneId>cn-hangzhou-b</ZoneId>
                  <SupportedEngines>
                        <SupportedEngine>
                              <SupportedEngineVersions>
                                    <SupportedEngineVersion>
                                          <Version>5.6</Version>
                                          <SupportedCategorys>
                                                <SupportedCategory>
                                                      <Category>HighAvailability</Category>
                                                      <SupportedStorageTypes>
                                                            <SupportedStorageType>
                                                                  <AvailableResources>
                                                                        <AvailableResource>
                                                                              <StorageRange>{"values":[{"max":2000,"min":5,"step":5}]}</StorageRange>
                                                                              <DBInstanceClass>rds.mysql.s1.small</DBInstanceClass>
                                                                              <DBInstanceStorageRange>
                                                                                    <Step>5</Step>
                                                                                    <Max>2000</Max>
                                                                                    <Min>5</Min>
                                                                              </DBInstanceStorageRange>
                                                                        </AvailableResource>
                                                                  </AvailableResources>
                                                                  <StorageType>local_ssd</StorageType>
                                                            </SupportedStorageType>
                                                      </SupportedStorageTypes>
                                                </SupportedCategory>
                                          </SupportedCategorys>
                                    </SupportedEngineVersion>
                              </SupportedEngineVersions>
                              <Engine>MySQL</Engine>
                        </SupportedEngine>
                  </SupportedEngines>
            </AvailableZone>
      </AvailableZones>
</DescribeAvailableResourceResponse>
```

`JSON` format

```
{
    "RequestId": "A32E046E-2643-4B65-828D-23FEED4853A3",
    "AvailableZones": {
        "AvailableZone": [
            {
                "Status": "Enable",
                "RegionId": "cn-hangzhou",
                "ZoneId": "cn-hangzhou-b",
                "SupportedEngines": {
                    "SupportedEngine": [
                        {
                            "SupportedEngineVersions": {
                                "SupportedEngineVersion": [
                                    {
                                        "Version": "5.6",
                                        "SupportedCategorys": {
                                            "SupportedCategory": [
                                                {
                                                    "Category": "HighAvailability",
                                                    "SupportedStorageTypes": {
                                                        "SupportedStorageType": [
                                                            {
                                                                "AvailableResources": {
                                                                    "AvailableResource": [
                                                                        {
                                                                            "StorageRange": "{\"values\":[{\"max\":2000,\"min\":5,\"step\":5}]}",
                                                                            "DBInstanceClass": "rds.mysql.s1.small",
                                                                            "DBInstanceStorageRange": {
                                                                                "Step": 5,
                                                                                "Max": 2000,
                                                                                "Min": 5
                                                                            }
                                                                        }
                                                                    ]
                                                                },
                                                                "StorageType": "local_ssd"
                                                            }
                                                        ]
                                                    }
                                                }
                                            ]
                                        }
                                    }
                                ]
                            },
                            "Engine": "MySQL"
                        }
                    ]
                }
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


# Query endpoints

You can call the DescribeDBInstanceNetInfo operation to query all the endpoints of an ApsaraDB RDS instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=DescribeDBInstanceNetInfo&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDBInstanceNetInfo|The operation that you want to perform. Set the value to **DescribeDBInstanceNetInfo**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Flag|String|No|N/A|A hidden parameter. |
|DBInstanceNetRWSplitType|String|No|Normal|The type of endpoint to query. Valid values:

 -   **Normal**
-   **ReadWriteSplitting**

 **Note:** The system returns both types of endpoints by default. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBInstanceNetInfos|Array| |An array that consists of endpoints. |
|DBInstanceNetInfo| | | |
|ConnectionString|String|rm-uf6wxxxxx.mysql.rds.aliyuncs.com|The endpoint that is used to connect to the instance. |
|IPAddress|String|192.168.12.84|The IP address that is associated with the endpoint. |
|IPType|String|Public|The network type of the instance. Valid values:

 -   If the instance resides in the classic network:
    -   **Inner**: internal network
    -   **Public**: Internet
-   If the instance resides in a virtual private cloud \(VPC\):
    -   **Private**: internal network
    -   **Public**: Internet |
|Port|String|3306|The port that is associated with the endpoint. |
|VPCId|String|vpc-uf6f7l4fg90xxxxxxxxxx|The ID of the VPC to which the instance belongs. |
|VSwitchId|String|vsw-uf6adz52c2pxxxxxxxxxx|The ID of the VSwitch associated with the specified VPC. |
|ConnectionStringType|String|Normal|The type of the endpoint. Valid values:

 -   **Normal**
-   **ReadWriteSplitting** |
|MaxDelayTime|String|12|The threshold of latency that is allowed on the read-only instances. Unit: seconds. This parameter is returned only for the read/write splitting endpoint.

 **Note:** If the latency on a read-only instance exceeds the specified threshold, ApsaraDB RDS no longer routes read requests to the read-only instance. |
|DistributionType|String|Standard|The policy that is used to allocate read weights. This parameter is returned only for a read/write splitting endpoint. Valid values:

 -   **Standard**: ApsaraDB RDS automatically allocates a read weight to each instance based on the instance specifications.
-   **Custom**: You must manually allocate a read weight to each instance. |
|DBInstanceWeights|Array| |An array that consists of read weights. This parameter is returned only when the read/write splitting function is enabled for the instance. |
|DBInstanceWeight| | | |
|DBInstanceId|String|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|DBInstanceType|String|Master|The role of the instance. Valid values:

 -   **Master**: primary
-   **Readonly**: read-only |
|Weight|String|100|The read weight of the instance. |
|Availability|String|Unavailable|The availability of the instance. Valid values:

 -   **Unavailable**
-   **Available** |
|ExpiredTime|String|1209534|The remaining time of the instance in the classic network if the instance is connected in hybrid access mode. Unit: seconds. |
|SecurityIPGroups|Array| |An array that consists of IP address whitelists. |
|securityIPGroup| | | |
|SecurityIPGroupName|String|Default|The name of the IP address whitelist. |
|SecurityIPs|String|127.0.0.1|An array that consists of IP addresses in the IP address whitelist. |
|Upgradeable|String|Disabled|Indicates whether the IP version can be updated. Valid values: **Enable and Disabled**.

 **Note:** The IP version can be updated from IPv4 to IPv6. |
|InstanceNetworkType|String|VPC|The network type of the instance. Valid values:

 -   **Classic**
-   **VPC** |
|RequestId|String|777C4593-8053-427B-99E2-105593277CAB|The ID of the request. |
|SecurityIPMode|String|safety|The whitelist mode of the instance. Valid values:

 -   **normal**: standard whitelist mode
-   **safety**: enhanced whitelist mode |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=DescribeDBInstanceNetInfo
&DBInstanceId=rm-uf6wjk5xxxxxxx
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDBInstanceNetInfoResponse>
	  <dBInstanceNetInfos>
		    <connectionString>rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com</connectionString>
		    <connectionStringType>Normal</connectionStringType>
		    <iPAddress>192.168.xx.xx</iPAddress>
		    <iPType>Public</iPType>
		    <port>3306</port>
		    <upgradeable>Disabled</upgradeable>
		    <vPCId></vPCId>
	  </dBInstanceNetInfos>
	  <instanceNetworkType>Classic</instanceNetworkType>
	  <requestId>777C4593-8053-427B-99E2-105593277CAB</requestId>
</DescribeDBInstanceNetInfoResponse>
```

`JSON` format

```
{
    "dBInstanceNetInfos": [
        {
            "connectionString": "rm-uf6wjk5xxxxxxx.mysql.rds.aliyuncs.com",
            "connectionStringType": "Normal",
            "dBInstanceWeights": [],
            "iPAddress": "192.168.xx.xx",
            "iPType": "Public",
            "port": "3306",
            "securityIPGroups": [],
            "upgradeable": "Disabled",
            "vPCId": ""
        }
    ],
    "instanceNetworkType": "Classic",
    "requestId": "777C4593-8053-427B-99E2-105593277CAB"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


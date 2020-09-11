# Modify proxy endpoint

You can call the ModifyDBProxyEndpointAddress operation to modify the endpoint that is used to connect to the dedicated proxies of an ApsaraDB for RDS instance.

The dedicated proxy feature provides advanced functions, such as read/write splitting, connection pool, and transaction splitting. For more information, see [Dedicated proxy](~~138705~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyDBProxyEndpointAddress&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDBProxyEndpointAddress|The operation that you want to perform. Set the value to **ModifyDBProxyEndpointAddress**. |
|DBInstanceId|String|Yes|rm-t4n3axxxxx|The ID of the instance. |
|DBProxyEndpointId|String|Yes|ta9um4xxxxx|The ID of the endpoint that is used to connect to the dedicated proxies of the instance. |
|DBProxyConnectStringNetType|String|No|Public|The network type of the endpoint. Valid values:

-   **Public**
-   **VPC**
-   **Classic**

Default value: **Classic**. |
|DBProxyNewConnectString|String|No|test123456|The prefix of the endpoint.

**Note:** You must specify either the **DBProxyNewConnectString** or **DBProxyNewConnectStringPort** parameter. |
|DBProxyNewConnectStringPort|String|No|3307|The port associated with the endpoint.

**Note:** You must specify either the**DBProxyNewConnectString**or**DBProxyNewConnectStringPort**parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|50F6C32B-DD73-4DA1-ADA2-0EAF2B0FCD8A|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyDBProxyEndpointAddress
&DBInstanceId=m-t4n3axxxxx
&DBProxyEndpointId=ta9um4xxxxx
&DBProxyNewConnectString=test123456
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBProxyEndpointAddressResponse>
  <RequestId>50F6C32B-DD73-4DA1-ADA2-0EAF2B0FCD8A</RequestId>
</ModifyDBProxyEndpointAddressResponse>
```

`JSON` format

```
{
    "RequestId": "50F6C32B-DD73-4DA1-ADA2-0EAF2B0FCD8A"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|ParameterLeastAssociate|Must input at least one optional parameter.|The error message returned because neither of the optional parameters is specified. When you clone an RDS instance, you must specify either the cloning time or the used backup set.|
|400|InvalidConnectionString.Format|Specified connection string is not valid.|The error message returned because the specified endpoint is invalid.|
|400|InvalidPort.Malformed|Specified port is not valid.|The error message returned because the specified port is invalid.|
|400|InvalidConnectionString.Duplicate|Specified connection string already exists in the Aliyun RDS.|The error message returned because the specified endpoint is used by another RDS instance.|
|404|InsufficientResourceCapacity|There is insufficient capacity available for the requested instance.|The error message returned because the available resources are insufficient. Please try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


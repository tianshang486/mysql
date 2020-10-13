# Manually renew an ApsaraDB for RDS instance

Manually renews an ApsaraDB for RDS instance.

Before you call this operation, make sure that you fully understand the billing methods and [pricing](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing) of ApsaraDB for RDS.

Before you call this operation, make sure that the following requirements are met:

-   You can only renew subscription instances.
-   You must confirm that your payment account has sufficient balance or credit.

**Note:** By default, coupons available under your account are preferentially used for payment.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=RenewInstance&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RenewInstance|The operation that you want to perform. Set the value to **RenewInstance**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxxxxx|The ID of the instance to be renewed. |
|Period|Integer|Yes|12|The renewal period of the subscription instance. Unit: months. Valid values:

-   **1-9**
-   **12**
-   **24**
-   **36**
-   **48**
-   **60** |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotency of requests. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|AutoPay|String|No|True|Specifies whether payment is automatically made during the renewal. Valid values:

-   **True**: Automatic payment is enabled. Make sure that your account has adequate balance.
-   **False**: Automatic payment is disabled. You have to manually pay the order in the console. Log on to the console. In the upper-right corner, choose **Billing Management \> Billing Management**. On the Billing Management page, click **Bills**. On the Unpaid tab, click Make Payment in the Actions column.

Default value:**False**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|Long|201815745430941|The ID of the order. |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=RenewInstance
&DBInstanceId=rm-uf6wjk5xxxxxxxxxx
&Period=12
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RenewInstanceResponse>
      <OrderId>20286717xxxxx</OrderId>
      <RequestId>E10319A3-B96A-46B0-81CE-D610DC891409</RequestId></RenewInstanceResponse>
```

`JSON` format

```
{
    "OrderId": "20286717xxxxx",
    "RequestId": "E10319A3-B96A-46B0-81CE-D610DC891409"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


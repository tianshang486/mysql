# Change billing method

You can call the TransformDBInstancePayType operation to change the billing method of an ApsaraDB RDS instance.

**Note:**

-   If you change the billing method from subscription to pay-as-you-go, you will receive a refund. For more information, see [Switch the billing method from subscription to pay-as-you-go](~~161875~~).
-   If the balance of your Alibaba Cloud account is insufficient, you cannot change the billing method from pay-as-you-go to subscription.
-   This operation is not supported for instances that have unfinished configuration change orders.
-   This operation is not supported for instances that are created in dedicated clusters.

ApsaraDB RDS supports the following two billing methods:

-   Subscription: A subscription instance is an instance that you can subscribe to for a specified period of time and pay for up front. Subscription billing is more cost-effective than pay-as-you-go billing. Therefore, we recommend that you select subscription billing with a longer commitment. You can receive larger discounts for longer subscription periods.
-   Pay-as-you-go: A pay-as-you-go instance is charged per hour based on your actual resource usage. The hourly fee is calculated based on the instance type you specified in the purchase order and is deducted accordingly from the balance of your Alibaba Cloud account. We recommend that you select pay-as-you-go billing for short-term use. If you no longer need your pay-as-you-go instance, you can release it to reduce costs.

For more information about the billing methods, see [Pricing, billable items, and billing methods](~~45020~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=TransformDBInstancePayType&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TransformDBInstancePayType|The operation that you want to perform. Set the value to **TransformDBInstancePayType**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxx|The ID of the instance. |
|PayType|String|Yes|Prepaid|The billing method of the instance. Valid values:

 -   **Postpaid**: pay-as-you-go
-   **Prepaid**: subscription |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|UsedTime|Integer|No|1|The subscription period of the instance if the instance uses the subscription billing method. Valid values:

 -   If you set the **Period** parameter to **Year**, the value of the UsedTime parameter ranges from **1 to 5**.
-   If you set the **Period** parameter to **Month**, the value of the UsedTime parameter ranges from **1 to 9**.

 **Note:** This parameter must be specified if you set the **PayType** parameter to **Prepaid**. |
|Period|String|No|Month|The renewal period of the instance if the instance uses the subscription billing method. Valid values:

 -   **Year**
-   **Month**

 **Note:** This parameter must be specified if you set the **PayType** parameter to **Prepaid**. |
|BusinessInfo|String|No|None|The extended business information of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ChargeType|String|Prepaid|The billing method of the instance. |
|DBInstanceId|String|rm-uf6wjk5xxxxxx|The ID of the instance. |
|ExpiredTime|String|2020-04-20T10:00:00Z|The expiration time of the instance.

 **Note:** If you change the billing method to pay-as-you-go, this parameter is not returned. |
|OrderId|Long|205157600280623|The ID of the order. |
|RequestId|String|5E6E09DE-5B12-4BFF-A55E-1C86EDE06D9A|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=TransformDBInstancePayType
&DBInstanceId=rm-uf6wjk5xxxxxx
&PayType=Prepaid
&UsedTime=3
&Period=Month
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TransformDBInstancePayTypeResponse>
  <ChargeType>Prepaid</ChargeType>
  <DBInstanceId>rm-uf6wjk5xxxxxx</DBInstanceId>
  <ExpiredTime>2020-04-20T10:00:00Z</ExpiredTime>
  <OrderId>205157600280623</OrderId>
  <RequestId>5E6E09DE-5B12-4BFF-A55E-1C86EDE06D9A</RequestId>
</TransformDBInstancePayTypeResponse>
```

`JSON` format

```
{
    "ChargeType":"Prepaid",
    "DBInstanceId":"rm-uf6wjk5xxxxxx",
    "ExpiredTime":"2020-04-20T10:00:00Z",
    "OrderId":205157600280623,
    "RequestId":"5E6E09DE-5B12-4BFF-A55E-1C86EDE06D9A"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|InvalidDBInstanceName.NotFound|The specified DB instance name does not exist.|The error message returned because the specified DBInstanceId does not exist. Enter a valid DBInstanceId and try again.|
|400|InvalidOrderCharge.NotSupport|The specified order charge does not support in RDS.|The error message returned because ApsaraDB RDS does not support the payment method. Submit a ticket.|
|400|InvalidOrderTask.NotSupport|The Current InstanceId exist Order Task in RDS.|The error message returned because the instance has unfinished orders. Try again later.|
|400|InvalidPaymentMethod.Incomplete|No payment method is specified for your account. We recommend that you add a payment method.|The error message returned because your Alibaba Cloud account does not have a valid payment method. Add a valid payment method and try again.|
|400|InvalidOldInstanceType.NotSupport|Specified oldInstanceType does not support in RDS.|The error message returned because the instance does not support this operation.|
|403|OperationDenied.LockMode|The operation is not permitted when the instance locked.|The error message returned because the instance is locked.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


# Modify parameters of an ApsaraDB for RDS instance

Modifies parameters of an ApsaraDB for RDS instance.

You can modify the parameters directly or by using a parameter template. After you submit the parameter reconfiguration request, ApsaraDB for RDS starts a task to apply the new parameter values to the instance. If a new parameter value takes effect only after the instance restarts, ApsaraDB for RDS restarts the instance. For more information about the reconfigurable parameters, see [Use the console to set parameters](~~26179~~).

**Note:** Before executing a parameter reconfiguration task, ApsaraDB for RDS checks whether the target parameters exist, whether they are reconfigurable, and whether the new parameter values are valid.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Rds&api=ModifyParameter&type=RPC&version=2014-08-15)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyParameter|The operation that you want to perform. Set the value to **ModifyParameter**. |
|DBInstanceId|String|Yes|rm-uf6wjk5xxxxxxx|The ID of the instance. |
|Parameters|String|Yes|\{"delayed\_insert\_timeout":"600","max\_length\_for\_sort\_data":"2048"\}|The JSON strings of parameters and their values. All the parameter values are of the string type. Format: \{"Parameter name 1": "Parameter value 1", "Parameter name 2": "Parameter value 2"...\}

 **Note:** If you specify this parameter, you do not need to specify the **ParameterGroupId** parameter. |
|ClientToken|String|No|ETnLKlblzczshOTUbOCzxxxxxxxxxx|The client token that is used to ensure the idempotency of requests. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Forcerestart|Boolean|No|false|Specifies whether the modified parameters take effect only after the instance restarts. Valid values:

 -   **true**: The system forcibly restarts the instance. If a new parameter value takes effect only after an instance restarts, you must set this parameter to true. Otherwise, the new parameter value cannot take effect.
-   **false**: The system does not forcibly restart the instance.

 Default value: **false**. |
|ParameterGroupId|String|No|rpg-xxxxxxxxx|The ID of the parameter template.

 **Note:**

-   If you specify this parameter, you do not need to specify the **Parameters** parameter.
-   If applying the parameter template requires an instance restart, you must specify the **Forcerestart** parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|542BB8D6-4268-45CC-A557-B03EFD7AB30A|The ID of the request. |

## Examples

Sample requests

```
http(s)://rds.aliyuncs.com/? Action=ModifyParameter
&DBInstanceId=rm-uf6wjk5xxxxxxx
&Parameters={"delayed_insert_timeout":"600","max_length_for_sort_data":"2048"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyParameterResponse>
         <RequestId>542BB8D6-4268-45CC-A557-B03EFD7AB30A</RequestId>
</ModifyParameterResponse>
```

`JSON` format

```
{
       "RequestId":"542BB8D6-4268-45CC-A557-B03EFD7AB30A"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Rds).


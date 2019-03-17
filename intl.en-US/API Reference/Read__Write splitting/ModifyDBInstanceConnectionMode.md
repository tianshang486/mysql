# ModifyDBInstanceConnectionMode {#reference_pyz_mm2_12b .reference}

## Description {#section_l21_v32_12b .section}

This API is used to enable or disable the database proxy function. This API is no longer supported.

**Note:** This API is no longer supported.

## Request parameters {#section_qzx_w32_12b .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|Required parameter. Value: ModifyDBInstanceConnectionMode.|
|DBInstanceId|String|Yes|Instance ID|
|ConnectionMode|String|Yes| -   Performance: Disable the database proxy function.
-   Safe: Enable the database proxy function.

 |

## Response parameters {#section_rpk_z32_12b .section}

|Name|Type|Description|
|----|----|-----------|
|<Common return parameters\>|-|For more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|


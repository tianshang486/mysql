# Query whether SQL audit is enabled {#reference_wvs_k23_12b .reference}

## Description {#section_l21_v32_12b .section}

This API is used to query whether SQL collection is enabled for the specified RDS instance.

## Request parameters {#section_qzx_w32_12b .section}

|Name|Type|Required or not|Description|
|----|----|---------------|-----------|
|Action|String|Yes|Required parameter. Value: DescribeSQLCollectorPolicy.|
|DBInstanceId|String|Yes|Instance ID|

## Return parameters {#section_a5x_zlh_12b .section}

|Name|Type|Description|
|----|----|-----------|
|<Public Return Parameters\>|-|For more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|SQLCollectorStatus|String| -   Enable: SQL collection is enabled.
-   Disabled: SQL collection is disabled.

 |


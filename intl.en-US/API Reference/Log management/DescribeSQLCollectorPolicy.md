# DescribeSQLCollectorPolicy {#reference_wvs_k23_12b .reference}

You can call this operation to check whether SQL collection is enabled for an instance.

**Note:** This operation is not applicable to SQL Server 2017 Cluster Edition instances.

## Request parameters {#section_qzx_w32_12b .section}

|Parameter|Type|Required?|Description|
|---------|----|---------|-----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeSQLCollectorPolicy.|
|DBInstanceId|String|Yes|The ID of the instance.|

## Response parameters {#section_a5x_zlh_12b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|<Common response parameters\>|-|For more information, see [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|SQLCollectorStatus|String|Valid values: -   Enable SQL.
-   Disabled SQL.

 |


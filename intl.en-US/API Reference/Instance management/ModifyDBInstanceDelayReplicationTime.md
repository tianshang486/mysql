# ModifyDBInstanceDelayReplicationTime {#reference_j4c_yrq_p2b .reference}

This API is used to modify the replication delay of read-only instances. This API is no longer supported.

**Note:** This API is no longer supported.

## Request parameters {#section_qhs_w54_p2b .section}

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|Action|String|Yes|Action to perform. Value: ModifyDBInstanceDelayedReplicationTime|
|DBInstanceId|String|Yes|Read-only instance ID.|
|ReadSQLReplicationTime|Integer|Yes|Replication delay of read-only instances. Unit: second. Default value: 0.|

## Response parameters {#section_mx3_1x4_p2b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|RequestId|String|See [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|DBInstanceId|String|Instance ID.|
|DelayedReplicationTime|String|Replication delay.|
|TaskId|String|Task ID.|


# DescribeDBInstanceSwitchLog {#reference_lfx_n4p_p2b .reference}

This API is used to view the master/slave switchover log. This API is no longer supported.

## Description {#section_pyg_v54_p2b .section}

**Note:** This API is no longer supported.

## Request parameters {#section_qhs_w54_p2b .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|Required parameter. Value: DescribeDBInstanceSwitchLog|
|DBInstanceId|String|Yes|Instance ID.|
|StartTime|String|Yes|Log start time. Example: 2011-06-11T15:00Z|
|EndTime|String|Yes|Log end time, whch must be later than the start time. Example: 2011-06-11T16:00Z|
|PageSize|Integer|Yes|Maximum number of records on each page. Values: 30/50/100. Default value: 30|
|PageNumber|Integer|Yes|Page number, which is greater than 0 and does not exceed 30. Default value: 1|

## Response parameters {#section_mx3_1x4_p2b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|RequestId|String|See [Public parameters](intl.en-US/API Reference/Use APIs/Public parameters.md#).|
|DBInstanceId|String|Instance ID.|
|TotalRecordCount|Integer|Total number of records.|
|PageNumber|Integer|Current page number.|
|PageRecordCount|Integer|Maximum number of records on each page.|
|Items|List|List of swithover log entries.|

## Items {#section_j2h_mbq_p2b .section}

|Parameter|Type|Description|
|---------|----|-----------|
|SwitchId|String|Instance ID.|
|SwitchCauseCode|String|Reason for the switchover.|
|SwitchStartTime|String|Start time of the switchover.|
|SwitchFinishTime|String|End time of the switchover.|
|TotalSessions|String|Total number of sessions at the time of the switchover.|
|AffectedSessions|String|Number of sessions affected by the switchover|


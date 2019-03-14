# DescribeDBInstanceSwitchLog {#reference_lfx_n4p_p2b .reference}

该接口用于查看实例的主备切换日志，已下线。

## 描述 {#section_pyg_v54_p2b .section}

适用于MySQL高可用版实例、SQL Server实例、PostgreSQL实例、PPAS实例。

**说明：** 该API已下线。

## 请求参数 {#section_qhs_w54_p2b .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|系统规定参数，取值为：DescribeDBInstanceSwitchLog。|
|DBInstanceId|String|是|实例ID。|
|StartTime|String|是|查询开始时间，格式如：2011-06-11T15:00Z。|
|EndTime|String|是|查询结束时间，格式如：2011-06-11T16:00Z，必须大于查询开始时间。|
|PageSize|Integer|是|每页记录数，取值：30/50/100，默认值：30。|
|PageNumber|Integer|是|页码，取值为：大于0，且不超过30。默认值：1。|

## 返回参数 {#section_mx3_1x4_p2b .section}

|名称|类型|描述|
|--|--|--|
|RequestId|String|详见[公共参数](intl.zh-CN/API参考/使用API/公共参数.md#)。|
|DBInstanceId|String|实例ID。|
|TotalRecordCount|Integer|总记录数。|
|PageNumber|Integer|当前页数。|
|PageRecordCount|Integer|每页显示记录数。|
|Items|List|主备日志列表。|

## Item数据格式 {#section_j2h_mbq_p2b .section}

|名称|类型|描述|
|--|--|--|
|SwitchId|String|切换实例的ID。|
|SwitchCauseCode|String|切换原因。|
|SwitchStartTime|String|切换开始时间。|
|SwitchFinishTime|String|切换结束时间。|
|TotalSessions|String|切换时总会话数。|
|AffectedSessions|String|切换时影响会话数。|


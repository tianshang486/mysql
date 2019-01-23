# CalculateDBInstanceWeight {#reference_n4p_cjf_12b .reference}

## 描述 {#section_l21_v32_12b .section}

该接口用于计算系统指定的权重。如果是自定义读权重，请参见[DescribeDBInstanceNetInfo](intl.zh-CN/API参考/网络管理/DescribeDBInstanceNetInfo.md#)。

**说明：** 

-   适用于MySQL实例和SQL Server 2017集群版实例。
-   主实例必须在没有被锁定的情况下才能进行查询，否则操作将失败。

## 请求参数 {#section_qzx_w32_12b .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|系统规定参数，取值为CalculateDBInstanceWeight。|
|DBInstanceId|String|是|主实例ID。|

## 返回参数 {#section_rpk_z32_12b .section}

|参数|类型|说明|
|--|--|--|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/使用API/公共参数.md#)。|
|DBInstanceWeights|List|系统实时计算的实例权重信息。|

## DBInstanceWeight {#section_avj_3jf_12b .section}

|名称|类型|描述|
|--|--|--|
|DBInstanceId|String|只读实例ID。|
|DBInstanceType|String|实例类型：-   Master：主实例
-   Readonly：只读实例

|
|Weight|String|系统实时计算的实例权重。|


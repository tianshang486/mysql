# CreateDiagnosticReport {#reference_dhm_5ff_12b .reference}

该接口用于实时生成诊断报告，已下线。

## 描述 {#section_l21_v32_12b .section}

该接口用于实时生成诊断报告。

**说明：** 该API已下线，您可以在控制台上手动创建诊断报告。

## 请求参数 {#section_qzx_w32_12b .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|系统规定参数，取值为CreateDiagnosticReport。|
|DBInstanceId|String|是|实例ID。|
|StartTime|String|否|监控数据起始时间，格式示例为2012-06-11T15:00Z。若不传入StartTime，则系统会使用当前时间前1个小时的时间。|
|EndTime|String|否|监控数据结束时间，格式示例为2012-06-11T15:00Z。与StartTime的间隔不得超过24小时。若不传入EndTime，默认是StartTime的值加一个小时。|

## 返回参数 {#section_rpk_z32_12b .section}

|参数|类型|说明|
|--|--|--|
|<公共返回参数\>|-|详见[公共参数](cn.zh-CN/API参考/使用API/公共参数.md#)。|
|RequestId|String|请求ID。|
|ReportId|String|报告ID。|

## 请求示例 {#section_l4g_pj2_12b .section}

```

https://rds.aliyuncs.com/?Action=CreateDiagnosticReport
&DBInstanceId=rm-bp1842vmucXXXXXX
&<公共请求参数>
```

## 返回示例 {#section_xtg_rj2_12b .section}

**XML格式**

```
<DeleteDBInstanceResponse>  
         <ReportId>10058234</ReportId><RequestId>C6EE1CE1-6ADF-4D9B-BD9A-114EB6221F02</RequestId>
</DeleteDBInstanceResponse>
```


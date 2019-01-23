# ModifyDBInstanceSpec {#reference_ddv_lp2_12b .reference}

## 描述 {#section_l21_v32_12b .section}

该接口用于变更实例的规格或者存储空间，使用该接口时必须满足如下条件，否则操作将失败：

-   实例状态为运行中。
-   实例中没有正在执行的的备份任务。
-   请求参数中必须至少指定实例规格（DBInstanceClass）或存储空间（DBInstanceStorage）其中一个参数。
-   若降低磁盘空间配置，输入的磁盘空间不能小于实际使用空间大小的1.1倍。
-   当前只支持对常规实例和只读实例变更配置，不支持灾备实例和临时实例。

## 请求参数 {#section_qzx_w32_12b .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是|系统规定参数，取值为ModifyDBInstanceSpec。|
|DBInstanceId|String|是|需要变更配置的实例。|
|PayType|String|是|计费方式：-   Postpaid：按量付费。
-   Prepaid：包年包月。

|
|DBInstanceClass|String|否|实例规格，详见[实例规格表](../../../../../intl.zh-CN/云数据库RDS简介/实例规格/实例规格表.md#)。|
|DBInstanceStorage|Integer|否|自定义存储空间，取值必须为5的整数倍，取值范围如下：-   MySQL为\[5,2000\]
-   SQL Server为\[10,3000\]
-   PostgreSQL为\[5,2000\]
-   PPAS为\[250,500\]
-   MariaDB为\[20,1000\]

不同付费方式和不同版本实例，支持的取值范围不同，请以控制台创建实例页面为准。

|
|EffectiveTime|String|否|设置实例变更配置的生效时间：-   Immediate：立即生效，默认为；立即生效。
-   MaintainTime：在实例可运维时间段内生效。实例的可运维时间段设置请参见[ModifyDBInstanceMaintainTime](intl.zh-CN/API参考/实例管理/ModifyDBInstanceMaintainTime.md#)。

|

## 返回参数 {#section_y43_h32_12b .section}

|名称|类型|描述|
|--|--|--|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/使用API/公共参数.md#)。|

## 请求示例 {#section_l4g_pj2_12b .section}

```
https://rds.aliyuncs.com/?Action=ModifyDBInstanceSpec
&DBInstanceId=rdsaiiabnaiiabn
&PayType=Postpaid
&DBInstanceStorage=10
&<公共请求参数>
```

## 返回示例 {#section_xtg_rj2_12b .section}

**XML格式**

```
<ModifyDBInstanceSpecResponse>
         <RequestId>3C5CFDEE-F774-4DED-89A2-1D76EC63C575</RequestId>
</ModifyDBInstanceSpecResponse>
```

**JSON格式**

```
{
    "RequestId": " 3C5CFDEE-F774-4DED-89A2-1D76EC63C575 "
  }
```


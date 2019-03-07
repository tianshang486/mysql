# 创建PostgreSQL只读实例 {#concept_gsm_zz1_ygb .concept}

您可以通过创建只读实例满足大量的数据库读取需求，增加应用的吞吐量。创建只读实例相当于复制了一个主实例，数据与主实例一致，主实例的数据更新也会自动同步到所有只读实例。

关于只读实例的更多介绍，请参见[PostgreSQL只读实例简介](intl.zh-CN/RDS for PostgreSQL 快速入门/只读实例/PostgreSQL只读实例简介.md#)。

## 前提条件 {#section_kdj_3gb_ygb .section}

-   主实例版本为PostgreSQL 10.0。
-   主实例规格不低于8核32G（独享套餐）。

## 注意事项 {#section_dbp_zq5_vdb .section}

-   只能在主实例内创建只读实例，不能将已有实例切换为只读实例。
-   由于创建只读实例时是从备实例复制数据，因此不会影响主实例。
-   只读实例的参数不继承主实例上的参数设置，会生成默认的参数值，可以在只读实例的控制台上进行修改。
-   只读实例的规格和存储空间不能低于主实例。
-   最多创建5个只读实例。
-   计费方式：按量付费，即每小时扣费一次，费用和相同规格的按量付费主实例价格一致。

## 创建只读实例 { .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155192193536543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在页面右侧单击**添加只读实例**。

    ![添加只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/155192193539780_zh-CN.png)

5.  在购买页面，设置只读实例的参数，然后单击**立即购买**。

    ![购买界面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/155192193539782_zh-CN.png)

    **说明：** 

    -   专有网络VPC：建议选择与主实例相同的VPC。
    -   规格和存储空间：只读实例的规格和存储空间不能低于主实例。
    -   数量：根据业务量购买，多个只读实例可以提高可用性，最多5个。
6.  在**订单确认**页面，确认订单信息，勾选**《产品服务条款》和《服务级别协议》和《使用条款》**，单击**去支付**，根据提示完成支付。

几分钟后，该只读实例即创建成功。

## 查看只读实例 {#section_dgy_ylr_52b .section}

**在实例列表中查看只读实例**

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择只读实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155192193536543_zh-CN.png)

3.  在实例列表中找到只读实例，单击该只读实例的ID。

    ![选择只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/155192193539783_zh-CN.png)


**在主实例的基本信息页面查看只读实例**

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择主实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155192193536543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在主实例的**基本信息**页面，把鼠标悬停于只读实例的数量上，单击只读实例的ID。

    ![主实例内跳转只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/155192193539784_zh-CN.png)


## 查看只读实例的延迟时间 {#section_sww_dv5_vdb .section}

只读实例同步主实例的数据时，可能会有一定的延迟。您可以在只读实例的基本信息页面查看延迟时间。

![只读实例延迟](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133902/155192193539785_zh-CN.png)

## 相关API {#section_hcn_555_jgb .section}

|API|描述|
|---|--|
|[CreateReadOnlyDBInstance](../intl.zh-CN/API参考/实例管理/CreateReadOnlyDBInstance.md#)|创建RDS只读实例|


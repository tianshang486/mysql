# 备份MySQL数据 {#concept_l1m_xgn_ydb .concept}

备份数据用于应付数据丢失或损坏，您可以设置备份策略自动备份MySQL数据和日志，或者手动备份MySQL数据。

## 注意事项 {#section_jyb_zgx_wfb .section}

-   实例备份文件占用备份空间，空间使用量超出免费的额度将会产生额外的费用，请合理设计备份周期，以满足业务需求的同时，兼顾备份空间的合理利用。关于免费额度详情，请参见[查看备份空间免费额度](cn.zh-CN/RDS for MySQL 用户指南/备份数据/查看备份空间免费额度.md#)。
-   关于具体的计费方式与收费项，请参见[计费方式与收费项](../cn.zh-CN/云数据库RDS价格/计费方式与收费项.md#)。
-   关于备份空间使用量的计费标准，请参见[云数据库 RDS 详细价格信息](https://www.aliyun.com/price/product#/rds/detail)。
-   备份期间不要执行DDL操作，避免锁表导致备份失败。
-   尽量选择业务低峰期进行备份。
-   若数据量较大，花费的时间可能较长，请耐心等待。
-   备份文件有保留时间，请及时下载需要保留的备份文件到本地。

## 备份策略 {#section_oyj_3k4_ydb .section}

阿里云数据库支持数据备份和日志备份。如要按照时间点恢复数据，需启用日志备份。各类型数据库备份策略如下：

|数据库类型|数据备份|日志备份|
|-----|----|----|
|MySQL| -   MySQL 5.5/5.6/5.7 本地SSD盘（含高可用版和金融版）：
    -   自动备份支持全量物理备份。
    -   手动备份支持全量物理备份、全量逻辑备份和单库逻辑备份。
-   MySQL 5.7 SSD云盘（高可用版）：

仅支持快照备份，可恢复至新建实例，不支持下载。

-   MySQL 5.7 SSD云盘（基础版）：

仅支持快照备份，可恢复至新建实例，不支持下载。


 | -   Binlog文件会占用实例的磁盘容量。
-   Binlog大小超过500MB或写入超过6小时就会切换到新的Binlog文件继续写入，老的Binlog文件会异步上传。
-   您可以通过[一键上传 Binlog](https://help.aliyun.com/document_detail/60546.html?spm=a2c4g.11186623.2.6.JGyUIA)功能（免费）将 Binlog 文件上传至 OSS，不影响实例的数据恢复功能，Binlog 也不再占用实例磁盘空间。

 **说明：** 

-   基础版暂不支持一键上传Binlog。
-   不支持访问Binlog文件所在的OSS存储空间。

 |

## 设置自动备份MySQL数据 {#section_f33_lk4_ydb .section}

阿里云数据库会执行用户设定的备份策略，自动备份数据库。

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com)。
2.  选择目标实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/154882903036543_zh-CN.png)

3.  单击目标实例的ID，进入基本信息页面。
4.  在菜单中选择**备份恢复**。
5.  在备份恢复页面中选择 **备份设置**，单击**编辑**。
6.  在备份设置页面设置备份规格，单击**确定**。参数说明如下：

    |参数|说明|
    |--|--|
    |数据备份保留|备份文件可以保留7~730天，默认为7天。**说明：** MySQL 5.7 SSD云盘（基础版）的备份文件保存7天，不可修改。

|
    |备份周期|可以设置为一星期中的某一天或者某几天。|
    |备份时间|可以设置为任意时段，以小时为单位，建议设置为业务低峰期时间。|
    |日志备份|日志备份的开关。**说明：** 关闭日志备份会导致所有日志备份被清除，并且无法使用按时间点恢复数据的功能。

|
    |日志备份保留|     -   日志备份文件保留的天数，默认为 7 天。
    -   可以设置为 7~730 天，且必须小于等于数据备份天数。
 **说明：** MySQL 5.7 SSD云盘（基础版）的备份文件保存7天，不可修改。

 |

    ![备份设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/67073/154882903037578_zh-CN.png)


## 手动备份MySQL数据 {#section_yvd_yk4_ydb .section}

本例以MySQL 5.7 本地SSD盘（高可用版）单库逻辑备份为例。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择目标实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/154882903036543_zh-CN.png)

3.  单击目标实例的 ID，进入基本信息页面。
4.  单击页面右上角的**备份实例**，打开备份实例对话框。

    ![备份MySQL数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7964/15488290304105_zh-CN.png)

    **说明：** 

    -   备份方式、备份策略：各引擎支持的备份策略不同，请参见[表 1](#table_uwl_3k4_ydb)。
    -   单库备份时，选择左侧的数据库，单击**\>**将要备份的数据库加入列表。若您还没有数据库，请先[创建数据库](../cn.zh-CN/RDS for MySQL 快速入门/初始化配置/创建账号和数据库.md#)。
5.  设置好备份方式、备份策略，单击**确定**。

## 常见问题 {#section_h54_lrx_pgb .section}

1.  RDS for MySQL的数据备份是否可以关闭？

    答：不可以关闭。可以减少备份频率，一周至少2次。数据备份保留天数最少7天，最多730天。

2.  RDS for MySQL的日志备份是否可以关闭？

    答：可以关闭（基础版除外）。备份设置内关闭日志备份开关即可。


## 相关文档 {#section_wfb_2ft_cgb .section}

-   [下载数据备份和日志备份](cn.zh-CN/RDS for MySQL 用户指南/备份数据/下载数据备份和日志备份.md#)
-   [恢复MySQL数据](cn.zh-CN/RDS for MySQL 用户指南/恢复数据/恢复MySQL数据.md#)

## 相关API {#section_hcn_555_jgb .section}

|API|描述|
|---|--|
|[CreateBackup](../cn.zh-CN/API参考/备份恢复/CreateBackup.md#)|创建备份|
|[DescribeBackups](../cn.zh-CN/API参考/备份恢复/DescribeBackups.md#)|查看备份列表|


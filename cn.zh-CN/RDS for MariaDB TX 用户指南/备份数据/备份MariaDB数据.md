# 备份MariaDB数据 {#concept_l1m_xgn_ydb .concept}

您可以通过设置备份策略调整RDS数据备份和日志备份的周期来实现自动备份，也可以手动备份RDS数据。

## 注意事项 {#section_rdy_k15_1gb .section}

-   实例备份文件占用备份空间，空间使用量超出免费的额度将会产生额外的费用，请合理设计备份周期，以满足业务需求的同时，兼顾备份空间的合理利用。关于免费额度详情，请参见[查看备份空间免费额度](cn.zh-CN/RDS for MariaDB TX 用户指南/备份数据/查看备份空间免费额度.md#)。
-   关于具体的计费方式与收费项，请参见[计费方式与收费项](../cn.zh-CN/云数据库RDS价格/计费方式与收费项.md#)。
-   关于备份空间使用量的计费标准，请参见[云数据库 RDS 详细价格信息](https://www.aliyun.com/price/product#/rds/detail)。
-   备份期间不要执行DDL操作，避免锁表导致备份失败。
-   尽量选择业务低峰期进行备份。
-   若数据量较大，花费的时间可能较长，请耐心等待。
-   备份文件有保留时间，请及时下载需要保留的备份文件到本地。

## 备份策略 {#section_oyj_3k4_ydb .section}

|数据库类型|数据备份|日志备份|
|-----|----|----|
|MariaDB|支持快照备份，不支持物理备份和逻辑备份。| -   Binlog文件会占用实例的磁盘容量。
-   Binlog大小超过500MB或写入超过6小时就会切换到新的Binlog文件继续写入，老的Binlog文件会异步上传。
-   您可以通过[一键上传 Binlog](https://help.aliyun.com/document_detail/60546.html?spm=a2c4g.11186623.2.6.JGyUIA)功能（免费）将 Binlog 文件上传至 OSS，不影响实例的数据恢复功能，Binlog 也不再占用实例磁盘空间。

 **说明：** 不支持访问Binlog文件所在的OSS存储空间。

 |

## 设置自动备份 {#section_f33_lk4_ydb .section}

阿里云数据库会执行用户设定的备份策略，自动备份数据库。

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com)。
2.  选择目标实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155201425036543_zh-CN.png)

3.  单击目标实例的ID，进入基本信息页面。
4.  在菜单中选择 **备份恢复**。
5.  在 备份恢复页面中选择 **备份设置**，单击 **编辑**。
6.  在 备份设置页面设置备份规格，单击 **确定**。参数说明如下：

    |参数|说明|
    |--|--|
    |数据备份保留|默认为7天，可以设置为 7~730 天。|
    |备份周期|默认每天都进行备份，不可修改。|
    |备份时间|可以设置为任意时段，以小时为单位。|
    |日志备份|日志备份的开关。**说明：** 关闭日志备份会导致所有日志备份被清除，并且无法使用按时间点恢复数据的功能。

|
    |日志备份保留|     -   日志备份文件保留的天数，默认为 7 天。
    -   可以设置为 7~730 天，且必须小于等于数据备份天数。
 |

    ![备份设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/63819/155201425040330_zh-CN.png)


## 常见问题 {#section_h54_lrx_pgb .section}

1.  RDS for MariaDB TX的数据备份是否可以关闭？

    答：不可以关闭。数据备份保留天数最少7天，最多730天。

2.  RDS for MariaDB TX的日志备份是否可以关闭？

    答：可以关闭。备份设置内关闭日志备份开关即可。


## 相关API {#section_e3z_r2c_kgb .section}

|API|描述|
|---|--|
|[CreateBackup](../cn.zh-CN/API参考/备份恢复/CreateBackup.md#)|创建备份|
|[DescribeBackups](../cn.zh-CN/API参考/备份恢复/DescribeBackups.md#)|查看备份列表|
|[DescribeBackupPolicy](../cn.zh-CN/API参考/备份恢复/DescribeBackupPolicy.md#)|查看备份策略|
|[ModifyBackupPolicy](../cn.zh-CN/API参考/备份恢复/ModifyBackupPolicy.md#)|修改备份策略|


# RDS for MySQL查看增量数据的方法 {#concept_oqj_m35_jhb .concept}

RDS for MySQL查看增量数据可以通过SQL审计、Binlog以及DTS订阅三种方式。

## SQL审计 {#section_ynl_q35_jhb .section}

[SQL审计](../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/SQL审计.md#)会统计所有的DML和DDL操作的信息，这些信息是采集系统对网络上的包进行采集得到的。SQL审计并不会解析实际的参数的值， 并且在SQL查询量较大的时候会丢失少量的记录。因此通过这种方式来统计准确的增量数据是不精确的。

## Binlog {#section_chr_bj5_jhb .section}

Binlog会准确记录数据库所有的增删改操作。该日志可以准确的恢复用户的增量数据。RDS的Binlog会先存储在实例中，系统会定期上传到OSS上面备份，然后清理实例中的Binlog。

**操作步骤**

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/) 。
2.  在页面左上角，选择实例所在的地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155496735736543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏单击**备份恢复**。
5.  在日志备份找到所需的Binlog，单击右侧**下载**。
6.  单击**复制外网地址**。

    ![复制外网地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8282/155496735744249_zh-CN.png)

7.  在已安装MySQL的Linux系统内使用如下命令下载Binlog：

    ```
    wget -c '<Binlog文件外网下载地址>'
    ```

    ![下载Binlog](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8282/155496735744250_zh-CN.png)

8.  解密文件转换为可读形式，命令如下：

    ```
    mysqlbinlog --no-defaults -v --base64-output=decode-rows <Binlog文件名> > binlog.sql
    ```

9.  用`more binlog.sql`查看具体的日志信息，或者导出后检查问题SQL。

## DTS订阅 {#section_s4n_mp5_jhb .section}

DTS的数据订阅功能可以将RDS的增量数据实时推送给用户，用户可以定制增量数据，可以选择部分表的结构或者数据的增量，详情请参见[数据订阅](https://help.aliyun.com/document_detail/26596.html)。


# 【通知】TokuDB引擎转换为InnoDB引擎 {#concept_778692 .concept}

RDS for MySQL在2019年8月1日后将不再支持TokuDB引擎，本文介绍如何将TokuDB引擎转换为InnoDB引擎。

## 背景信息 {#section_d2x_c2r_d3b .section}

由于Percona已经不再对TokuDB提供支持，很多已知BUG无法修正，极端情况下会导致业务受损，因此RDS for MySQL在2019年8月1日后将不再支持TokuDB引擎。由于直接进行引擎转换会阻塞DML操作，影响并发，建议您尽快对业务评估后选择以下其中一种方案对引擎进行转换。

## TokuDB引擎下线时间 {#section_ls5_9os_t36 .section}

2019年8月1日

## 适用范围 {#section_p74_nhm_x74 .section}

存储引擎为TokuDB的实例。

**说明：** 您可以使用`show engines;`命令查看实例当前默认引擎，或者使用`show create table <表名>;`命令查看表的存储引擎。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149250121_zh-CN.png)

## 注意事项 {#section_j7h_49t_t7g .section}

-   转换存储引擎后空间占用会增大，在操作期间需要预留出的空间大约为：并行操作的TokuDB表容量\*2。操作期间请随时关注空间使用情况。
-   转换引擎后，CPU使用率会下降，但IOPS会上升。这是由于数据页没有压缩，所以读取相同的数据量，IOPS会有所上升。
-   全库迁移时，由于需要切换连接地址，请在业务低峰期进行操作。
-   全库迁移时，如果变更了数据库版本，建议提前进行兼容性测试。

## 方案建议 {#section_rvl_8vz_tea .section}

-   实例中的表较小（100M以下），且业务可接受短时阻塞时，可以使用方案一，锁表时间短，而且免去各种工具配置流程。
-   实例中的表较大（大于5G）时，建议使用方案二或方案三。
-   实例中的所有表都需要转换时，建议使用方案三或方案四。
-   切换引擎后请修改实例参数**default\_storage\_engine**为**InnoDB**。

## 方案一 {#section_tcd_dhr_d3b .section}

此方案为直接转换引擎，最简单直接，但过程中会全程阻塞DML操作，且大表转换时间比较久。

操作步骤

1.  [通过DMS登录RDS数据库](../cn.zh-CN/RDS for MySQL 用户指南/数据库连接/通过DMS登录RDS数据库.md#)。
2.  在上方选择**SQL操作** \> **SQL窗口**。
3.  执行如下命令：

    ``` {#codeblock_uwt_de9_3ki}
    Alter table test.testfs engine innodb
    ```

    ![直接修改](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149249981_zh-CN.png)


## 方案二 {#section_hwb_33r_d3b .section}

此方案为使用第三方工具进行转换。支持Online DDL的第三方工具很多，例如Percona开发的[pt-osc](https://www.percona.com/doc/percona-toolkit/LATEST/pt-online-schema-change.html)、Git-hub开发的[gh-ost](https://github.com/github/gh-ost)等，这里以gh-ost为例进行转换说明，详细说明请参见[gh-ost](https://github.com/github/gh-ost/blob/master/README.md)。

原理说明

gh-ost进行转换的基本原理是新建一个与原表结构相同的临时表，然后同步原表数据，全量完成后通过模拟Slave进程读取Binlog，实时同步数据到临时表。最后在业务低峰时间段重命名表进行切换。此方案主要压力来自全量数据初始化时的IO，但是可以通过修改参数限制IO。

-   优点：机动性强，可以自定义时间，同步过程可控。
-   缺点：每一个表都要用命令同步一次，如果表很多的话操作比较繁琐。

参数说明

|参数|说明|
|--|--|
|--initially-drop-old-table|检查并删除已经存在的旧表。|
|--initially-drop-ghost-table|检查并删除已经存在的ghost中间表。|
|--aliyun-rds|在阿里云RDS上执行。|
|--assume-rbr|设置gh-ost为rbr binlog模式。|
|--allow-on-master|在主库上执行gh-ost。|
|--assume-master-host|主库的地址。|
|--user|数据库账号名称。|
|--password|数据库密码。|
|--host|连接地址，与主库地址相同即可。|
|--database|数据库名称。|
|--table|表名。|
|--alter|操作语句。|
|--chunk-size|行拷贝的batch大小。|
|--postpone-cut-over-flag-file|切换文件。指定时间删除此文件立刻进行表切换。|
|--panic-flag-file|生成此文件，ghost进程立刻停止。|
|--serve-socket-file|用于接收交互命令。|
|--execute|直接执行。|

前提条件

-   已在本地主机或ECS安装gh-ost。
-   已在RDS实例的IP白名单中添加本地主机或ECS的IP。

操作步骤

1.  在本地主机或ECS上执行如下命令进行转换，等待转换完成。

    ``` {#codeblock_l46_is0_gsr}
    gh-ost --user="test01" --password="Test123456" --host="rm-bpxxxxx.mysql.rds.aliyuncs.com"  --database="test" --table="testfs"  --alter="engine=innodb" --initially-drop-old-table --initially-drop-ghost-table --aliyun-rds --assume-rbr --allow-on-master --assume-master-host="rm-bpxxxxx.mysql.rds.aliyuncs.com" --chunk-size=500 --postpone-cut-over-flag-file="/tmp/ghostpost.postpone" --panic-flag-file="/tmp/stop.flag" --serve-socket-file="/tmp/ghost.sock" --execute
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149249986_zh-CN.png)

2.  [通过DMS登录RDS数据库](../cn.zh-CN/RDS for MySQL 用户指南/数据库连接/通过DMS登录RDS数据库.md#)。
3.  在左侧查看表，会发现存在以\_gho、\_ghc结尾的临时表。

    ![生成临时表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149249980_zh-CN.png)

4.  执行`rm /tmp/ghostpost.postpone`命令开始切换表。结果如下。

    ![开始切换表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349988_zh-CN.png)

    **说明：** 忽略显示的error，实际已经切换完成。

5.  检查表并验证数据。

    **说明：** 验证数据没有问题后删除\_del表即可。

    ![切换成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349989_zh-CN.png)


## 方案三 {#section_rck_kdl_23b .section}

此方案使用阿里云的数据传输服务DTS（Data Transmission Service）实时同步原表数据到临时表，在业务低峰期锁原表并交换表名。该方案可以大量的表同时操作。

操作步骤

1.  [通过DMS登录RDS数据库](../cn.zh-CN/RDS for MySQL 用户指南/数据库连接/通过DMS登录RDS数据库.md#)。
2.  在上方选择**SQL操作** \> **SQL窗口**。
3.  使用如下命令创建临时表。

    ``` {#codeblock_6j6_seo_sdx}
    CREATE TABLE `testfs_tmp` (
      `id` int(11) NOT NULL AUTO_INCREMENT,
      `vc` varchar(8000) DEFAULT NULL,
      PRIMARY KEY (`id`)
    ) ENGINE=innodb  DEFAULT CHARSET=utf8
    					
    ```

4.  [购买数据同步作业](https://help.aliyun.com/document_detail/26604.html#h2-url-2)。

    **说明：** 数据同步作业需要收费，详细价格请参见[数据传输](https://cn.aliyun.com/price/product#/dts/detail)。

5.  在数据传输控制台左侧单击**数据同步**。
6.  找到购买的数据同步作业，在右侧单击**配置同步链路**。
7.  配置如下参数。

    |类别|参数|说明|
    |--|--|--|
    |源实例信息|实例类型|选择**RDS实例**。|
    |实例ID|选择需要切换引擎的RDS实例。|
    |连接方式|有**非加密传输**和**SSL安全连接**两种连接方式。选择**SSL安全连接**，需要提前开启[SSL加密](../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置SSL加密.md#)，会显著增加CPU消耗。|
    |目标实例信息|实例类型|选择**RDS实例**。|
    |实例ID|选择需要切换引擎的RDS实例。|
    |连接方式|有**非加密传输**和**SSL安全连接**两种连接方式。选择**SSL安全连接**，需要提前开启[SSL加密](../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置SSL加密.md#)，会显著增加CPU消耗。|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349990_zh-CN.png)

8.  单击**授权白名单并进入下一步**。
9.  等待创建同步账号，然后单击**下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349991_zh-CN.png)

10. 将左侧的表testfs移动到右侧，单击**编辑**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349992_zh-CN.png)

11. 修改**数据库名**为之前创建的testfs\_tmp，单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349993_zh-CN.png)

12. 单击**下一步**。
13. 仅勾选**全量数据初始化**，单击**预检查并启动**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349994_zh-CN.png)

14. 等待预检查完成，单击**关闭**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349995_zh-CN.png)

15. 等待数据同步延迟为0ms。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149449996_zh-CN.png)

16. 在DMS的SQL窗口执行切换表名命令：

    ``` {#codeblock_qu8_bq9_6mn}
    rename table `testfs` to `testfs_del`,`testfs_tmp` to `testfs`;
    ```

    **说明：** 

    -   切换后DTS同步会报错，是正常现象。
    -   验证数据后请尽快释放同步作业，避免继续收费。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149449997_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149449999_zh-CN.png)


## 方案四 {#section_3nx_6p6_elf .section}

此方案使用DTS同步整个数据库至新实例，适用于有实例升级需求，或者可以接受业务停机时间相对长一些的实例。

操作步骤

1.  源实例导出所有结构脚本，将脚本中关于引擎部分删除或修改。

    **说明：** 例如将`create table t1(id int,name varchar(10)) engine=tokudb;`修改为`create table t1(id int,name varchar(10)) engine=innodb;`。

2.  [新建RDS实例](../cn.zh-CN/RDS for MySQL 快速入门/创建RDS for MySQL实例.md#)，用修改过的脚本创建库、表。
3.  将源实例数据库使用DTS[同步至新实例](https://help.aliyun.com/document_detail/26633.html)上。

    **说明：** 在同步初始化时，仅勾选**全量数据初始化**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/630438/156879149349994_zh-CN.png)

4.  确认同步无延迟后，切换应用连接地址到新实例即可。


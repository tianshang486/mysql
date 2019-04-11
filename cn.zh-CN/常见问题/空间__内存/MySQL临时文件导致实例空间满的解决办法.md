# MySQL临时文件导致实例空间满的解决办法 {#concept_nqk_bh3_3gb .concept}

MySQL实例可能会由于查询语句的排序、分组、关联表产生的临时表文件，或者大事务未提交前产生的binlog cache文件，导致实例空间满，为避免数据丢失，RDS会对实例进行自动锁定，磁盘锁定之后，将无法进行写入操作。

## 背景信息 {#section_tsc_ny1_3gb .section}

当实例由于实例空间满自动锁定时，控制台可以在**基本信息** \> **运行状态**看到如下信息：

![实例空间满](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85053/155494970535652_zh-CN.png)

## 前提条件 {#section_xgd_ny1_3gb .section}

-   对于MySQL 5.6版本的实例，升级实例存储空间后即可解锁实例，关于如何升级实例配置，请参见[变更配置](../../../../../cn.zh-CN/RDS for MySQL 用户指南/实例管理/变更配置.md#)，若实例存储空间已到最大值，请提交工单联系客服临时解锁实例，再进行后续操作。
-   对于MySQL 5.5/5.7版本的实例，请提交工单联系客服临时解锁实例，再进行后续操作。

## 实施步骤 {#section_ayd_ny1_3gb .section}

**注意事项**

清理临时文件有延迟，请耐心等待实例已使用空间的下降。

**操作步骤**

1.  [通过 DMS登录数据库](../../../../../cn.zh-CN/RDS for MySQL 用户指南/附录/通过DMS登录RDS数据库.md#)。
2.  选择**SQL操作** \> **SQL窗口**，执行如下命令查看数据库的会话。

    ```
    show processlist
    ```

3.  单击显示结果中的State进行状态排序，在状态栏查看是否有大量 Copy to tmp table 、Sending data等信息，再根据Info列的语句确定是哪个SQL语句在建立临时表，记下该语句的Id。

    ![查看会话](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85444/155494970535875_zh-CN.png)

4.  可以通过命令行或者混合云数据库管理平台HDM（Hybrid Cloud Database Management）来终止会话。
    -   命令行：
        1.  在SQL窗口执行如下命令终止会话。

            ```
            kill <会话Id>
            ```

    -   混合云数据库管理平台：
        1.  选择**性能** \> **空间**，跳转到混合云数据库管理平台（Hybrid Cloud Database Management，HDM）。

            **说明：** 对于第一次进入的用户需要对HDM进行授权，若已授权，请跳到第4步。

        2.  在授权HDM访问您的云资源信息页面单击**确定**，并在弹出的云资源访问授权页面单击**同意授权**。

            ![授权HDM访问云资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8229/155494970535681_zh-CN.png)

            ![云资源访问授权](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8229/155494970535682_zh-CN.png)

        3.  在实例会话中找到之前记下的Id，单击该行任意位置选中该行，在右上角单击**kill选中会话**。

            ![kill会话](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85444/155494970535876_zh-CN.png)


## 后续维护 {#section_lbp_rh3_3gb .section}

-   针对查询产生的临时文件，应该优化SQL语句，避免频繁使用 order by、group by 操作，可以适当调大tmp\_table\_size和max\_heap\_table\_size，但是为了减少磁盘使用而调高 tmp\_table\_size 和 max\_heap\_table\_size 并不明智，因为内存资源远比磁盘资源宝贵；可以通过`explain`+SQL语句查看是否使用内部临时表，在 Extra 字段中有 Using temporary 字样的代表会使用内部临时表。示例如下：

    ```
    explain select * from alarm group by created_on order by default;
    ```

    ![explain示例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85444/155494970535925_zh-CN.png)

-   针对binlog cache，应该少执行大事务，尤其应该减少在多个连接同时执行大事务，如果大事务比较多，可以适当调大binlog\_cache\_size，但是同样不应该为了节省磁盘调整这个参数，使用短连接执行大事务可以有效降低临时空间开销。

## 更多信息 {#section_gxp_4y1_3gb .section}

-   [数据文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL数据文件导致实例空间满的解决办法.md#)
-   [Binlog文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL Binlog文件导致实例空间满的解决办法.md#)
-   [系统文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL系统文件导致实例空间满的解决办法.md#)


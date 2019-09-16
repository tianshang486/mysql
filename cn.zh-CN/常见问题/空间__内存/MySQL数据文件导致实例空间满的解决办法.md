# MySQL数据文件导致实例空间满的解决办法 {#concept_nlr_ddb_3gb .concept}

MySQL实例可能会由于数据文件长时间未整理导致实例空间满，为避免数据丢失，RDS会对实例进行自动锁定，磁盘锁定之后，将无法进行写入操作。

## 背景信息 {#section_tsc_ny1_3gb .section}

当实例由于实例空间满自动锁定时，控制台可以在**基本信息** \> **运行状态**看到如下信息：

![实例空间满自动锁](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85053/156859702235652_zh-CN.png)

## 前提条件 {#section_xgd_ny1_3gb .section}

-   对于MySQL 5.6/5.7/8.0版本的实例，请[升级内核小版本](../../../../cn.zh-CN/RDS for MySQL 用户指南/实例管理/升级内核小版本.md#)（需要版本号高于20190815，支持[实例锁优化](../../../../cn.zh-CN/AliSQL内核/AliSQL Release Notes.md#)），升级后即可执行删除数据的操作。
-   对于MySQL 5.5版本的实例，请提交工单联系客服临时解锁实例，再进行后续操作。

## 实施步骤 {#section_ayd_ny1_3gb .section}

**注意事项**

-   删除表前请确保有数据备份，以免造成损失。
-   推荐使用`drop`或`truncate`命令释放空间。
-   `optimize`操作将会锁表，建议在业务低峰期操作。
-   清理数据文件有延迟，请耐心等待实例已使用空间的下降。

**操作步骤**

1.  [通过 DMS登录数据库](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据库连接/通过DMS登录RDS数据库.md#)。
2.  选择**SQL操作** \> **SQL窗口**，执行如下命令查看数据库的文件大小，分析其中可以删除的历史数据文件或无用数据文件。

    ``` {#codeblock_mtc_cul_jk8}
    SELECT file_name, concat(TOTAL_EXTENTS,'M') as 'FIle_size' FROM INFORMATION_SCHEMA.FILES  order by TOTAL_EXTENTS DESC 
    ```

    ![查看文件大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85053/156859702235653_zh-CN.png)

3.  使用`drop`、`truncate`或者`delete`命令均可以清理数据。

    **说明：** 请确保已参照[前提条件](#)解锁实例。

    -   **drop**：使用`drop table <数据库名>.<表名>`删除不需要的表。
    -   **truncate**：使用`truncate table <数据库名>.<表名>`删除不需要的表。
    -   **delete**：

        **说明：** 未临时解锁的实例不支持**delete**操作，仅支持**drop**和**truncate**。

        1.  使用`delete from <数据库名>.<表名>`删除表中数据。
        2.  使用`optimize table <数据库名>.<表名>`回收空间。

## 后续维护 {#section_plp_4y1_3gb .section}

对于经常有`delete`操作的表，容易产生数据空洞，可以在业务低峰期使用`optimize table <数据库名>.<表名>`回收空间。

## 更多信息 {#section_gxp_4y1_3gb .section}

-   [Binlog文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL Binlog文件导致实例空间满的解决办法.md#)
-   [临时文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL临时文件导致实例空间满的解决办法.md#)
-   [系统文件导致实例空间满的解决办法](cn.zh-CN/常见问题/空间__内存/MySQL系统文件导致实例空间满的解决办法.md#)


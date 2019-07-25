# 全量备份数据上云SQL Server 2008 R2版 {#concept_swt_smw_ydb .concept}

SQL Server 2008 R2版本的实例支持便捷的数据上云操作，您只需要在自建数据库上利用微软官方备份功能备份好全量数据，再将备份文件上传至阿里云的[对象存储OSS](../../../../intl.zh-CN/产品简介/什么是对象存储 OSS.md#)中，就可以通过RDS控制台一键将数据全量迁移至RDS的指定数据库中。该功能利用了微软官方的备份恢复方案，兼容性100%，加上OSS强大的能力，使数据上云效率非常高。本文将介绍本地数据上云的操作步骤。

## 前提条件 {#section_z4d_hnw_ydb .section}

已在RDS中创建目标数据库，关于如何创建数据库，请参见[创建数据库和账号SQL Server 2008 R2版](../../../../intl.zh-CN/RDS for SQL Server 快速入门/初始化配置/创建数据库和账号/创建数据库和账号SQL Server 2008 R2版.md#)。

**说明：** RDS中的目标数据库名称可以与要迁移的本地数据库名称相同。

## 计费说明 {#section_q1w_3nw_ydb .section}

数据上云操作时，RDS不会额外收取费用，OSS会收取费用，详情如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15640177464362_zh-CN.png)

**图示说明：**

-   将本地数据备份文件上传至OSS时不产生任何额外费用。
-   当备份文件存储在OSS上时，需要额外支付OSS的存储费用，计费详情请参见[OSS定价](https://www.alibabacloud.com/zh/product/oss?spm=a3c0i.7990255.247275.8.7a40749en97oY9#pricing)。
-   将备份文件从OSS迁移至RDS时，若通过内网迁移，不产生任何额外费用；若通过外网迁移，OSS会收取外网流出流量的费用，计费详情请参见[OSS定价](https://www.alibabacloud.com/zh/product/oss?spm=a3c0i.7990255.247275.8.7a40749en97oY9#pricing)。

    **说明：** 只有当RDS实例和OSS的Bucket在同一地域时，二者才能内网互通。所以在上传备份文件时，请将文件上传至与目标RDS实例在同一地域的Bucket上面。


## 操作步骤 {#section_fm1_34w_ydb .section}

1.  准备本地数据库，详细步骤如下：
    1.  启动Microsoft SQL Server Management Studio （SSMS）客户端。
    2.  登录要上云的数据库。
    3.  执行如下命令，检查本地数据库的Recover Mode。

        ``` {#codeblock_tbc_yfr_rhh}
        use master;
        go
        select name, case recovery_model
        when 1 then 'FULL'
        when 2 then 'BULD_LOGGED'
        when 3 then 'SIMPLE' end model from sys.databases
        where name not in ('master','tempdb','model','msdb');
        go
        ```

        确认本地数据库的model值：

        -   如果model值不为FULL，请执行步骤d。

        -   如果model值为FULL，请执行步骤e。

    4.  执行如下命令，将源数据库的Recover Mode设置为FULL。

        ``` {#codeblock_jxv_o2k_04j}
        ALTER DATABASE [dbname] SET RECOVERY FULL;
        go
        ALTER DATABASE [dbname] SET AUTO_CLOSE OFF;
        go
        ```

        **说明：** 将Recover Mode改成FULL模式后，会使SQL Server日志增加，请确保有足够的硬盘空间。

    5.  执行如下命令，备份源数据库，本例以备份文件名为filename.bak为例。

        ``` {#codeblock_yqz_ec7_8zb}
        use master;
        go
        BACKUP DATABASE [testdbdb] to disk ='d:\backup\filename.bak' WITH COMPRESSION,INIT;
        go
        ```

    6.  执行如下命令，校验备份文件的完整性。

        ``` {#codeblock_504_4b4_4s5}
        USE master
         GO
         RESTORE FILELISTONLY 
           FROM DISK = N'D:\Backup\filename.bak';
        ```

        返回结果说明：

        -   如果有结果集返回，则备份文件有效。
        -   如果报错，则备份文件有误，请执行步骤e，重新备份。
    7.  执行如下命令，还原源数据库的Recover Mode。

        ``` {#codeblock_o0w_dyf_37l}
        ALTER DATABASE [dbname] SET RECOVERY SIMPLE;
        go
        ```

        **说明：** 如果您未执行步骤d，即数据库的Recover Mode本来就是FULL，没有做过变更，则无需执行该步骤。

2.  将本地备份文件上传至OSS并获取文件的URL，详细步骤如下：
    1.  将备份文件上传到OSS中，详细步骤如下：
        -   关于上传小于5GB的单个文件的操作步骤，请参见[上传文件](https://www.alibabacloud.com/help/doc-detail/31886.html)。
        -   关于上传多个文件或大于5GB的单个文件的操作步骤，请参见[断点续传](https://www.alibabacloud.com/help/doc-detail/31850.html)。若需要使用图形化的操作界面，请参见[ossbrowser](https://www.alibabacloud.com/help/doc-detail/61872.html)。
    2.  在 [OSS 管理控制台](https://oss.console.aliyun.com/)左侧的菜单栏中，选择备份文件所在的Bucket。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15640177464363_zh-CN.png)

    3.  选择**文件管理**。
    4.  单击目标备份文件的文件名。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15640177464364_zh-CN.png)

    5.  在**链接有效时间（秒）**栏中修改链接的有效时间，建议改成28800秒，即8小时。

        **说明：** 将备份文件从OSS迁移至RDS时，需要使用备份文件的URL，若该URL超过了链接的有效时间，则数据迁移会失败，所以建议您将该参数设置为最大值28800秒。

    6.  单击**复制文件URL**，系统默认的是文件的外网连接地址。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15640177474365_zh-CN.png)

    7.  若要通过内网迁移数据，将备份文件URL中的Endpoint改成内网Endpoint。不同的网络类型、不同地域所对应的内网Endpoint不同，详情请参见[访问域名和数据中心](https://www.alibabacloud.com/help/doc-detail/31837.html)。

        例如，若备份文件的URL是：

        ``` {#codeblock_i1q_voy_o7j}
        http://rdstest-yanhua.oss-cn-shanghai.aliyuncs.com/testmigraterds_20170906143807_FULL.bak?Expires=1514189963&OSSAccessKeyId=TMP.AQGVf994YTPfArSpw78uix2rdGBi-dPe_FzQSLwOLP7MVlR-XXXX
        ```

        您需要将URL中的外网Endpoint

        ``` {#codeblock_dw1_rpo_cwz}
        oss-cn-shanghai.aliyuncs.com
        ```

        改成内网Endpoint

        ``` {#codeblock_m52_35t_nj8}
        oss-cn-shanghai-internal.aliyuncs.com
        ```

        。

3.  将备份文件从OSS迁移至RDS，详细步骤如下：
    1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
    2.  选择目标实例所在地域。
    3.  单击目标实例的ID，进入基本信息页面。
    4.  在左侧菜单栏中选择**数据库管理**，进入数据库管理页面。
    5.  找到目标数据库，在其对应的**操作**栏中，单击**从OSS上的备份文件迁入**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15640177474366_zh-CN.png)

    6.  在数据导入向导对话框中，阅读提示内容，单击**下一步**，进入上传备份文件到OSS页面。
    7.  阅读提示内容，单击**下一步**，进入数据导入页面。
    8.  在**备份文件OSS URL**栏中填写备份文件在OSS的URL。

        **说明：** 目前，RDS for SQL Server 2008 R2仅支持一种上云方案，即全量备份文件一次性迁入

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7997/15640177474367_zh-CN.png)

    9.  单击**确定**。
    10. 在左侧菜单栏中选择**数据上云**，进入从OSS迁移备份文件至RDS中的任务列表页面。
    11. 找到目标迁移任务，若任务状态为成功，则表示数据已成功迁移至RDS的数据库中。若迁移任务长时间没有变成成功状态，单击目标迁移任务后面的**查看文件详情**，即可查看任务没有成功的原因。解决完问题后，请重新执行上述所需要的步骤。


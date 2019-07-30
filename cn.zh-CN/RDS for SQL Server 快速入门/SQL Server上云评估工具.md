# SQL Server上云评估工具 {#concept_x1k_nsp_y2b .concept}

本文介绍SQL Server的上云评估工具。关于MySQL、PostgreSQL、MariaDB的上云，请使用[DTS](https://help.aliyun.com/product/26590.html)工具。关于Oracle的上云（到RDS for PPAS），请使用[ADAM](https://help.aliyun.com/product/53556.html)工具。

SQL Server上云评估工具Database Assessment Tool是一款用于对自建SQL Server数据库进行评估并给出上云评估报告的自动化工具，帮助您做好上云前的分析和准备工作。

## 支持的自建数据库 {#section_fcb_lnw_y2b .section}

-   本地自建SQL Server数据库
-   云虚拟机上的自建SQL Server数据库

## 工具下载 {#section_r5m_kq5_y2b .section}

[点此下载](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/127793/cn_zh/1564472514793/AliyunDATForSQLServer.zip)上云评估工具。

## 开始评估 {#section_lmn_pq5_y2b .section}

1.  打开SQL Server上云评估工具。
2.  在左上角单击**新建连接**。
3.  在弹出的对话框中，填写要迁移的SQL Server数据库服务器的地址以及验证方式。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18826/156447307310703_zh-CN.png)

4.  单击**保存**。

    左侧出现已连接的数据库服务器。

5.  单击**+**号展开数据库列表，选择要进行上云评估的数据库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18826/156447307310684_zh-CN.png)

6.  单击**上云评估**。
7.  评估完成后，单击右下角的**生成报告**，将报告保存到您指定的路径。

## 查看评估报告 {#section_drr_5fv_y2b .section}

评估报告包含以下内容：

-   **上云建议** 

    提供建议您使用的RDS实例的系列、规格和版本。

-   **检测项目——与RDS for SQL Server兼容** 

    RDS for SQL Server支持这些功能，但是您需要选择特定的RDS for SQL Server版本。

-   **检测项目——通过调整可与RDS for SQL Server兼容** 

    通过极少的调整，即可在云数据库RDS for SQL Server上实现的功能。

-   **检测项目——与RDS for SQL Server不兼容** 

    RDS不支持这些功能，您可以使用报告中提供的替代性措施。


[点此查看评估报告示例](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/89311/cn_zh/1536669647578/sample_report.html)


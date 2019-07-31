# 基于MaxCompute的大数据计算 {#concept_hyv_pnx_wdb .concept}

大数据计算服务\(MaxCompute，原名ODPS\)是一种快速、完全托管的TB/PB级数据仓库解决方案。MaxCompute向用户提供了完善的数据导入方案以及多种经典的分布式计算模型，能够更快速的解决用户海量数据计算问题，有效降低企业成本，并保障数据安全。通过数据集成服务，可将 RDS 数据导入 MaxCompute，实现大规模的数据计算。下面以 MaxCompute 和 RDS 搭配为例介绍大数据计算方案。

## 前提条件 {#section_msx_c4x_wdb .section}

-   已开通 MaxCompute 服务，并完成项目设置
-   已开通数据集成服务

## 操作步骤 {#section_xdy_d4x_wdb .section}

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com/)，选择目标实例。
2.  在 RDS 实例上增加数据集成的白名单。

    ``` {#codeblock_u6r_38a_te5}
    CDP 白名单：    
     10.152.69.0/25  
     10.153.136.0/25  
     10.143.32.77  
     10.143.32.78
    ```

3.  登录 [MaxCompute 管理控制台](https://home-intl.console.aliyun.com/)，创建 MaxCompute 数据表。

    更多 MaxCompute 操作请参见 [什么是MaxCompute](https://www.alibabacloud.com/help/zh/doc-detail/27800.html)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8003/15645401953213_zh-CN.png)

4.  登录 [数据集成管理控制台](https://cdp.console.aliyun.com/)，设置 RDS 源库和 MaxCompute 目标库信息。

    更多数据集成操作请参见 [DataWorks](https://www.alibabacloud.com/help/zh/doc-detail/73015.html)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8003/15645401953214_zh-CN.png)

5.  设置数据集成同步字段。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8003/15645401953215_zh-CN.png)

6.  设置数据集成速度与出错控制。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8003/15645401953216_zh-CN.png)

7.  完成设置后，将数据导入 MaxCompute。
8.  登录 [MaxCompute 管理控制台](https://home-intl.console.aliyun.com/)，执行查询操作，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8003/15645401963217_zh-CN.png)



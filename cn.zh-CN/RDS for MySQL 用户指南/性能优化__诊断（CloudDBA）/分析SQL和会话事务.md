# 分析SQL和会话事务 {#concept_m5d_yf4_wdb .concept}

MySQL CloudDBA可以通过审计日志分析SQL，并通过分析结果给出相应的优化建议。另外，MySQL CloudDBA可以通过审计日志分析会话事务，并列出正常会话事务和长会话事务的详情。本文将介绍如何分析SQL和会话事务，并查看诊断详情。

## 前提条件 {#section_ayv_dg4_wdb .section}

-   实例需要开通SQL洞察功能，关于开通步骤，请参见[SQL洞察](cn.zh-CN/RDS for MySQL 用户指南/SQL洞察.md#)。SQL洞察默认关闭，该功能开启后，将会产生额外的费用，详细收费标准请参见[云数据库RDS详细价格信息](https://www.aliyun.com/price/product?spm=5176.doc26197.2.2.xiv3Vl#/rds/detail)。

-   实例为如下版本：
    -   MySQL 5.7 高可用版
    -   MySQL 5.6版
    -   MySQL 5.5 高可用版

## 操作步骤 {#section_as4_fg4_wdb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择目标实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156324685536543_zh-CN.png)

3.  单击目标实例ID，进入基本信息页面。
4.  在左侧导航栏中，选择**CloudDBA** \> **SQL统计** ，进入SQL统计页面。
5.  选择CPU或IOPS，并选择要进行数据分析的时间范围，单击**确定**，状态图中即会显示当前实例的CPU或IOPS在指定时间段内的使用率状况，如下图所示。

    **说明：** 您最多只能选择1天的时间段。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468553078_zh-CN.png)

6.  选择获取审计日志的起始时间（需在步骤5中所选择的时间范围内）以及时长，然后单击获取审计日志，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468553079_zh-CN.png)

7.  分析任务创建成功后，页面列表中会显示分析进度，如下图所示

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468553080_zh-CN.png)

8.  分析任务完成后，您可以查看分析详情。
    -   查看SQL分析详情

        1.  找到目标分析记录，并单击**SQL分析**栏下的**查看**，进入SQL分析详情页面，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468563081_zh-CN.png)

            SQL分析详情页面会显示获取审计日志时间段内的CPU/IOPS使用率状况，以及SQL详情，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468563082_zh-CN.png)

        2.  选择分析维度，状态表及SQL详情列表中即会显示相应信息，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468563083_zh-CN.png)

        3.  若需要查看某条SQL语句的优化建议，单击目标SQL，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468563084_zh-CN.png)

        4.  单击**SQL优化建议**，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468563085_zh-CN.png)

            系统会返回SQL语句的问题及优化建议（若有），如下图所示。

            **说明：** 为不断提高CloudDBA智能分析与优化的质量，请对系统提供的优化建议提出您宝贵的意见和建议，单击**确定**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468563086_zh-CN.png)

    -   查看事务分析详情

        1.  找到目标分析记录，并单击**事务分析**栏下的**查看**，进入事务分析详情页面，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468573087_zh-CN.png)

        2.  单击饼状图中的事务类型，下方列表即会显示该类事务的详情，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468573088_zh-CN.png)

        3.  在会话事务列表中选中要查看的事务，即可在会话事务详情栏中查看事务详情，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468573089_zh-CN.png)

        4.  若选中的事务中有多条语句，在会话事务详情栏中单击**上一个事务**或**下一个事务**即可查看每个语句的会话事务详情，如下图所示。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7911/15632468573090_zh-CN.png)



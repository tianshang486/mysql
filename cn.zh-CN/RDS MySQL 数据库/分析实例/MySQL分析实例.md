# MySQL分析实例

RDS MySQL提供分析实例功能，可以将RDS MySQL主实例中的数据自动同步到MySQL分析实例中，解决RDS MySQL复杂分析查询卡顿问题，实现毫秒级针对万亿级数据进行即时的多维分析透视和业务探索。

## 使用场景

随着企业业务发展，精细化实时运营诉求越来越强烈，RDS MySQL用户经常会遇到以下问题：

-   进行复杂分析查询时，经常会出现查询卡顿。只读实例只能分担读压力，无法从根本上解决复杂分析慢的问题。
-   构建实时数仓成本太高，公司留给数据分析预算有限，只能默默忍受越来越长的卡顿时间，殊不知在无限的忍受中公司错过了很多机会。

此时，您可以在RDS MySQL控制台上创建一个MySQL分析实例，MySQL分析实例的复杂分析性能约为MySQL的100倍，系统自动通过DTS将RDS MySQL主实例中的全量数据和增量数据实时同步到MySQL分析实例中。您无需关注数据如何入库，无需担心分析卡顿，系统自动帮您搭建实时数据仓库，真正实现在线业务库和分析库全面隔离和完全解耦。

## MySQL分析实例和只读实例区别

使用场景上，只读实例主要面向在线读写分离应用，MySQL分析实例专注报表查询，交互式分析和跑批等应用。具体如下图介绍。产品实现上，只读实例是只能接收只读请求的RDS MySQL，而分析实例是一个AnalyticDB for MySQL集群（分析实例技术解读请参见[MySQL分析实例简介]()）。

![分析实例与只读实例区别-最新 ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9413729951/p88536.jpg)

**说明：** 查询不会自行路由到分析实例，需要用户自己切换。

## 前提条件

-   RDS MySQL实例版本需满足以下条件才可以创建MySQL分析实例：
    -   MySQL 8.0三节点企业版
    -   MySQL 8.0高可用版（本地SSD盘或SSD云盘）
    -   MySQL 5.7三节点企业版
    -   MySQL 5.7高可用版（本地SSD盘或SSD云盘）
    -   MySQL 5.6
-   RDS MySQL中存在表数据。

## 计费

MySQL分析实例的费用由两部分组成：

-   AnalyticDB for MySQL集群的费用，如何收费请参见[规格详情]()。
-   DTS费用，请参见[产品定价](/cn.zh-CN/产品定价/产品定价.md)。

    **说明：** DTS同步链路规格默认为medium模式，若出现同步延时可能需要[升级实例配置](/cn.zh-CN/实例管理/升级实例配置.md)。


## 优惠活动

自即日起，凡购买MySQL分析实例的用户可享受[9.9元3个月](https://ads.console.aliyun.com/adb/cn-beijing/instances/rds)的优惠活动，活动截止日期为2020-12-31。

## 创建分析实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)，单击**添加分析实例**，按照系统提示完成授权操作。

    ![添加分析实例](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2513729951/p98368.jpg)

2.  授权成功后，系统跳转至MySQL分析实例的购买页面，按照购买流程创建MySQL分析实例。
3.  MySQL实例创建成功后，系统进行数据同步。

详细步骤请参见[创建和查看MySQL分析实例]()。

## 常见问题

-   [MySQL分析实例使用限制]()
-   [常见数据同步问题]()


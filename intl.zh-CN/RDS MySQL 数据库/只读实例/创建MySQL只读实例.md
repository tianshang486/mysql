# 创建MySQL只读实例

您可以通过创建只读实例满足大量的数据库读取需求，增加应用的吞吐量。创建只读实例相当于复制了一个主实例，数据与主实例一致，主实例的数据更新也会自动同步到所有只读实例。

其他引擎创建只读实例请参见：

-   [创建SQL Server只读实例](/intl.zh-CN/RDS SQL Server 数据库/快速入门/只读实例/创建SQL Server只读实例.md)
-   [创建PostgreSQL只读实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/只读实例/创建PostgreSQL只读实例.md)
-   [创建PPAS只读实例](/intl.zh-CN/RDS PPAS 数据库/快速入门/只读实例/创建PPAS只读实例.md)

关于只读实例的更多介绍，请参见[只读实例简介](/intl.zh-CN/RDS MySQL 数据库/只读实例/MySQL只读实例简介.md)。

## 前提条件

实例版本如下：

-   MySQL 8.0高可用版或三节点企业版
-   MySQL 5.7高可用版或三节点企业版
-   MySQL 5.6

**说明：** 如果您的MySQL 5.7三节点企业版不支持只读实例，请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)处理。

## 注意事项

-   只能在主实例内创建只读实例，不能将已有实例切换为只读实例。
-   由于创建只读实例时是从备实例复制数据，因此不会影响主实例。
-   只读实例的参数不继承主实例上的参数设置，会生成默认的参数值，可以在只读实例的控制台上进行修改。
-   只读实例数量：

    |数据库类型|内存|数量|
    |-----|--|--|
    |MySQL|≥64GB|最多创建10个只读实例|
    |＜64GB|最多创建5个只读实例|

-   计费方式：按量付费，即每小时扣费一次，费用取决于扣费时的只读实例规格。具体费用请参见[详细价格信息](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.10521d15K8Buqg#pricing)中的只读实例部分。

## 创建只读实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在页面右侧单击**添加只读实例**。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2413729951/p9361.png)

5.  设置只读实例的参数。

    |参数|说明|
    |--|--|
    |**可用区**|可用区是地域中的一个独立物理区域，不同可用区之间没有实质性区别。相比单可用区，多可用区能提供可用区级别的容灾。|
    |**实例规格**|    -   **入门级**：通用型的实例规格，独享被分配的内存和I/O资源，与同一服务器上的其他通用型实例共享CPU和存储资源。
    -   **企业级**：独享或独占型的实例规格。独享型指独享被分配的CPU、内存、存储和I/O资源。独占型是独享型的顶配，独占整台服务器的CPU、内存、存储和I/O资源。
**说明：** 每种规格都有对应的CPU核数、内存、最大连接数和最大IOPS。详情请参见[主实例规格列表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 |
    |**存储空间**|存储空间包括数据空间、系统文件空间、Binlog文件空间和事务文件空间。调整存储空间时最小单位为5GB。 **说明：** 部分本地SSD盘的存储空间大小与实例规格绑定，ESSD/SSD云盘不受此限制。详情请参见[主实例规格列表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 |

6.  单击**下一步：实例配置**，设置如下参数。

    |参数|说明|
    |--|--|
    |**网络类型**|    -   **经典网络**：传统的网络类型。
    -   **专有网络**：也称为VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。选择专有网络时您需要选择对应的**VPC**和**主节点交换机**。
**说明：** 请确保RDS实例与需要连接的ECS实例网络类型一致（如果选择专有网络，还需要保证VPC一致），否则它们无法通过内网互通。 |

7.  单击**下一步：确认订单**。

8.  勾选服务协议，单击**去支付**，根据提示完成支付。

    **说明：** 如果您的实例支持开通[数据库独享代理](/intl.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)（付费服务），您可以额外勾选**代理服务**，可以在创建只读实例的同时开通独享代理。


## 查看只读实例

在实例列表中查看只读实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  在实例列表中找到只读实例，单击该只读实例的ID。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3413729951/p2617.png)


在主实例的基本信息页面查看只读实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  在实例列表中找到主实例，单击该主实例的ID。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3413729951/p32584.png)

4.  在主实例的**基本信息**页面，将鼠标悬停于只读实例的数量上，单击只读实例的ID。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3413729951/p9379.png)


## 查看只读实例的延迟时间

只读实例同步主实例的数据时，可能会有一定的延迟。您可以在只读实例的基本信息页面查看延迟时间。

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3413729951/p2636.png)

## 常见问题

-   只读实例不能包年包月吗？

    为保证按需变配，只读实例当前仅支持按量付费，不支持包年包月。

-   创建只读实例为什么无法选择某个可用区？

    没有某个可用区表示该可用区暂无资源，您可以选择其他可用区，不影响您使用只读实例。

-   创建只读实例时可以选择和主实例不同的专有网络VPC吗？

    不可以。只读实例必须和主实例处于相同VPC，否则创建时会报错。


## 相关API

|API|描述|
|---|--|
|[t8102.md\#](/intl.zh-CN/API 参考/只读实例/创建只读实例.md)|创建RDS只读实例|


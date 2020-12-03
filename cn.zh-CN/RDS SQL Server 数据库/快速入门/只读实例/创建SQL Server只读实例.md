# 创建SQL Server只读实例

您可以通过创建只读实例满足大量的数据库读取需求，增加应用的吞吐量。创建只读实例相当于复制了一个主实例，数据与主实例一致，主实例的数据更新也会自动同步到所有只读实例。

关于只读实例的更多介绍，请参见[SQL Server只读实例简介](/cn.zh-CN/RDS SQL Server 数据库/快速入门/只读实例/SQL Server只读实例简介.md)。

## 前提条件

主实例版本为SQL Server 2017集群版。

## 注意事项

-   只能在主实例内创建只读实例，不能将已有实例切换为只读实例。
-   由于创建只读实例时是从备实例复制数据，因此不会影响主实例。
-   最多创建7个只读实例。

## 创建只读实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。
4.  在页面右侧单击**添加只读实例**。

    ![添加只读实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4851760061/p168763.png)

5.  设置以下参数，单击**下一步：实例配置**。

    |类别|说明|
    |--|--|
    |**计费方式**|    -   **包年包月**：属于预付费，即在新建实例时需要支付费用。适合长期需求，价格比按量付费更实惠，且购买时长越长，折扣越多。
    -   **按量付费**：属于后付费，即按小时扣费。适合短期需求，用完可立即释放实例，节省费用。 |
    |**存储类型**|    -   **SSD云盘**：基于分布式存储架构的弹性块存储设备。将数据存储于SSD云盘，即实现了计算与存储分离。
    -   **ESSD云盘**：增强型（Enhanced）SSD云盘，是阿里云全新推出的超高性能云盘产品。ESSD云盘基于新一代分布式块存储架构，结合25GE网络和RDMA技术，为您提供单盘高达100万的随机读写能力和更低的单路时延。ESSD云盘分为如下三类：
        -   ESSD云盘：PL1性能级别的ESSD云盘。
        -   ESSD PL2云盘：相比PL1，PL2性能级别的ESSD云盘大约可提升2倍IOPS和吞吐量。
        -   ESSD PL3云盘：相比PL1，PL3性能级别的ESSD云盘最高可提升20倍IOPS、11倍吞吐量，适合对极限并发I/O性能要求极高、读写时延极稳定的业务场景。
更多信息，请参见[存储类型](/cn.zh-CN/云数据库 RDS 简介/存储类型.md)。 |
    |**可用区**|可用区是地域中的一个独立物理区域。|
    |**实例规格**|    -   **入门级**：共享/通用型的实例规格，独享被分配的内存和I/O资源，与同一服务器上的其他通用型实例共享CPU和存储资源。
    -   **企业级**：独享或独占型的实例规格。独享型指独享被分配的CPU、内存、存储和I/O资源。独占型是独享型的顶配，独占整台服务器的CPU、内存、存储和I/O资源。
**说明：** 每种规格都有对应的CPU核数、内存、最大连接数和最大IOPS。详情请参见[主实例规格列表](/cn.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 |
    |**存储空间**|存储空间包括数据空间、系统文件空间、Binlog文件空间和事务文件空间。调整存储空间时最小单位为5GB。 **说明：** 本地SSD盘的独享套餐等规格由于资源独享的原因，存储空间大小和实例规格绑定。详情请参见[主实例规格列表](/cn.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 |

    **说明：** 为保证数据同步有足够的I/O性能支撑，建议只读实例的规格（内存）不小于主实例。

6.  设置以下参数，**下一步：确认订单**。

    |类别|说明|
    |--|--|
    |**网络类型**|    -   **经典网络**：传统的网络类型。
    -   **专有网络**：也称为VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。选择专有网络时您需要选择对应的**VPC**和**主节点交换机**。
**说明：** 请确保RDS实例与需要连接的ECS实例网络类型一致（如果选择专有网络，还需要保证VPC一致），否则它们无法通过内网互通。 |
    |**资源组**|实例所属的资源组。|

7.  单击**下一步：确认订单**，确认**参数配置**，选择**购买量**，勾选服务协议，单击**去支付**完成支付。

几分钟后，该只读实例即创建成功。

## 查看只读实例

-   在实例列表中查看只读实例
    1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
    2.  选择只读实例所在地域。

        ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

    3.  在实例列表中找到只读实例，单击该只读实例的ID。

        ![只读实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8603729951/p39852.png)

-   在主实例的基本信息页面查看只读实例
    1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
    2.  选择主实例所在地域。

        ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

    3.  在实例列表中找到主实例，单击该主实例的ID。

        ![主实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8603729951/p39853.png)

    4.  在主实例的**基本信息**页面，把鼠标悬停于只读实例的数量上，单击只读实例的ID。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3413729951/p9379.png)


## 在集群管理页面查看只读实例

前提条件

已在集群管理页面[开通读写分离]()。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9603729951/p32588.png)

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择主实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  在实例列表中找到主实例，单击该主实例的ID。
4.  在左侧导航栏中，单击**集群管理**。
5.  找到只读实例，单击该只读实例的ID。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8603729951/p32587.png)


## 查看只读实例的延迟时间

只读实例同步主实例的数据时，可能会有一定的延迟。您可以在只读实例的基本信息页面查看延迟时间。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3413729951/p2636.png)

## 相关API

|API|描述|
|---|--|
|[创建只读实例](/cn.zh-CN/API 参考/只读实例/创建只读实例.md)|创建RDS只读实例|


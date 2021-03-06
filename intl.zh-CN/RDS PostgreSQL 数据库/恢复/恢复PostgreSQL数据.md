# 恢复PostgreSQL数据

如果拥有RDS PostgreSQL实例的数据备份，可以按本文介绍的方法恢复数据。

原实例需要满足如下条件：

-   运行中且没有被锁定。
-   当前没有迁移任务。
-   如果要按时间点进行恢复，需要确保日志备份已开启。

    **说明：** 基础版实例不支持日志备份，因此不支持按时间点恢复。

-   若要按备份集恢复，则原实例必须至少有一个备份集。

RDS PostgreSQL支持按备份集或时间点恢复数据。恢复数据的过程如下：

1.  恢复到一个新实例（此功能原名为克隆实例）。
2.  登录到新实例，验证实例的数据是否正确。
3.  将数据迁移到原实例。

## 注意事项

-   新实例的白名单设置、备份设置、参数设置和当前实例保持一致。
-   新实例的数据信息和账号信息与备份集或时间点当时的信息一致。

## 计费方式

与新购实例相同，详情请参见[详细价格信息](https://www.alibabacloud.com/product/apsaradb-for-rds#pricing)。

## 恢复数据到新实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏选择**备份恢复**。

5.  在页面右上角，单击**数据库恢复（原克隆实例）**。

6.  设置如下参数。

    |类别|说明|
    |--|--|
    |**计费方式**|    -   **包年包月**：属于预付费，即在新建实例时需要支付费用。适合长期需求，价格比按量付费更实惠，且购买时长越长，折扣越多。
    -   **按量付费**：属于后付费，即按小时扣费。适合短期需求，用完可立即释放实例，节省费用。 |
    |**还原方式**|    -   **按时间点**：可以设置为日志备份保留时间内的任意时间点。如要查看或修改日志备份保留时间，请参见[备份PostgreSQL数据](/intl.zh-CN/RDS PostgreSQL 数据库/备份/备份PostgreSQL数据.md)。
    -   **按备份集**
**说明：** 只有开启了日志备份，才会显示**按时间点**。 |
    |**系列**|    -   **基础版**：单节点，计算与存储分离，性价比高。
    -   **高可用版**：一个主节点和一个备节点，经典高可用架构。
**说明：** 不同地域和数据库版本支持的系列不同，请以实际界面为准。关于各个系列的详细介绍，请参见[产品系列概述](/intl.zh-CN/云数据库 RDS 简介/产品系列/产品系列概述.md)。 |
    |**可用区**|可用区是地域中的一个独立物理区域，**主节点可用区**指主实例所在可用区，**备节点可用区**指备实例所在可用区。

您可以设置实例为**单可用区部署**或**多可用区部署**：

    -   **单可用区部署**：**主节点可用区**和**备节点可用区**都处于相同可用区。
    -   **多可用区部署**（推荐）：**主节点可用区**和**备节点可用区**处于不同可用区，能提供可用区级别的容灾。您只需要选择**主节点可用区**，系统会自动选择**备节点可用区**。
**说明：**

    -   实例创建后，您可以在实例的**服务可用性**页面查看主备节点信息。
    -   基础版实例只有一个节点，只能部署在一个可用区内。
![可用区](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1677559951/p87361.png) |
    |**实例规格**|    -   **通用规格（入门级）**：通用型的实例规格，独享被分配的内存和I/O资源，与同一服务器上的其他通用型实例共享CPU和存储资源。
    -   **独享规格（企业级）**：独享或独占型的实例规格。独享型指独享被分配的CPU、内存、存储和I/O资源。独占型是独享型的顶配，独占整台服务器的CPU、内存、存储和I/O资源。
    -   **专属规格**：完全独享虚拟主机或物理主机资源，开放主机权限，可直接在主机上按需分配多个数据库实例。更多信息，请参见[添加主机]()。
**说明：** 每种规格都有对应的CPU核数、内存、最大连接数和最大IOPS。详情请参见[主实例规格列表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 |
    |**存储空间**|存储空间包括数据空间、系统文件空间、Binlog文件空间和事务文件空间。调整存储空间时最小单位为5GB。 **说明：** 本地SSD盘的独享套餐等规格由于资源独享的原因，存储空间大小和实例规格绑定。详情请参见[主实例规格列表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。 |

7.  单击**下一步：网络和资源组**。

8.  设置如下参数。

    |类别|说明|
    |--|--|
    |**网络类型**|    -   **经典网络**：传统的网络类型。
    -   **专有网络**（推荐）：也称为VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。选择专有网络时您需要选择对应的**VPC**和**主节点交换机**。
**说明：** 请确保RDS实例与需要连接的ECS实例网络类型一致（如果选择专有网络，还需要保证VPC一致），否则它们无法通过内网互通。 |
    |**资源组**|实例所属的资源组。|

9.  单击**下一步：确认订单**。

10. 确认**参数配置**，选择**购买量**和**购买时长**（仅包年包月实例），勾选服务协议，单击**去支付**完成支付。


## 登录到新实例并验证数据

关于登录实例的操作，请参见[连接实例](/intl.zh-CN/RDS PostgreSQL 数据库/快速入门/连接PostgreSQL实例.md)。

## 迁移数据到原实例

确认新实例的数据之后，您可以将需要的数据从新实例迁移回原实例。详情请参见[RDS实例间的数据迁移](https://www.alibabacloud.com/help/zh/doc-detail/26626.htm)。

**说明：** 数据迁移是指将一个实例（称为源实例）的数据复制到另一个实例（称为目标实例），迁移操作不会对源实例造成影响。


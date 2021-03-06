# MySQL单库单表恢复

RDS MySQL支持单库和单表的数据恢复，可以通过备份指定恢复误删的数据库或表，快速恢复MySQL的数据。

-   实例为如下版本：
    -   MySQL 8.0 高可用版（本地SSD盘）
    -   MySQL 5.7 高可用版（本地SSD盘）
    -   MySQL 5.6 高可用版
-   实例存储引擎不为X-Engine。
-   实例内的表低于50000张才可以使用单库单表恢复功能，超过50000张表时无法使用。
-   控制台**备份恢复** \> **备份设置**里开启单库单表恢复功能。

    ![控制台开通库表恢复](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2646037061/p44546.png)

    **说明：**

    -   开通单库单表恢复功能后，备份格式会修改，用于支持库表恢复，且开通之后无法关闭该功能。
    -   新实例默认开启该功能，无法关闭。
-   如果是恢复到原实例，原实例需要满足如下条件：
    -   运行中且没有被锁定。
    -   当前没有迁移任务。
    -   如果要按时间点进行恢复，需要确保日志备份已开启。
    -   若要按备份集恢复，则原实例必须至少有一个备份集。
-   如果是恢复到新实例，原实例需要满足如下条件：
    -   运行中且没有被锁定。
    -   如果要按时间点进行恢复，需要确保日志备份已开启。
    -   若要按备份集恢复，则原实例必须至少有一个备份集。

**说明：** 如果需要进行数据库级别的数据恢复，请参见[恢复MySQL数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)。

## 注意事项

-   恢复到原实例过程中会进行主备切换，RDS服务可能会出现闪断，请确保您的应用有自动重连机制；恢复到新实例不会进行主备切换。
-   单库单表恢复功能会将备份文件从tar压缩包变成xbstream文件包，备份文件占用的存储空间会略微增大，请您关注[备份使用量](/intl.zh-CN/RDS MySQL 数据库/备份/查看备份空间免费额度.md)。超出免费备份空间额度的部分将会产生额外费用，请合理设计备份周期，以满足业务需求的同时，兼顾备份空间的合理利用。
-   单库单表恢复只会恢复指定的表，请勾选所有涉及到的表。以下几种情况会导致恢复失败：

    -   从最近一份备份集生成时间点到指定恢复的时间点，这段时间内指定的表被删除，恢复会失败。
    -   出现未指定的表时会恢复失败。例如指定恢复表b，但是表b是表a在指点时间点之前重命名的，由于表a没有指定，恢复会失败。
    如果无法确定所有涉及的表，则需要进行实例级别的恢复，详情请参见[恢复MySQL数据](/intl.zh-CN/RDS MySQL 数据库/恢复/恢复MySQL数据.md)。

-   每次最多选择50个库或者表。

## 操作步骤

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中选择**备份恢复**。

5.  单击**数据库 库/表级别恢复**。

    **说明：** 如未看到**数据库 库/表级别恢复**按钮，请参见前提条件。

    ![库/表级别恢复](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2646037061/p37783.png)

6.  设置如下参数。

    ![库/表级别恢复参数设置1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4313729951/p37784.png)

    |参数名称|说明|
    |----|--|
    |**回档位置**|    -   **回档到原实例**：将库/表恢复到原实例中。
    -   **回档到新实例**：新购实例，并将库/表恢复到新实例中。 |
    |**还原方式**|    -   **按备份集**
    -   **按时间点**：可以设置为日志备份保留时间内的任意时间点。如要查看或修改日志备份保留时间，请参见[备份MySQL数据](/intl.zh-CN/RDS MySQL 数据库/备份/备份MySQL数据.md)。
**说明：** 只有开启了日志备份，才会显示**按时间点**。 |
    |**备份集**|选择备份集来进行库/表恢复。 **说明：** **还原方式**选择**按备份集**时可用。 |
    |**还原时间**|选择时间点来进行库/表恢复。 **说明：** **还原方式**选择**按时间点**时可用。 |
    |**还原模式**|    -   **逻辑还原**：速度较慢。
    -   **物理还原**：速度较快，但是实例会进行主备切换，所有只读实例会重启。如果实例处于运维状态、指定恢复的库表数据量较少或只读实例复制中断时，后端会自动选择**逻辑还原**。
**说明：** 实例有只读实例时此选项可见。 |
    |**需要恢复的库和表**|勾选需要恢复的库或表。|
    |**已选择的库和表**|    -   显示已勾选的库和表，并可预设恢复后的库/表名称。
    -   显示已勾选的库和表的总大小，以及该实例剩余存储空间，请关注剩余存储空间是否足够。 |

7.  单击**确定**。

8.  （**回档到新实例**执行此步骤）在实例购买页面，设置新实例的参数并完成支付即可。参数说明如下。

    |参数名称|说明|
    |----|--|
    |**可用区**|可用区是地域中的一个独立物理区域，不同可用区之间没有实质性区别。

 您可以选择将RDS实例与ECS实例创建在同一可用区或不同的可用区。 **说明：** 新实例的地域与原实例相同，不支持修改。 |
    |**规格**|每种规格都有对应的CPU核数、内存、最大连接数和最大IOPS。具体请参见[实例规格表](/intl.zh-CN/云数据库 RDS 简介/产品规格/主实例规格列表.md)。|
    |**存储空间**|该存储空间包括数据空间、系统文件空间、Binlog文件空间和事务文件空间。|
    |**网络类型**|    -   **经典网络**：传统的网络类型。
    -   **专有网络**（推荐）：也称为VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。 |


## 常见问题

-   备份文件从tar压缩包变成xbstream文件包，会导致之前的备份不可用吗？

    之前的备份仍然可用。

-   之前可以使用单库单表恢复，为什么突然不能用了？

    可能您实例内的表数量过多。实例内的表低于50000张才可以使用单库单表恢复功能，超过50000张表时无法使用。


## 相关API

|API|描述|
|---|--|
|[单库单表恢复](/intl.zh-CN/API 参考/恢复/单库单表恢复.md)|恢复RDS实例的某个数据库或表到原实例上。|
|[克隆实例](/intl.zh-CN/API 参考/恢复/克隆实例.md)|恢复RDS实例的某个数据库或表到新实例上。|
|[查询备份恢复范围](/intl.zh-CN/API 参考/恢复/查询备份恢复范围.md)|查询RDS实例备份可恢复的时间范围。|


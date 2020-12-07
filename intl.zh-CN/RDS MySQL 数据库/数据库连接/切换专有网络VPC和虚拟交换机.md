# 切换专有网络VPC和虚拟交换机

您可以直接切换部分实例的专有网络VPC和虚拟交换机。

-   对于本地盘实例，您可以直接修改专有网络VPC和虚拟交换机。
-   对于云盘实例，您只能修改虚拟交换机，无法修改专有网络VPC。

**说明：** PostgreSQL引擎切换专有网络VPC和虚拟交换机请参见[切换虚拟交换机](/intl.zh-CN/RDS PostgreSQL 数据库/网络/VPC/交换机/切换虚拟交换机.md)。

## 影响

-   切换过程会有30秒闪断，请确保应用程序具有重连机制。
-   切换专有网络VPC和虚拟交换机会造成虚拟IP（VIP）的变更，请您在应用程序中尽量使用[连接地址]()进行连接，不要使用IP地址。
-   VIP的变更会短暂影响到DRDS的可用性，请及时在DRDS控制台刷新并查看连接信息。
-   VIP的变更会短暂影响到[DMS](https://www.alibabacloud.com/help/zh/doc-detail/47550.htm)、[DTS](https://www.alibabacloud.com/help/zh/doc-detail/26592.htm)的使用，变更结束后会自动恢复正常。
-   客户端缓存会导致只能读取数据，无法写入数据，请及时清理缓存。

## 操作步骤

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏选择**数据库连接**。

5.  在右侧单击**切换交换机**。

6.  选择VPC和虚拟交换机，并单击**确定**。

    **说明：** 如需新建VPC或虚拟交换机请单击**到控制台创建**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8277559951/p59958.png)

7.  在弹出的风险提示框中单击**确定切换**。


## 常见问题

不支持直接切换VPC和交换机的实例如何变更VPC？

-   对于支持从VPC切换到经典网络，以及支持从经典网络切换到VPC的实例：

    1.  将网络模式从VPC切换为经典网络。
    2.  将网络模式从经典网络切换至目的VPC。
    **说明：** 切换步骤请参见[切换网络类型](/intl.zh-CN/RDS MySQL 数据库/数据库连接/切换网络类型.md)。

-   对于不支持网络类型切换的实例：

    购买新的实例（购买时选择目的VPC），然后将数据迁移到新的实例。详情请参见[MySQL实例间数据迁移](/intl.zh-CN/RDS MySQL 数据库/数据迁移/RDS实例间数据迁移.md)。


## 相关文档

对于不支持直接切换专有网络VPC和虚拟交换机的实例，请您参见[RDS实例如何变更VPC](/intl.zh-CN/常见问题/连接/网络/RDS实例如何变更VPC.md)。


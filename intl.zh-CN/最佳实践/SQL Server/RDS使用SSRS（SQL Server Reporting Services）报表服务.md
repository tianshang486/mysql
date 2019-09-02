# RDS使用SSRS（SQL Server Reporting Services）报表服务 {#task_1580281 .task}

您可以使用ECS实例安装SSRS（SQL Server Reporting Services）报表服务器，然后基于RDS for SQL Server的数据输出报表。本文介绍如何将RDS for SQL Server作为数据源。

微软的SQL Server产品中包含SQL Server数据库引擎、Reporting Services（SSRS）、Analysis Services（SSAS）等服务端组件。其中SQL Server数据库引擎作为一个标准的关系型数据库组件，在阿里云上以RDS for SQL Server数据库产品的形式提供了标准的PaaS服务。但其他如SSRS等组件是以单独的Windows服务的方式运行的，在阿里云上并未以PaaS服务的形式提供。如果要在阿里云上使用SSRS服务，需要单独创建Windows系统的ECS实例，并安装配置SSRS服务组件。

**说明：** 目前暂不支持在RDS for SQL Server上创建SSRS的配置数据库。

## 前提条件 {#section_5iy_p7v_igq .section}

-   已[创建RDS for SQL Server实例](../../../../intl.zh-CN/RDS for SQL Server 快速入门/创建RDS for SQL Server实例.md#)。
-   已[创建Windows系统的ECS实例](https://www.alibabacloud.com/help/zh/doc-detail/87190.htm)。
-   ECS实例已[安装SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/installation-for-sql-server?view=sql-server-2017)。

**说明：** ECS实例内安装的SQL Server版本可以和RDS for SQL Server的版本不同。

## 操作步骤 {#section_umx_t6u_68i .section}

1.  在ECS实例上下载[Reporting Services](https://www.microsoft.com/zh-CN/download/details.aspx?id=55252)并安装。
2.  打开Report Server Configuration Manager软件，确认报表服务器名称并单击**连接**。 

    **说明：** 软件会自动检测ECS内的SQL Server报表服务器实例，如果有多个实例，需要您手动选择。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156738817654639_zh-CN.png)

3.  在左侧导航栏根据您的业务情况设置**服务账号**、**WEB服务URL**。 

    **说明：** 详细设置请参见[官方文档](https://docs.microsoft.com/en-us/sql/reporting-services/install-windows/install-reporting-services?view=sql-server-2017)。

4.  在左侧导航栏选择**数据库**，然后单击右侧的**更改数据库**，在ECS实例上创建新的报表服务器数据库。 

    1.  选择**创建新的报表服务器数据库**，单击**下一步**。
    2.  确认服务器名称，单击**下一步**。
    3.  填写报表服务器数据库名称并选择脚本使用的语言，单击**下一步**。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156738817754641_zh-CN.png)

    4.  设置账户连接报表服务器的凭据，单击**下一步**。
    5.  确认摘要，单击**下一步**，等待报表服务器数据库创建完成。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156738817754642_zh-CN.png)

    6.  单击**完成**。
    **说明：** 详细设置说明请参见[官方文档](https://docs.microsoft.com/en-us/sql/reporting-services/install-windows/install-reporting-services?view=sql-server-2017)。

5.  在左侧导航栏选择**WEB门户URL**，单击**应用**，等待应用完成后单击URL登录报表服务器的WEB管理页面。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156738817754644_zh-CN.png)

6.  在右上角选择**新建** \> **数据源**。
7.  设置新建数据源的各项参数。 

    |类别|参数|说明|
    |--|--|--|
    |**属性**|**名称**|新建数据源的名称。不能包含以下任何字符：/ @ $ & \* + = < \> : ' , ? | \\|
    |**说明**|数据源的描述，便于进行业务区分。|
    |**隐藏此项**|勾选后会隐藏此数据源。|
    |**启用此数据源**|勾选后才会启用此数据源。|
    |**连接**|**类型**|数据源类型。选择**Microsoft SQL Server**。|
    |**连接字符串**|RDS for SQL Server实例的域名和数据库名。格式：`Data Source=<RDS for SQL Server实例域名>; Initial Catalog=<数据库名>` **说明：** 请确保RDS实例的IP白名单已放通ECS实例的IP，详情请参见[设置白名单](../../../../intl.zh-CN/RDS for SQL Server 快速入门/初始化配置/设置白名单.md#)。

 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253389/156738817754649_zh-CN.png)

|
    |**凭据**|**登录数据源**|选择**使用以下凭据**。|
    |**凭据类型**|选择**数据库用户名和密码**。|
    |**用户名**|RDS for SQL Server实例的数据库账号。|
    |**密码**|RDS for SQL Server实例的数据库账号对应的密码。|

8.  单击**创建**。

数据源创建完成后您可以使用Report Builder、Visutal Studio等软件设计报表。详情请参见[Report Builder in SQL Server](https://docs.microsoft.com/en-us/sql/reporting-services/report-builder/report-builder-in-sql-server-2016?view=sql-server-2017)。


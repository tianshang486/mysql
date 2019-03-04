# 使用 DTS 迁移 SQL Server 数据 {#concept_cs3_4wv_ydb .concept}

使用数据传输服务 （DTS） 将本地数据库迁移到 RDS for SQL Server，可以实现应用不停服务的情况下，平滑完成数据库的迁移工作。

## 背景信息 {#section_mgv_dwv_ydb .section}

DTS 支持 SQL Server 数据结构迁移和全量迁移。

-   结构迁移

    DTS 会将本地数据库的结构定义迁移到目标实例。目前DTS支持结构迁移的对象有：表、视图、表触发器、同义词、SQL 存储过程、SQL 函数、自定义类型、plan guid、rule、default。

-   全量迁移

    DTS 会将本地数据库迁移对象的数据全部迁移到目标实例。如果在迁移过程中有增量更新的话，这些增量不会被迁移到目标库。所以建议在业务无写入时，使用 DTS 进行全量数据迁移。


## 迁移限制 {#section_bxq_2wv_ydb .section}

将本地数据库迁移到 RDS 上有以下限制：

-   迁移过程中，不支持 DDL 操作。
-   结构迁移不支持 assemblies、库级存储过程、service broker、全文索引、全文目录、分布式 schema、分布式函数、CLR 标量函数、CLR 标值函数、内部表、聚合函数和系统的迁移。
-   如果使用了对象名映射功能后，依赖这个对象的其他对象可能迁移失败。

## 前提条件 {#section_zw5_fwv_ydb .section}

已完成 RDS 实例数据库的准备，可参见如下资料：

-   [设置连接地址](cn.zh-CN/RDS for SQL Server 用户指南/数据库连接/设置连接地址.md#)
-   [创建数据库和账号SQL Server 2017版](../cn.zh-CN/RDS for SQL Server 快速入门/初始化配置/创建数据库和账号/创建数据库和账号SQL Server 2017版.md#)
-   [创建数据库和账号SQL Server 2012/2016版](../cn.zh-CN/RDS for SQL Server 快速入门/初始化配置/创建数据库和账号/创建数据库和账号SQL Server 2012__2016版.md#)
-   [创建数据库和账号SQL Server 2008 R2版](../cn.zh-CN/RDS for SQL Server 快速入门/初始化配置/创建数据库和账号/创建数据库和账号SQL Server 2008 R2版.md#)

## 操作步骤 {#section_ftm_gwv_ydb .section}

本例以有公网 IP 的本地数据库迁移到 RDS 上为例。

**准备本地数据**

在正式迁移之前，需要先在本地数据库和RDS实例中创建迁移账号，并在RDS实例中创建要迁移的数据库，并将要迁移的数据库的读写权限授权给迁移账号。不同的迁移类型需要不同的权限，如下表所示。

|迁移类型|结构迁移|全量迁移|
|----|----|----|
|本地数据库|select|select|
|RDS 实例|读写权限|读写权限|

1.  在本地数据库中创建迁移账号。

    ```
    create login username with password='password', default_database=mydb;
    go
    create user username for login username with default_schema=dbo;
    go
    ```

    参数说明：

    -   username：要创建的账号
    -   password：该账号的登录密码
    -   mydb：默认连接的数据库
    -   dbo：默认的数据表
    例：要创建账号为 William，密码为 Changme123 的账号访问数据 mydb 的数据表 dbo，命令如下：

    ```
    create login William with password='Changme123', default_database=mydb;
    go
    create user William for login William with default_schema=dbo;
    go
    ```

2.  在本地数据库中给迁移账号授权，本地数据库中迁移账号的权限要求请参见上表。

    ```
    GRANT privileges ON tablename TO username WITH GRANT OPTION;
    ```

    参数说明：

    -   privileges：该账号的操作权限，如 SELECT、INSERT、UPDATE 等。如果要授权该账号所有权限，则使用 *ALL*
    -   tablename：表名。如果要授权该账号所有的表权限，则使用通配符 *\**
    -   username：要授权的账号名
    -   WITH GRANT OPTION：授权该账号能使用GRANT命令，该参数为可选
    例：授权账号 *William* 对所有数据库和表的所有权限，命令如下：

    ```
    GRANT ALL ON* TO William;
    ```


**正式迁移操作**

1.  在 [RDS 管理控制台](https://rds.console.aliyun.com/) 上单击**迁移数据库**，进入[DTS](http://dts.console.aliyun.com/)，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334285_zh-CN.png)

2.  单击**创建在线迁移任务**，进入创建迁移任务页面，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334286_zh-CN.png)

3.  输入任务名称、本地数据库信息和目标数据库信息，单击授权白名单并进入下一步，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334287_zh-CN.png)

    -   任务名称：自定义任务名称，可以保持默认值
    -   源库信息
        -   实例类型：本地数据库的实例类型，可以选择 有公网 IP 的自建数据库、ECS 上的自建数据库、RDS 实例、云数据库 MongoDB。
        -   数据库类型：本地数据库的类型，可以选择 Oracle、MySQL、SQLServer、PostgreSQL、MongoDB。
        -   主机名或IP地址：本地数据库的公网地址。
        -   端口：本地数据库的公网端口。
        -   账号：本地数据库的迁移账号。
        -   密码：本地数据库迁移账号对应的密码。
    -   目标库信息
        -   实例类型：默认为 RDS 实例。
        -   RDS实例ID：目标 RDS 实例的 ID。单击下拉菜单将自动联想当前登录管理控制台的账号的 RDS 实例，点击选择所需要的实例。
        -   数据库名称：要迁移到目标数据库的名称。
        -   账号：目标 RDS 数据库的迁移账号。
        -   密码：目标 RDS 数据库迁移账号对应的密码。
4.  择迁移类型，并在迁移对象中选择要迁移的对象，单击**\>**将要迁移的对象放入已选择中，单击**预检查并启动**，如下图所示。

    **说明：** 

    -   数据迁移只会将本地数据库的数据（结构）复制一份到目标数据库，并不会对本地数据库数据（结构）造成影响
    -   数据迁移过程中，不支持DDL操作，如进行DDL操作可能导致迁移失败
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334288_zh-CN.png)

    如果要修改迁移对象在目标数据库上的名字，可以在已选择列表右侧单击**编辑** ，修改已选择的对象名称，如上图中4所示。

    **说明：** 以下以预检查不通过为例进行描述，如果预检查通过，请直接参见步骤 8。

5.  系统显示预检查结果，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334289_zh-CN.png)

6.  单击检测结果为失败的检测项后的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41612/155166533339863_zh-CN.png)，查看失败详细信息，根据失败详细信息完成错误排查。
7.  错误排查完毕后，在迁移任务列表页面，选择当前迁移任务，单击**启动**，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334290_zh-CN.png)

8.  系统预检查通过后，单击**确定**，自动进行迁移任务，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7979/15516653334291_zh-CN.png)


## 后续操作 {#section_hqh_ywv_ydb .section}

为了保证本地数据库安全，请在数据迁移完成后，删除本地数据库和 RDS 实例中的迁移账号。


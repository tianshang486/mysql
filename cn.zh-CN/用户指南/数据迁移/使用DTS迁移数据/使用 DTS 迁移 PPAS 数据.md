# 使用 DTS 迁移 PPAS 数据 {#concept_jzf_2vv_ydb .concept}

使用数据传输服务（DTS）将本地数据库迁移到 RDS for PPAS，可以实现应用不停服务的情况下，平滑完成数据库的迁移工作。迁移过程中，对本地的 Oracle 数据库没有影响。

## 背景信息 {#section_vy5_v5v_ydb .section}

DTS 数据迁移支持 PPAS 的结构迁移和全量迁移。

-   结构迁移

    DTS 会将迁移对象的结构定义迁移到目标实例。目前 DTS 支持结构迁移的对象有：表、视图、同义词、触发器、存储过程、存储函数、包、自定义类型。

-   全量迁移

    DTS 会将本地数据库迁移对象的数据全部迁移到目标实例。如果迁移过程中，本地 Oracle 数据库有数据写入的话，那么这些增量数据不一定能够被迁移到 RDS 中。所以，如果要保证数据一致性，那么尽量选择在业务低峰期进行全量迁移。


## 迁移限制 {#section_gtp_w5v_ydb .section}

将 PPAS 本地数据库迁移到 RDS 上有以下限制。

-   迁移过程中，不支持 DDL 操作。
-   不支持物化视图的迁移。
-   结构迁移时，会将 reverse index 迁移成普通索引。
-   结构迁移时，会将位图索引迁移成普通索引。
-   结构迁移时，会将分区索引迁移成在每个分区上单独创建的索引。

## 前提条件 {#section_gsw_x5v_ydb .section}

已完成 RDS 实例数据库的准备，可参见[设置连接地址](intl.zh-CN/用户指南/数据库连接/设置连接地址.md#)和 [创建数据库和账号](../intl.zh-CN/RDS for PPAS 快速入门/初始化配置/创建数据库和账号.md#)。

## 操作步骤 {#section_y1v_y5v_ydb .section}

本例以有公网 IP 的本地数据库迁移到 RDS 上为例。

**准备本地数据**

在正式迁移之前，需要先在本地数据库和 RDS 实例中创建迁移账号，并在 RDS 实例中创建要迁移的数据库，并将要迁移的数据库的读写权限授权给迁移账号。不同的迁移类型需要不同的权限，如下表所示。

|迁移类型|结构迁移|全量迁移|
|----|----|----|
|本地 Oracle 实例|schema 的 owner|schema 的 owner|
|RDS 上 PPAS 实例|schema 的 owner|schema 的 owner|

1.  通过 PostgreSQL 客户端，在本地数据库中创建迁移账号。

    ```
    CREATE USER username IDENTIFIED BY password;
    ```

    参数说明：

    -   username：要创建的账号
    -   password：该账号的登录密码
    如：

    ```
    CREATE USER myuser IDENTIFIED BY mypassword;
    ```

2.  在本地数据库中给迁移账号授权，本地数据库中迁移账号的权限要求请参见上表。

    ```
    GRANT privileges ON tablename TO username;
    ```

    参数说明：

    -   privileges：该账号的操作权限，如 SELECT、INSERT、UPDATE 等。如果要授权该账号所有权限，则使用 *ALL*
    -   tablename：表名。如果要授权该账号所有的表权限，则使用通配符 *\**
    -   username：要授权的账号名
    如：

    ```
    GRANT ALL ON* TO myuser;
    ```


**正式迁移操作**

1.  在 [RDS 管理控制台](https://rds.console.aliyun.com/) 上单击 **迁移数据库**，进入 [DTS](http://dts.console.aliyun.com/)，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474276_zh-CN.png)

2.  单击 **创建在线迁移任务**，进入创建迁移任务页面，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474277_zh-CN.png)

3.  输入任务名称、本地数据库信息和目标数据库信息，单击 **授权白名单并进入下一步**，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474278_zh-CN.png)

    -   任务名称：自定义任务名称，可以保持默认值
    -   源库信息
        -   **实例类型**：本地数据库的实例类型，这里选择**有公网 IP 的自建数据库**。
        -   **实例地区**：实例所属的地域。
        -   **数据库类型**：本地数据库的类型，这里选择**Oracle**。
        -   **主机名或IP地址**：本地数据库的公网地址。
        -   **端口**：本地数据库的公网端口。
        -   **实例类型**：本地数据库是否为RAC集群。
        -   **SID**：本地数据库的 SID。
        -   **数据库账号**：本地数据库的迁移账号。
        -   **数据库密码**：本地数据库迁移账号对应的密码。
    -   目标库信息
        -   **实例类型**：云数据库的实例类型，这里选择**RDS 实例**。
        -   **实例地区**：实例所属的地域。
        -   **RDS实例ID**：目标RDS实例的ID。点击下拉菜单将自动联想当前登录管理控制台的账号的RDS实例，点击选择实例。
        -   **数据库名称**：要迁移到目标数据库的名称。
        -   **数据库账号**：RDS数据库的迁移账号。
        -   **数据库密码**：RDS数据库迁移账号对应的密码。
4.  择迁移类型，并在迁移对象中选择要迁移的对象，单击**\>**将要迁移的对象放入已选择中，单击**预检查并启动**，如下图所示。

    **说明：** 

    -   选择结构迁移时，如果目标 RDS 实例的数据库mydatabase中，不存在跟本地数据库迁移账号同名的 Schema，那么 DTS 会自动创建同名Schema， 且Schema的Owner为迁移账号。
    -   数据迁移只会将本地数据库的数据（结构）复制一份到目标数据库，并不会对本地数据库数据（结构）造成影响。
    -   数据迁移过程中，不支持DDL操作，如进行DDL操作可能导致迁移失败。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474279_zh-CN.png)

    如果要修改迁移对象在目标数据库上的名字，可以在 *已选择* 列表右侧单击 **编辑**，修改已选择的对象名称，如上图4所示。

5.  此步骤以预检查不通过为例进行描述，如果预检查通过，请直接参见步骤 8。

    系统显示预检查结果，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474280_zh-CN.png)

6.  单击 检测结果 为失败的检测项后的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62525/155288834739855_zh-CN.png)，查看失败详细信息，根据失败详细信息完成错误排查。
7.  错误排查完毕后，在迁移任务列表页面，选择当前迁移任务，单击**启动**，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474281_zh-CN.png)

8.  系统预检查通过后，单击**确定**，自动进行迁移任务，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7978/15528883474282_zh-CN.png)


## 后续操作 {#section_vdk_4vv_ydb .section}

因迁移账号拥有读写权限，为了保证本地数据库安全，请在数据迁移完成后，删除本地数据库和 RDS 实例中的迁移账号。


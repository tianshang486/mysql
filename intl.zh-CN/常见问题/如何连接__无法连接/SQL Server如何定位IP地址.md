# SQL Server如何定位IP地址 {#concept_58941_zh .concept}

## 场景一 { .section}

**问题描述**

用户的公网IP不固定，使用本地IP查看工具定位到的IP不准确，即使将查询到的本地IP加入了RDS的白名单中，连接RDS的时候也会报错。所以，用户需要查询到准确的客户端IP才能访问RDS。

**注意事项**

如果您发现您本地设备的公网IP地址会变化，而且建立的连接是用于生产环境，则建议您改为使用内网连接，或者在白名单中配置合理的公网IP段，确保不会因为IP地址改变而断连。

**获取客户端IP**

1.  将IP地址0.0.0.0/0加入RDS实例的白名单中，操作方法请参见[设置白名单](../../../../intl.zh-CN/RDS for SQL Server 快速入门/初始化配置/设置白名单.md#)。

    **说明：** 将IP地址0.0.0.0/0添加到RDS实例的白名单中，代表允许任何IP访问RDS实例。

2.  使用客户端[连接RDS的SQL Server数据库](../../../../intl.zh-CN/RDS for SQL Server 快速入门/连接实例.md#)。
3.  执行如下命令，查询客户端IP。

    ```language-sql
    SELECT  CONNECTIONPROPERTY('PROTOCOL_TYPE') AS PROTOCOL_TYPE,
            CONNECTIONPROPERTY('CLIENT_NET_ADDRESS') AS CLIENT_NET_ADDRESS
    
    ```

4.  将步骤 **1** 在白名单中添加的 0.0.0.0/0 条目删除，添加上真实的出口IP。

## 场景二 {#section_vsk_1ym_1gb .section}

**问题描述**

若您想要统计已连接到RDS的SQL Server数据库的所有IP，或定位一些安全问题，如链接泄露等，您可以使用获取已连接到数据库的所有IP的方法。

**获取所有连接到数据库的IP**

1.  将IP地址0.0.0.0/0加入RDS实例的白名单中，操作方法请参见[设置白名单](../../../../intl.zh-CN/RDS for SQL Server 快速入门/初始化配置/设置白名单.md#)。
2.  使用客户端连接RDS的SQL Server数据库。
3.  执行如下命令，查询所有连接到数据库的IP。

    ```language-sql
    SELECT
    SP.SPID,
    SP.LOGINAME,
    SP.LOGIN_TIME,
    SP.HOSTNAME,
    SP.PROGRAM_NAME,
    DC.CLIENT_TCP_PORT,
    DC.CLIENT_NET_ADDRESS
    FROM SYS.SYSPROCESSES AS SP
    INNER JOIN SYS.DM_EXEC_CONNECTIONS AS DC
    ON SP.SPID = DC.SESSION_ID
    WHERE SP.SPID > 50
    AND DC.AUTH_SCHEME='SQL'
    
    ```

4.  将在步骤**1**中添加的0.0.0.0/0或您公司的IP段从白名单中删除。

## 查看更详细的连接参数配置 { .section}

在查询到已连接到数据库的所有IP后，若您需要查看单个连接更详细的参数配置，请执行如下命令：

```language-sql
SELECT * FROM SYS.DM_EXEC_SESSIONS WHERE SESSION_ID=<之前获取的SPID>

```


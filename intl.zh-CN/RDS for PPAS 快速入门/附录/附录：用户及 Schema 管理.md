# 附录：用户及 Schema 管理 {#concept_wnj_xxg_wdb .concept}

在使用 RDS 的过程中，由于 superuser 不完全放开，因此我们建议您在使用数据库时遵循单独建立用户并通过 schema 管理您的私有空间。

## 操作步骤 {#section_b1y_zxg_wdb .section}

**说明：** 本例中，myadmin 是建立实例时创建的管理账号，newuser 是当前需要新建的账号。

1.  建立有登录权限的用户。

    ```
    CREATE USER newuser LOGIN PASSWORD 'password';
    ```

    参数说明如下：

    -   USER：要创建的用户名，如 **newuser**。
    -   PASSWORD：用户名对应的密码，如 **password**。
2.  为新用户建立 schema。

    ```
    CREATE SCHEMA newuser;GRANT newuser to myuser;ALTER SCHEMA myuser OWNER TO newuser;REVOKE newuser FROM myuser;
    ```

    **说明：** 

    -   如果在进行 `ALTER SCHEMA newuser OWNER TO newuser` 之前没有将 newuser 加入到 myuser 角色，将会出现如下权限问题：

        ```
        ERROR: must be member of role "newuser"
        ```

    -   从安全角度出发，在处理完 OWNER 的授权后，请将 newuser 移出 myuser 角色以提高安全性。
3.  用新用户 newuser 进行数据库登陆。

    ```
    psql -U newuser -h intranet4example.pg.rds.aliyuncs.com -p 3433 pg001
    Password for user newuser:
    psql.bin (9.4.4, server 9.4.1)
    Type "help" for help.
    ```



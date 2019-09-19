# 附录：用户及 Schema 管理 {#concept_wnj_xxg_wdb .concept}

在使用 RDS 的过程中，由于 superuser 不完全放开，因此我们建议您在使用数据库时遵循单独建立用户并通过 schema 管理您的私有空间。

## 操作步骤 {#section_b1y_zxg_wdb .section}

**说明：** 本例中，myadmin 是建立实例时创建的管理账号，newuser 是当前需要新建的账号。

1.  用初始管理帐号登录数据库，如控制台中已经建立初始帐号的 myadmin。

    ``` {#codeblock_3wo_6qn_99m}
    psql -U myadmin -h intranet4example.pg.rds.aliyuncs.com -p 3433 pg001
    Password for user myadmin:
    psql.bin (9.4.4, server 9.4.1)
    Type "help" for help.
    ```

2.  建立普通帐号 newuser，密码为 password

    ``` {#codeblock_gp8_q1w_1pu}
    CREATE USER newuser LOGIN PASSWORD'password';
    ```

    参数说明如下：

    -   USER：要创建的用户名。
    -   password：用户名对应的密码。
3.  用新用户 newuser 进行数据库登录。

    ``` {#codeblock_963_bcr_5nt}
    psql -U newuser -h intranet4example.pg.rds.aliyuncs.com -p 3433 pg001
    Password for user newuser:
    psql.bin (9.4.4, server 9.4.1)
    Type "help" for help.
    ```

4.  建立新的业务DATABASE，并建立与用户 newuser 同名的 SCHEMA 作为业务的默认操作空间

    ``` {#codeblock_nc1_4k8_91i}
    CREATE DATABASE mydb;
    \c mydb;
    CREATE SCHEMA newuser;
    ```


**说明：** 

-   通过以上操作，用户 myadmin 将保持作为数据库的初始管理帐号。
-   所有用户业务操作都通过 mydb 进行处理，系统原生的系统库 edb 及 postgres 会存有系统表数据，不建议将业务数据放到系统库中。
-   以上操作以后库 mydb 库的主属用户将是 myuser，通过帐号 myuser 或以在此库建立任意对象


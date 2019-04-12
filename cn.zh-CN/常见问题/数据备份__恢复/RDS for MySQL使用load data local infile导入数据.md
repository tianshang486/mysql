# RDS for MySQL使用load data local infile导入数据 {#concept_183224 .concept}

RDS for MySQL不支持`load data infile`，因为这个命令要求待导入的文件必须在RDS实例上。但是您可以加上local关键字, 加上local后可以从客户端机器导入文件, 本文介绍如何使用`load data local infile`向RDS导入数据。

## 前提条件 {#section_hvp_qg0_o4h .section}

-   已对RDS实例设置白名单，申请外网地址，以及创建数据库和账号。详情请参见[快速入门](../../../../../cn.zh-CN/用户指南/快速入门.md#)。
-   已购买云服务器ECS，并且安装了与RDS for MySQL实例相同版本的mysql。
-   待导入的数据存储在txt文件中，示例如下。

    ![txt文档](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8298/155505027844294_zh-CN.png)


## 操作步骤 {#section_0en_7k9_x1n .section}

1.  登录ECS实例，修改mysql的配置文件my.cnf，加入一行配置`local-infile`。

    ![添加local-infile](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8298/155505027844295_zh-CN.png)

2.  在ECS实例上使用如下命令并输入高权限账号密码连接到RDS for MySQL实例：

    ``` {#codeblock_lii_f3q_0jk}
    mysql -h <RDS实例外网连接地址> -u <高权限账号名> -p
    ```

    ![连接RDS实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8298/155505027844296_zh-CN.png)

3.  执行如下命令导入：

    ``` {#codeblock_4jw_1sj_c3m}
    use <数据库名>;
    load data local infile '<待导入文件路径>' into table <表名> fields terminated by ',' lines terminated by '\n';
    ```

    **说明：** 

    -   into：导入时如果表有主键且表不为空，待导入文件里如果有相同的主键会报错并停止导入。可使用 replace into将新数据覆盖旧数据或者使用ingnore into来忽略主键冲突的记录。
    -   fields terminated ',' ：表示列之间使用逗号作为分隔符。
    -   lines terminated '\\n'：表示使用回车作为换行符，如果是Windows下的文件上传到Linux，需要使用 '\\r\\n' 。
    ![导入数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8298/155505027844299_zh-CN.png)



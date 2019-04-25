# RDS for MySQL远程获取Binlog {#concept_183137 .concept}

1.  首先[使用客户端连接实例](../../../../intl.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#section_fbz_ym5_vdb)后查看当前的binlog文件，命令如下：

    ``` {#codeblock_foz_t00_ku7}
    show master logs;
    ```

    或者

    ``` {#codeblock_8t9_xz8_n4u}
    show binary logs;
    ```

    ![查看当前binlog文件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8289/155618373345484_zh-CN.png)

2.  例如需要远程获取的是mysql-bin.000497，可以通过`--read-from-remote-server`参数实现远程读取并保存到本地的a.sql文件中：

    ``` {#codeblock_62c_e6x_u1y}
    mysqlbinlog  -umolan -p -hffffffffffffff.mysql.rds.aliyuncs.com --read-from-remote-server mysql-bin.000497 >a.sql
    ```

    ![远程读取](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8289/155618373445486_zh-CN.png)

3.  保存后即可进行查看。

    ![保存查看](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8289/155618373445487_zh-CN.png)



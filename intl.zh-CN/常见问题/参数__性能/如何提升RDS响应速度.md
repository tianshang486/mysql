# 如何提升RDS响应速度 {#concept_gwv_y4n_jhb .concept}

NSCD（Name Service Cache Daemon）是一种能够缓存passwd、group、hosts的本地缓存服务。若您使用短连接的方式连接RDS，请在与RDS相连的ECS实例上进行如下操作开启NSCD，提升RDS响应速度。

**说明：** ECS开启NSCD后，如果RDS的域名有变更，会影响生效时间。应用端如果要切换RDS域名，需要重点关注域名生效时间。

1.  在云服务器上执行如下命令安装NSCD：
    -   Ubuntu系统：`apt-get install nscd`
    -   CentOS 及 Aliyun Linux 系统：`yum install nscd`
2.  执行如下命令启动NSCD：

    ```
    service nscd start
    ```

    ![启动nscd](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8396/155488705544171_zh-CN.jpg)

3.  查看NSCD是否启动成功，命令如下：

    ```
    ps -ef|grep nscd
    ```

    **说明：** 若NSCD启动成功，则会返回如下结果。

    ![检查nscd](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8396/155488705544173_zh-CN.jpg)

4.  修改DNS解析文件，在 /etc/resolv.conf 文件中添加`options timeout:1 attempts:1`。


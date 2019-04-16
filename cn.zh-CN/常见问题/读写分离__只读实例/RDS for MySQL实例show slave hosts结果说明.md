# RDS for MySQL实例show slave hosts结果说明 {#concept_185342 .concept}

-   当RDS实例单独使用时（即未使用只读实例），执行`show slave hosts;`结果如下。

    ![单实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8302/155540492744582_zh-CN.png)

    显示的slave端是RDS实例的备实例，以确保RDS实例的高可用。

-   当RDS实例创建过只读实例，通过`show slave hosts;`显示三个slave端，如下图。

    ![只读实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8302/155540492744583_zh-CN.png)

    它们分别是：主实例的备实例、只读实例、只读实例的备实例，其中两个备实例用于保证RDS主实例与RDS只读实例的高可用。



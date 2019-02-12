# RDS for MySQL如何终止会话 {#concept_41713_zh .concept}

RDS for MySQL有两种方式来终止会话。

## 通过DMS终止 {#section_o5d_wfp_tgb .section}

1.  [通过DMS登录RDS数据库](../../../../../cn.zh-CN/RDS for MySQL 用户指南/附录/通过DMS登录RDS数据库.md#)。
2.  在上方选择**性能** \> **实例会话**。

    ![dms查看实例会话](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8303/154996337938756_zh-CN.png)

3.  在弹出的会话框中选择新版并进行授权（仅首次登录需授权）。
4.  通过Shift、Ctrl键选择多个会话，然后通过**kill选中会话**按钮来终止相关会话。

    ![kill会话](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8303/154996337938757_zh-CN.png)


## 通过kill命令终止 {#section_fc2_wfp_tgb .section}

1.  通过MySQL命令行工具连接实例，请参见[连接实例](../../../../../cn.zh-CN/RDS for MySQL 快速入门/连接实例.md#)。

    **说明：** RDS实例在连接数已满的情况下，是无法通过DMS或者MySQL命令行工具连接实例的。如果无法通过DMS或MySQL命令行工具连接，建议先在控制台的参数设置中将 wait\_timeout参数（单位秒）设置为比较小的值（比如 60），让RDS实例主动关闭空闲时间超过60秒的连接，以便稍后可以通过DMS或者MySQL命令行工具连接访问实例。

2.  通过如下命令查看当前会话情况，记下想要kill的会话的Id。

    ```
    show processlist;
    ```

    ![命令行查看会话](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8303/154996337938758_zh-CN.png)

3.  通过如下命令kill会话。

    ```
    kill <Id>;
    ```

    ![命令行kill会话](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8303/154996337938759_zh-CN.png)



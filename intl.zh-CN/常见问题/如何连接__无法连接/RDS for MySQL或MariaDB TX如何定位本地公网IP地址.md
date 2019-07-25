# RDS for MySQL或MariaDB TX如何定位本地公网IP地址 {#concept_qfv_2g5_42b .concept}

## 问题描述 {#section_f4x_fg5_42b .section}

-   已经将本地设备的公网IP地址添加到RDS白名单，但是仍然无法访问RDS实例，而其他设备能访问该RDS实例。
-   已经将本地设备的公网IP地址添加到RDS白名单，但是仍然无法访问RDS实例，而将RDS白名单设置为公司的网段或者0.0.0.0/0后，该设备可以访问RDS实例。

以上的任意一种情形，都很可能是因为您添加到白名单的本地设备公网IP地址不正确，本文介绍如何查询到本地设备的真实出口IP地址。

**说明：** 本文只适用于ECS以外的设备访问RDS实例的情况。如果是ECS实例访问RDS实例，可以在ECS实例的详情页面查看准确的公网IP地址和内网IP地址。

## 注意事项 {#section_nby_fjp_yfb .section}

如果您发现您本地设备的公网IP地址会变化，而且建立的连接是用于生产环境，则建议您改为使用内网连接，或者在白名单中配置合理的公网IP段，确保不会因为IP地址改变而断连。

## 定位本地设备的公网IP地址 {#section_ffh_njp_yfb .section}

1.  将公司的公网网段或者0.0.0.0/0添加到RDS for MySQL或MariaDB TX实例的白名单，具体操作请参见[设置白名单](../../../../intl.zh-CN/RDS for MySQL 快速入门/初始化配置/设置白名单.md#)。

    **说明：** 0.0.0.0/0表示允许任何设备访问RDS实例，有安全风险，请谨慎使用。如果使用，应当及时从白名单中删除。

2.  在本地设备，使用客户端或命令行连接到RDS实例。

    ``` {#codeblock_04n_16m_opt}
    mysql -hRDS连接地址 -u账户 -p密码 -P3306
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8224/156403352333319_zh-CN.jpg)

3.  查询进程信息。

    ``` {#codeblock_6w0_zz8_db5}
    show processlist
    ```

    如下图所示， **show processlist** 所在的行对应的 **Host** 就是本地设备的真实出口 IP 地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8224/156403352433320_zh-CN.jpg)

4.  将步骤 **1** 中在白名单中添加的 0.0.0.0/0 条目删除，添加上真实的出口 IP。


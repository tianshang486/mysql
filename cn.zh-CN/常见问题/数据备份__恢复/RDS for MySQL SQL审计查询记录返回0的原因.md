# RDS for MySQL SQL审计查询记录返回0的原因 {#concept_jjw_z25_jhb .concept}

RDS for MySQL的SQL审计功能保存了执行的SQL记录，包括连接的客户端IP、数据库名称、执行语句账号、SQL语句等等。

以下2种情况会导致返回记录数为 0 ：

-   **未查询到数据**

    ![未查询到数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8272/155496313444240_zh-CN.png)

-   **从查询缓存中获取的数据**

    如果实例开启了查询缓存（Query Cache），那么从查询缓存中获取数据的查询，其返回记录数会显示为 0，详情请参见[RDS for MySQL查询缓存（Query Cache）的设置和使用](cn.zh-CN/常见问题/参数__性能/RDS for MySQL查询缓存（Query Cache）的设置和使用.md#)。

    ![查询缓存](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8272/155496313444241_zh-CN.png)

    ![缓存后无法查询](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8272/155496313444242_zh-CN.png)



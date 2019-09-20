# RDS for MySQL表级锁等待 {#concept_rms_nfz_3hb .concept}

在RDS for MySQL实例日常使用中，会出现表级锁等待的情况，下面列出常见的2个原因。

-   **显式lock table**

    执行了`lock tables tab_name read`导致DML会话等待表级锁。

    ![显式lock](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8292/156894970543509_zh-CN.png)

-   **隐式lock table**

    mysqldump使用默认参数进行数据导出时，会默认的开启**--lock-tables**选项，进而导致导出表上的DML操作等待表级锁。

    **说明：** 对于使用mysqldump导出数据，建议在业务低峰期进行，并且设置**--single-transaction**选项进行Innodb引擎表导出，避免出现表级锁等待的情况。

    ![隐式lock](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8292/156894970543510_zh-CN.png)



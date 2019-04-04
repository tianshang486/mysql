# RDS for MySQL如何修改为utf8mb4字符集 {#concept_f5x_frv_hhb .concept}

## 操作步骤 {#section_svq_prv_hhb .section}

1.  [连接MySQL实例](../../../../../cn.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#)。
2.  在SQL窗口使用如下命令进行修改。

    ```
    修改库：    
    ALTER DATABASE <数据库名> CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
    修改表:
    ALTER TABLE <表名> CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    修改一列:
    ALTER TABLE <表名> CHANGE <列名> <字段类型> CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ```



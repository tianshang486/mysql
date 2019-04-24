# RDS for MySQL存储过程的创建和查看 {#concept_fyb_wld_n2b .concept}

## 创建存储过程 {#section_atw_wld_n2b .section}

可以通过DMS或MySQL客户端登录到RDS， 创建存储过程。示例代码如下：

``` {#codeblock_388_1yd_44s}
DROP PROCEDURE IF EXISTS TEST_PROC;
DELIMITER //
CREATE PROCEDURE TEST_PROC(IN ID int,OUT NAME VARCHAR(50))
BEGIN
IF(ID = 1) THEN SET NAME = ‘test1’;
END IF;
IF(ID = 2) THEN SET NAME = ‘test2’;
END IF;
SELECT version();
END //;
```

```

```

![创建存储过程](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8258/155609027345301_zh-CN.jpg)

## 查看存储过程 {#section_htw_wld_n2b .section}

在RDS for MySQL中，有两种方法查看数据库中的存储过程：

-   **通过系统表查询** 

    登录到数据库中，执行如下命令：

    ```
    select * from mysql.proc where db=’‘ and type=’procedure’ order by name;
    ```

    ![查看存储过程](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8258/155609027345302_zh-CN.png)

-   **通过show status查询** 

    登录到数据库中，执行如下命令：

    ``` {#codeblock_0ui_2qa_x2y}
    show procedure status;
    show create procedure \G;
    ```

    ![show procedure](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8258/155609027345303_zh-CN.jpg)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8258/155609027345304_zh-CN.jpg)



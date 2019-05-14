# RDS for MySQL排序分页查询数据顺序错乱的处理 {#concept_265240 .concept}

## MySQL排序分页查询数据顺序错乱的原因 {#section_fhu_osk_2cc .section}

MySQL排序分页查询某些时候会出现数据顺序错乱的情况，例如：

``` {#codeblock_jig_ezz_ty1}
CREATE TABLE alarm_test (
  id bigint(20) NOT NULL DEFAULT '0',
  detail varchar(255) CHARACTER SET utf8 NOT NULL,
  created_on timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

按照created\_on字段值排序，取前10行，如下图。

![created_on前10](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8299/155782706547276_zh-CN.png)

按照created\_on字段值排序，取从11行开始的10行，如下图。

![created_on11](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8299/155782706647278_zh-CN.png)

可以看出，2次排序分页操作得到的数据是有重合而且无序的（实际上排序分页结果会根据情况的不同而变化，结果不可预料）。出现这个问题的原因在于created\_on字段的值在前21行记录中有20行数据相同。

## 如何使排序字段结果有序 {#section_2ib_svp_0en .section}

使排序字段结果有序有如下两个方法：

-   修改排序规则，加入主键字段，使排序字段不存在重复记录，例如：

    ``` {#codeblock_rgt_gd8_qr9}
    select id, created_on from alarm_test order by created_on, id limit 0,10;
    ```

    ![加入主键字段](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8299/155782706647279_zh-CN.png)

-   在出现重复值的排序字段上添加索引，例如：

    ``` {#codeblock_s57_2wf_5k8}
    CREATE TABLE alarm_test_idx (
      id bigint(20) NOT NULL DEFAULT '0',
      detail varchar(255) CHARACTER SET utf8 NOT NULL,
      created_on timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
      PRIMARY KEY (id),
      KEY created_on (created_on)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4
    ```

    ![添加索引](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8299/155782706647280_zh-CN.png)


**说明：** 推荐使用添加索引的方法，在提供可预期的结果同时，提高查询的执行效率。


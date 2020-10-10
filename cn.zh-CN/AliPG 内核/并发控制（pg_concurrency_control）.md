# 并发控制（pg\_concurrency\_control）

RDS PostgreSQL提供pg\_concurrency\_control插件，用于对SQL进行并发控制。

RDS PostgreSQL实例版本为PostgreSQL 10。

## 参数说明

**说明：** 暂不支持在控制台修改以下参数，您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请修改。

|参数|默认值|说明|
|--|---|--|
|pg\_concurrency\_control.query\_concurrency|0|设置Select类型SQL并发控制的排队个数限制。取值范围为0~1024，默认值为0，表示关闭Select类型SQL并发控制。|
|pg\_concurrency\_control.bigquery\_concurrency|0|设置慢查询类型SQL并发控制的排队个数限制。取值范围为0~1024，默认值为0，表示关闭慢查询类型SQL并发控制。您可以使用`hint "/*+bigsql*/"`的方式来指定一个请求为慢查询。例如：

```
/*+bigsql*/select * from test;
```

此时`select * from test;`被认为是一个慢查询。 |
|pg\_concurrency\_control.transaction\_concurrency|0|设置事务块并发控制的排队个数限制。取值范围为0~1024，默认值为0，表示关闭事务块并发控制。|
|pg\_concurrency\_control.autocommit\_concurrency|0|设置DML类型SQL并发控制的排队个数限制。取值范围为0~1024，默认值为0，表示关闭DML类型SQL并发控制。|
|pg\_concurrency\_control.control\_timeout|1秒|设置Select类型SQL、DML类型SQL和事务块的并发控制排队等待时间。最小值为30毫秒（ms），最大值为3秒（s）。|
|pg\_concurrency\_control.bigsql\_control\_timeout|1秒|设置慢查询并发控制排队等待时间。最小值为30毫秒（ms），最大值为3秒（s）。|
|pg\_concurrency\_control.timeout\_action|TCC\_break|设置Select类型SQL、DML类型SQL和事务块的并发控制等待超时后的行为。取值：-   TCC\_break：跳过等待继续执行。
-   TCC\_rollback：超时后报错，事务回滚。
-   TCC\_wait：超时后重置时间戳继续等待。 |
|pg\_concurrency\_control.bigsql\_timeout\_action|TCC\_wait|设置慢查询并发控制等待超时后的行为。取值：-   TCC\_break：跳过等待继续执行。
-   TCC\_rollback：超时后报错，事务回滚。
-   TCC\_wait：超时后重置时间戳继续等待。 |

## 使用方法

1.  使用如下命令创建插件：

    ```
    create extension pg_concurrency_control;
    ```

2.  设置并发控制排队个数限制大于0，即开启插件排队功能。

    例如设置pg\_concurrency\_control.query\_concurrency=10，即开启Select类型SQL并发控制功能。其余功能开启方式类似。

    **说明：** 暂不支持在控制台修改参数，您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请修改。


## 使用示例

对自定义SQL操作进行并发控制。

1.  使用如下命令查看排队视图：

    ```
    select * from pg_concurrency_control_status();
    ```

    系统输出类似如下结果：

    ```
     autocommit_count | bigquery_count | query_count | transaction_count 
    ------------------+----------------+-------------+-------------------
                    0 |              0 |           0 |                 0 
    (1 row)
    ```

2.  设置pg\_concurrency\_control.query\_concurrency大于0，例如10。

3.  执行慢查询语句：

    ```
    /*+ bigsql */ select pg_sleep(10);
    ```

4.  再次查看排队视图：

    ```
    select * from pg_concurrency_control_status();
    ```

    系统输出类似如下结果：

    ```
     autocommit_count | bigquery_count | query_count | transaction_count 
    ------------------+----------------+-------------+-------------------
                    0 |              1 |           0 |                 0 
    (1 row)
    ```

    **说明：** 慢查询执行完毕后，排队信息会自动清空。



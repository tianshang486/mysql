# RDS for PostgreSQL 9.4中如何支持jsonb\_set等新的 jsonb函数 {#concept_266112 .concept}

## 解决方案 {#section_9ck_15k_a35 .section}

1.  使用客户端连接数据库后执行如下命令：

``` {#codeblock_hgu_mnf_0lu}
create extension jsonbx;
```

**说明：** 如果遇到以下错误，请通过控制台重启数据库实例以升级到最新的9.4版本。

``` {#codeblock_lxg_cmm_mvj}
postgres=> create extension jsonbx;
ERROR:  invalid extension name: "jsonbxx"
DETAIL:  Extension is not supported.
```

2.  执行如下命令：

    ``` {#codeblock_fw8_f4l_9z1}
    jsonb_pretty (in 9.5)
    jsonb_concat (in 9.5)
    jsonb_delete(jsonb, text) (in 9.5)
    jsonb_delete_idx(jsonb, int) (in 9.5)
    jsonb_delete_path(jsonb, text[]) (in 9.5)
    jsonb_set(jsonb, text[], jsonb) (in 9.5)
    concatenation operator (||) (in 9.5)
    delete key operator (jsonb - text) (in 9.5)
    delete key by index operator (jsonb - int) (in 9.5)
    delete key by path operator (jsonb - text[]) (in 9.5)
    ```



# RDS for MySQL通过mysqlbinlog查看binlog日志 {#concept_d5p_pv4_mgb .concept}

当需要查看binlog日志中具体的SQL语句时，可以通过mysqlbinlog命令查看。

## 前提条件 {#section_kzz_4y4_mgb .section}

本地Linux主机已安装MySQL。

## 操作步骤 {#section_ep1_py4_mgb .section}

1.  在安装MySQL的本地Linux主机上[下载binlog日志文件](../../../../../cn.zh-CN/RDS for MySQL 用户指南/备份数据/下载数据备份和日志备份.md#)。
2.  在命令行中输入如下命令即可查看具体内容。

    ```
    mysqlbinlog -vv --base64-output=decode-rows <binlog文件路径>
    ```

    **说明：** 

    -   -vv：查看具体SQL语句及备注。
    -   --base64-output=decode-rows：解码。
    ![解码查看](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8293/155503646337626_zh-CN.png)


## 常见报错 {#section_xse_y02_i9w .section}

``` {#codeblock_hhk_xox_53m}
ERROR: Error in Log_event::read_log_event(): 'Sanity check failed', data_len: 151, event_type: 35
ERROR: Could not read entry at offset 120: Error in log format or read error.
```

请检查使用的mysqlbinlog版本，例如使用3.3版本会遇到上述错误，3.4版本可以正常查看，这种情况下您可以使用较高版本的mysqlbinlog。

## 常见错误 {#section_wwz_x1p_mgb .section}

忘记使用`--base64-output=decode-rows`导致输出的是未解码的内容。

![未解码查看](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8293/155503646337627_zh-CN.png)


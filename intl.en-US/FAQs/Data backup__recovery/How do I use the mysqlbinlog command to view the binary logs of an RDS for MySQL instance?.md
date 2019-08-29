# How do I use the mysqlbinlog command to view the binary logs of an RDS for MySQL instance? {#concept_d5p_pv4_mgb .concept}

You can run the mysqlbinlog command to view specific SQL statements in the binary logs of an RDS for MySQL instance.

## Prerequisites {#section_kzz_4y4_mgb .section}

MySQL has been installed on your Linux-based on-premises host that runs a Linux operating system.

## Procedure {#section_ep1_py4_mgb .section}

1.  [Download data and log backup files](../../../../intl.en-US/User Guide/Backup/Download data and log backup files.md#) on your Linux-based on-premises host that runs MySQL.
2.  Run the following command in the CLI:

    ``` {#codeblock_bf8_65r_lk4}
    mysqlbinlog -vv --base64-output=decode-rows <Save path of binary files>
    ```

    **Note:** 

    -   `-vv`: to view SQL statements and remarks.
    -   `--base64-output=decode-rows`: to decode the content.
    ![解码查看](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8293/156704453137626_en-US.png)


## System errors {#section_xse_y02_i9w .section}

``` {#codeblock_hhk_xox_53m}
ERROR: Error in Log_event::read_log_event(): 'Sanity check failed', data_len: 151, event_type: 35
ERROR: Could not read entry at offset 120: Error in log format or read error.
```

If either of the preceding errors occurs, check the version of the used mysqlbinlog command. For example, if you use Version 3.3, these errors may occur. In such case, you can upgrade the command version.

## Content errors {#section_wwz_x1p_mgb .section}

If you forget to enter `--base64-output=decode-rows`, the displayed content is not decoded, as shown in the following figure.

![未解码查看](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8293/156704453137627_en-US.png)


# Purge Large File Asynchronously {#task_1942041 .task}

AliSQL支持通过异步删除大文件的方式保证系统稳定性。

使用InnoDB引擎时，直接删除大文件会导致POSIX文件系统出现严重的稳定性问题，因此InnoDB会启动一个后台线程来异步清理数据文件。当删除单个表空间时，会将对应的数据文件先重命名为临时文件，然后清除线程将异步、缓慢地清理文件。

**说明：** AliSQL提供清除文件日志来保证DDL语句的原子性。

## 使用方法 {#section_r6h_789_0er .section}

1.  查看实例全局变量设置，示例如下： 

    ``` {#codeblock_l3d_0is_rka}
    mysql> SHOW GLOBAL VARIABLES LIKE '%data_file_purge%';
      +----------------------------------------+-------+
      | Variable_name                          | Value |
      +----------------------------------------+-------+
      | innodb_data_file_purge                 | ON    |
      | innodb_data_file_purge_all_at_shutdown | OFF   |
      | innodb_data_file_purge_dir             |       |
      | innodb_data_file_purge_immediate       | OFF   |
      | innodb_data_file_purge_interval        | 100   |
      | innodb_data_file_purge_max_size        | 128   |
      | innodb_print_data_file_purge_process   | OFF   |
      +----------------------------------------+-------+
    ```

    参数说明如下。

    |参数|说明|
    |--|--|
    |innodb\_data\_file\_purge|是否启用异步清除策略。|
    |innodb\_data\_file\_purge\_all\_at\_shutdown|正常关机时全部清理。|
    |innodb\_data\_file\_purge\_dir|临时文件目录。|
    |innodb\_data\_file\_purge\_immediate|取消数据文件的链接但不清理。|
    |innodb\_data\_file\_purge\_interval|清理时间间隔。单位：ms。|
    |innodb\_data\_file\_purge\_max\_size|每次清理单个文件大小的最大值。单位：MB。|
    |innodb\_print\_data\_file\_purge\_process|是否打印文件清理工作进程。|

    **说明：** 建议使用如下命令进行设置：

    ``` {#codeblock_hwx_hxu_he0}
    set global INNODB_DATA_FILE_PURGE = on;
    set global INNODB_DATA_FILE_PURGE_INTERVAL = 100;
    set global INNODB_DATA_FILE_PURGE_MAX_SIZE = 128;
    ```

2.  使用如下命令查看清理进度： 

    ``` {#codeblock_8ft_xj4_grg}
    select * from information_schema.innodb_purge_files;
    ```



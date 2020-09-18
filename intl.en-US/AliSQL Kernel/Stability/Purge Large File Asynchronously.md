# Purge Large File Asynchronously

This topic describes how to use the Purge Large File Asynchronously function to delete files from an ApsaraDB for RDS instance running AliSQL. This function is designed to ensure database stability by deleting large files asynchronously.

If your ApsaraDB for RDS instance runs the InnoDB storage engine, directly deleting large files from the instance compromises the stability of your POSIX file system. As a result, InnoDB starts a background thread to delete large files asynchronously. InnoDB renames data files housing tablespaces to identify them as temporary files before starting to delete the tablespaces asynchronously.

**Note:** AliSQL ensures the atomicity of Data Definition Language \(DDL\) statements by deleting log files.

## Procedure

1.  View the global variable settings of your RDS instance, as shown in the following example:

    ```
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

    The following table describes these variables.

    |Variable|Description|
    |--------|-----------|
    |innodb\_data\_file\_purge|Specifies whether to enable the Purge Large File Asynchronously function.|
    |innodb\_data\_file\_purge\_all\_at\_shutdown|Specifies whether to delete all files when the host server of your RDS instance is shut down.|
    |innodb\_data\_file\_purge\_dir|The directory for stored temporary files.|
    |innodb\_data\_file\_purge\_immediate|Specifies whether to revoke data file links, but not to delete them.|
    |innodb\_data\_file\_purge\_interval|The intervals at which files are deleted. Unit: ms.|
    |innodb\_data\_file\_purge\_max\_size|The maximum size of a single file that can be deleted. Unit: MB.|
    |innodb\_print\_data\_file\_purge\_process|Specifies whether to display the file deletion process.|

    **Note:** We recommend that you set the following variables to the values provided in the example:

    ```
    set global INNODB_DATA_FILE_PURGE = on;
    set global INNODB_DATA_FILE_PURGE_INTERVAL = 100;
    set global INNODB_DATA_FILE_PURGE_MAX_SIZE = 128;
    ```

2.  Run the following command to view the file deletion progress:

    ```
    select * from information_schema.build_current_task
    ```



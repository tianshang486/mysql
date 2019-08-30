# Restore data from physical backup files of ApsaraDB for MySQL to an on-premises user-created database {#concept_41817_zh .concept}

The open source software Percona XtraBackup can be used to back up and restore databases. This topic describes how to use this software to restore data from physical backup files of ApsaraDB for MySQL to a user-created database.

**Note:** 

-   For more information about how to back up ApsaraDB for MySQL data, see [Back up RDS data](../../../../intl.en-US/User Guide/Backup/Back up RDS data.md#).
-   Percona XtraBackup does not support Windows. For more information about how to back up and restore data in Windows, see [Use mysqldump to migrate MySQL data](../../../../intl.en-US/User Guide/Data migration/Use mysqldump to migrate MySQL data.md#).

## Precautions {#section_bd4_5gz_5fb .section}

This topic describes how to restore data from physical backup files of MySQL 5.7 in Linux 7.

-   Make sure that Percona XtraBackup has been installed. You can download from the Percona XtraBackup official website.

    To restore data of MySQL 5.6 and earlier versions, you must install Percona XtraBackup 2.3. For more information, see [Installing Percona XtraBackup 2.3](https://www.percona.com/doc/percona-xtrabackup/2.3/installation.html).

    To restore data of MySQL 5.7, you must install Percona XtraBackup 2.4. For more information, see [Installing Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html).

-   If your ApsaraDB for MySQL instances use the database engine MySQL 5.6 and are created after February 20, 2019, the backup files of such instances are in xbstream format with the suffix of \_qp.xb.
-   The on-premises MySQL database is installed in a 64-bit Linux system. The version of the database is the same as that of ApsaraDB for MySQL.

**Note:** You can only restore data from backup files of ApsaraDB for MySQL to an on-premises MySQL database in Linux.


## Prerequisites {#section_hqi_9kq_hlg .section}

The database engine of the ApsaraDB for MySQL instance must be in one of the following editions:

-   MySQL 5.7 High-availability Edition \(with local SSDs\)
-   MySQL 5.6
-   MySQL 5.5

## Procedure {#section_ooe_3fz_r97 .section}

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com).
2.  In the upper-left corner of the page, select the region where the instance is located.
3.  Find the instance and click the instance ID.
4.  In the left-side navigation pane, click **Backup and Restoration**.
5.  Click the **Data Backup** tab.
6.  Select a time range that you need to query, then click **Search**.
7.  In the backup list, find the backup file and click **Download**.

    **Note:** If **Download** does not appear, make sure that the version of your instance supports [downloading physical backup files](../../../../intl.en-US/User Guide/Backup/Download data and log backup files.md#).

    ![Download a backup file.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156715265347407_en-US.png)

8.  In the Download Instance Backup Set dialog box that appears, click **Copy External Download URL**.

    ![Copy the external download URL](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156715265447408_en-US.png)

9.  Log on to the ECS instance.
10. Run the following command to download the backup file:

    ``` {#codeblock_8q1_jx0_mvl}
    wget -c '<external download URL>' -O <customized file name>.tar.gz
    					
    ```

    **Note:** 

    -   `-c`: specifies to resume from the breakpoint.
    -   `-O`: specifies a name for the download file \(use the file name suffix .tar.gz, .xb.gz or \_qp.xb as contained in the URL\).
11. Run the following command to decompress the downloaded backup file:

    **Note:** This topic uses the custom path /home/mysql/data as an example. You can replace it with the path of your backup file.

    There are three formats for physical backup files:

    -   tar compressed package \(.tar.gz\)
    -   xbstream compressed package \(.xb.gz\)
    -   xbstream file package \(\_qp.xb\)
    **Note:** If your ApsaraDB for MySQL instances use the database engine MySQL 5.6 and are created after February 20, 2019, the backup files of such instances are in xbstream format with the suffix of \_qp.xb.

    For tar compressed packages \(.tar.gz\), run the following command:

    ``` {#codeblock_xpo_vum_r09}
    tar -izxvf <backup file name>.tar.gz -C /home/mysql/data
    ```

    For xbstream compressed packages \(.xb.gz\), run the following command:

    ``` {#codeblock_o3v_gfv_syk}
    gzip -d -c <backup file name>.xb.gz | xbstream -x -v -C /home/mysql/data
    ```

    For xbstream file packages \(\_qp.xb\), run the following command:

    ``` {#codeblock_y11_9a2_tgq}
    ## Unpack
     cat <backup file name>_qp.xb | xbstream -x -v -C /home/mysql/data
    ## Decompress
    innobackupex --decompress --remove-original /home/mysql/data
    ```

    **Note:** `-C` specifies the directory to decompress the file to. Optional. If you do not specify this parameter, the file is decompressed to the current directory.

12. Run the following command to query the information of the files after decompression:

    ``` {#codeblock_0eg_uzq_fls}
    ls -l /home/mysql/data
    					
    ```

    After the command is executed, the following result is displayed. The information in blue indicates the databases contained in the RDS instance when the backup file was generated.

    ![View the decompressed file](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156715265447410_en-US.jpg)

13. Run the following command to restore the backup file to the on-premises database:

    ``` {#codeblock_1pd_fvx_w4h}
    innobackupex --defaults-file=/home/mysql/data/backup-my.cnf --apply-log /home/mysql/data
    					
    ```

    If the following result is displayed, the backup file is restored to the on-premises database.

    ![Restored](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156715265447412_en-US.jpg)

    **Note:** Make sure that you have installed the proper version of Percona XtraBackup. Install Percona XtraBackup 2.3 for MySQL 5.6 and earlier versions, Percona XtraBackup 2.4 for MySQL 5.7, and Percona XtraBackup 8.0 for MySQL 8.0.

14. To avoid compatibility problems, follow these steps to reconfigure the backup-my.cnf parameter:
    1.  Run the following command to edit the backup-my.cnf file in text:

        ``` {#codeblock_62v_93u_j4y}
        vi /home/mysql/data/backup-my.cnf
        							
        ```

    2.  Comment out the following parameters that are not supported in user-created databases:

        ``` {#codeblock_nl2_snh_63t .language-bash}
        #innodb_log_checksum_algorithm
        #innodb_fast_checksum
        #innodb_log_block_size
        #innodb_doublewrite_file
        #rds_encrypt_data
        #innodb_encrypt_algorithm
        #redo_log_version
        #master_key_id
        ```

        **Note:** 

        -   If your on-premises database uses the MyISAM engine, which is incompatible with the InnoDB engine in ApsaraDB for RDS, you must comment out the following parameters and add the skip-grant-tables parameter:

            ``` {#codeblock_a4z_eiq_jli}
            #innodb_log_checksum_algorithm=strict_crc32
            #redo_log_version=1
            skip-grant-tables
            ```

        -   If your on-premises database uses the MyISAM engine, and error messages related to the storage engine are displayed when you manage system tables, run the following command to switch the storage engine:

            ``` {#codeblock_ksm_3u3_jrp}
            alter engine <table name> engine=myisam;
            ```

    3.  Press the Esc**Esc** key, enter `:wq`, and press the **Enter key** to save.
15. Run the following command to change the owner of the file to the on-premises MySQL user:

    ``` {#codeblock_nat_wuy_eou .language-bash}
    chown -R mysql:mysql /home/mysql/data
    					
    ```

16. Run the following command to start the on-premises MySQL process:

    ``` {#codeblock_s00_cqo_7pc}
    mysqld_safe --defaults-file=/home/mysql/data/backup-my.cnf --user=mysql --datadir=/home/mysql/data &
    					
    ```

17. Run the following command to log on to the on-premises MySQL database to verify that the process has been started:

    ``` {#codeblock_o16_aau_cpg}
     mysql -uroot -p<database password>
    					
    ```

    If the following result is displayed, the parameters are commented out and the owner of the file is changed.

    ![Started](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8199/156715265447413_en-US.jpg)



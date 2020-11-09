# Restore the data of an ApsaraDB RDS for MySQL instance from a logical backup file to a self-managed MySQL instance

This topic describes how to restore the data of an ApsaraDB RDS for MySQL instance from a logical backup file to a self-managed MySQL instance. You can use the mysqldump utility that is provided in MySQL to perform the restoration.

Your RDS instance runs one of the following MySQL versions and RDS editions:

-   MySQL 8.0 on RDS High-availability Edition \(with local SSDs\)
-   MySQL 5.7 on RDS High-availability Edition \(with local SSDs\)
-   MySQL 5.6
-   MySQL 5.5

**Note:**

-   For more information about how to restore data from a physical backup file to a self-managed MySQL instance, see [Use a physical backup file to restore an ApsaraDB RDS for MySQL instance to a user-created MySQL database](/intl.en-US/RDS MySQL Database/Restoration/Use a physical backup file to restore an ApsaraDB RDS for MySQL instance to a user-created
         MySQL database.md).
-   For more information about how to back up the data of an ApsaraDB RDS for MySQL instance, see [Back up the data of an RDS instance]().

## Demo environment

The self-managed MySQL instance runs on a 64-bit Linux operating system. In addition, it runs the same MySQL version as your RDS instance. In this topic, Linux 7 and MySQL 5.7 are used as examples.

## Procedure

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Backup and Restoration**.

5.  Select a time range and click **OK**

6.  In the data backup file list, find the logical backup file that you want to download, and click **Download** in the Actions column.

    **Note:** If **Download** does not appear, check whether the MySQL version of your RDS instance supports the download of logical backup files. For more information, see [Download data and log backup files of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Backup/Download data and log backup files of an ApsaraDB RDS for MySQL instance.md).

7.  In the Download Instance Backup Set dialog box, click ![Copy icon](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2274884061/p130030.png) to the right of **Copy Public Endpoint**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630359951/p32292.png)

8.  Log on to the self-managed MySQL instance and run the following command to download the logical backup file:

    ```
    wget -c '<The URL from which to download the logical backup file over the Internet>' -O <The name to use for the downloaded logical backup file>.tar
    ```

    **Note:**

    -   -c: enables resumable download.
    -   -O: saves the downloaded logical backup file with a specified name.
9.  Run the following command to decompress the logical backup file, which includes the compressed files of the default system databases and the databases that you created:

    ```
    tar xvf <The name of the logical backup file>.tar
    ```

10. Run the following command to decompress the compressed file of the database that you want to restore:

    ```
    gzip -d <The name of the compressed file>.gz
    ```

    **Note:** The .sql file that is generated from the decompression will be imported in Step 12.

11. Run the following commands to log on to the self-managed MySQL instance and create an empty database:

    ```
    mysql -u root -p<The password of the self-managed MySQL database>
    create database <The name of the self-managed MySQL database>;
    exit
    ```

12. Run the following command to import the .sql file into the self-managed MySQL database:

    ```
    mysql -u root -p<The password of the self-managed MySQL database> <The name of the self-managed MySQL database> < ~/<The name of the database that you want to restore on the RDS instance\>.sql
    ```

13. Log on to the self-managed MySQL database and check for table data. If table data exists, the restoration is successful.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8630359951/p32293.png)


## FAQ

Why does my RDS instance not have logical backup files?

The default backup mode is physical backup. You must manually start logical backups if required. For more information, see [Manually back up an RDS instance](/intl.en-US/RDS MySQL Database/Backup/Back up an ApsaraDB RDS for MySQL instance.md).


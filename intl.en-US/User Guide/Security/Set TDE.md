# Set TDE {#concept_jrp_dw4_ydb .concept}

Transparent Data Encryption \(TDE\) can be used to perform real-time I/O encryption and decryption on instance data files. To improve data security, you can enable TDE to encrypt instance data.

After TDE is enabled, data is encrypted before being written to the disk and decrypted when being read from the disk into the memory. TDE does not increase the size of data files. You do not need to modify your applications before using the TDE function.

-   
**Note:** 

-   After TDE is enabled, it cannot be disabled any more.
-   After TDE is enabled, to restore data to a local computer, you need to use RDS to decrypt data first by referring to [Decrypt data](#section_e12_sw4_ydb).
-   After TDE is eabled, CPU usage significantly increases.
-   The key and licence used for encryption are provided by [Key Management Service \(KMS\)](https://www.alibabacloud.com/help/product/28933.htm) rather than RDS.
-   For MySQL 5.6, TDE can be configured only for the entire instance.
-   For SQL Server 2008 R2, TDE can be configured only for the databases.

## Prerequisites {#section_ttb_lw4_ydb .section}

-   The instance is RDS for SQL Server 2008 R2 or RDS for MySQL 5.6.
-   You have logged in with an Alibaba account rather than a RAM user account.
-   KMS has been activated. If KMS has not been activated, you will be prompted to activate it when attempting to enable TDE.

## Procedure {#section_azm_mw4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/) and select the target instance.
2.  Click **Security** in the left-side navigation pane.
3.  On the Security page, click the **SQL TDE** tab.
4.  Click **Disabled**, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7950/15566149894151_en-US.png)

5.  Click **OK** to enable TDE.

    **Note:** If you have not activated KMS, you are prompted to do so.

6.  -   For RDS for MySQL, [connect to the instance](../../../../intl.en-US/Quick Start for MySQL/Connect to an instance.md#) and run the following command to encrypt tables.

    ``` {#codeblock_pjp_77w_ee7}
    alter table <tablename> engine=innodb, block_format=encrypted;
    ```

-   For RDS for SQL Server, click **Configure TDE**, select the databases to encrypt, add them to the right, and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7950/155661498942085_en-US.png)


## Decrypt data {#section_e12_sw4_ydb .section}

-   To decrypt a MySQL table encrypted by TDE, run the following command:

    ```
    alter table <tablename> engine=innodb, block_format=default;
    ```

-   To decrypt a SQL Server table encrypted by TDE, click **Configure TDE** and move the database to the left.

